.. _section-compute-pci-passthrough:

========================================
Attaching physical PCI devices to guests
========================================

The PCI passthrough feature in OpenStack allows full access and direct
control of a physical PCI device in guests. This mechanism is generic for any
kind of PCI devices (for example: Network Interface Card (NIC), Graphics
Processing Unit (GPU) or any other devices that can be attached to a PCI bus).
Correct driver installation is the only requirement for the guest to properly
use the devices.

PCI devices, if supported by the hardware, can provide Single Root I/O
Virtualization and Sharing (SR-IOV) functionality. In this case, a physical
device is virtualized and appears as multiple PCI devices. Virtual PCI
devices are assigned to the same or different guests. In the case of PCI
passthrough, the full physical device is assigned to only one guest and cannot
be shared.

.. note::

   For Attaching virtual SR-IOV devices to guests, refer to the
   `Networking Guide`_.

To enable PCI passthrough, follow the steps below:

#. Enable PCI passthrough (Compute)
#. Configure PCI devices in nova-compute (Compute)
#. Configure nova-scheduler (Controller)
#. Configure nova-api (Controller)**
#. Configure a flavor (Controller)

.. note::

   The PCI device with address ``0000:41:00.0`` is as an example. Expect
   to change this according to your actual environment.

Enable PCI passthrough (Compute)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Enable VT-d and IOMMU. For more information, refer to steps one and two
in `Create Virtual Functions`_.

Configure PCI devices nova-compute (Compute)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Configure ``nova-compute`` to allow the PCI device to be passed through to
   VMs. Edit ``/etc/nova/nova.conf``:

   .. code-block:: ini

      [default]
      pci_passthrough_whitelist = { "address": "0000:41:00.0" }

   Alternatively specify multiple PCI devices using whitelisting:

   .. code-block:: ini

      [default]
      pci_passthrough_whitelist = { "vendor_id": "8086", "product_id": "10fb" }

   All PCI devices matching the ``vendor_id`` and ``product_id`` are added to
   the pool of PCI devices available for passthrough to VMs.

   For more information about the syntax of ``pci_passthrough_whitelist``,
   refer to `nova.conf configuration options`_.

#. Restart ``nova-compute`` with :command:`service nova-compute restart`.

Configure nova-scheduler (Controller)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Configure ``nova-scheduler`` as specified in `Configure nova-scheduler`_.

#. Restart ``nova-scheduler`` with :command:`service nova-scheduler restart`.

Configure nova-api (Controller)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Specify the PCI alias for the device.

   Configure a PCI alias ``a1`` to request a PCI device with a ``vendor_id`` of
   ``0x8086`` and a ``product_id`` of ``0x154d``. The ``vendor_id`` and
   ``product_id`` correspond the PCI device with address ``0000:41:00.0``.

   Edit ``/etc/nova/nova.conf``:

   .. code-block:: ini

      [default]
      pci_alias = { "vendor_id":"8086", "product_id":"154d", "device_type":"type-PF", "name":"a1" }

   For more information about the syntax of ``pci_alias``, refer to
   `nova.conf configuration options`_.

#. Restart ``nova-api`` with :command:`service nova-api restart`.

Configure a flavor (Controller)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configure a flavor to request two PCI devices, each with ``vendor_id`` as
``0x8086`` and ``product_id`` as ``0x154d``.

.. code-block:: console

   # openstack flavor set m1.large --property "pci_passthrough:alias"="a1:2"

For more information about the syntax for ``pci_passthrough:alias``, refer to
`flavor`_.

Create instances with PCI passthrough devices
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``nova-scheduler`` selects a destination host that has PCI devices
available with the specified ``vendor_id`` and ``product_id`` that matches
the ``pci_alias`` from the flavor.

.. code-block:: console

   # openstack server create --flavor m1.large --image cirros-0.3.4-x86_64-uec --wait test-pci

.. Links
.. _`Create Virtual Functions`: http://docs.openstack.org/mitaka/networking-guide/adv-config-sriov.html#create-virtual-functions-compute
.. _`Configure nova-scheduler`: http://docs.openstack.org/mitaka/networking-guide/adv-config-sriov.html#configure-nova-scheduler-controller
.. _`nova.conf configuration options`: http://docs.openstack.org/mitaka/config-reference/compute/config-options.html
.. _`flavor`: http://docs.openstack.org/admin-guide/compute-flavors.html
.. _`Networking Guide`: http://docs.openstack.org/mitaka/networking-guide/adv-config-sriov.html
