=============
Customization
=============

.. toctree::
   :maxdepth: 1

   ops_customize_development.rst
   ops_customize_objectstorage.rst
   ops_customize_compute.rst
   ops_customize_dashboard.rst
   ops_customize_conclusion.rst

OpenStack might not do everything you need it to do out of the box. To
add a new feature, you can follow different paths.

To take the first path, you can modify the OpenStack code directly.
Learn `how to contribute
<https://wiki.openstack.org/wiki/How_To_Contribute>`_,
follow the `Developer's Guide
<http://docs.openstack.org/infra/manual/developers.html>`_, make your
changes, and contribute them back to the upstream OpenStack project.
This path is recommended if the feature you need requires deep
integration with an existing project. The community is always open to
contributions and welcomes new functionality that follows the
feature-development guidelines. This path still requires you to use
DevStack for testing your feature additions, so this chapter walks you
through the DevStack environment.

For the second path, you can write new features and plug them in using
changes to a configuration file. If the project where your feature would
need to reside uses the Python Paste framework, you can create
middleware for it and plug it in through configuration. There may also
be specific ways of customizing a project, such as creating a new
scheduler driver for Compute or a custom tab for the dashboard.

This chapter focuses on the second path for customizing OpenStack by
providing two examples for writing new features.
The first example shows how to modify Object Storage service (swift)
middleware to add a new feature, and the second example provides a new
scheduler feature for Compute service (nova).
To customize OpenStack this way you need a development environment.
The best way to get an environment up and running quickly is to run
DevStack within your cloud.
