..
    Warning: Do not edit this file. It is automatically generated from the
    software project's code and your changes will be overwritten.

    The tool to generate this file lives in openstack-doc-tools repository.

    Please make any changes needed in the code, then run the
    autogenerate-config-doc tool from the openstack-doc-tools repository, or
    ask for help on the documentation mailing list, IRC channel or meeting.

.. _keystone-auth_token:

.. list-table:: Description of authorization token configuration options
   :header-rows: 1
   :class: config-ref-table

   * - Configuration option = Default value
     - Description
   * - **[keystone_authtoken]**
     -
   * - ``admin_password`` = ``None``
     - (String) Service user password.
   * - ``admin_tenant_name`` = ``admin``
     - (String) Service tenant name.
   * - ``admin_token`` = ``None``
     - (String) This option is deprecated and may be removed in a future release. Single shared secret with the Keystone configuration used for bootstrapping a Keystone installation, or otherwise bypassing the normal authentication process. This option should not be used, use `admin_user` and `admin_password` instead.
   * - ``admin_user`` = ``None``
     - (String) Service username.
   * - ``auth_admin_prefix`` =
     - (String) Prefix to prepend at the beginning of the path. Deprecated, use identity_uri.
   * - ``auth_host`` = ``127.0.0.1``
     - (String) Host providing the admin Identity API endpoint. Deprecated, use identity_uri.
   * - ``auth_port`` = ``35357``
     - (Integer) Port of the admin Identity API endpoint. Deprecated, use identity_uri.
   * - ``auth_protocol`` = ``https``
     - (String) Protocol of the admin Identity API endpoint. Deprecated, use identity_uri.
   * - ``auth_section`` = ``None``
     - (Unknown) Config Section from which to load plugin specific options
   * - ``auth_type`` = ``None``
     - (Unknown) Authentication type to load
   * - ``auth_uri`` = ``None``
     - (String) Complete public Identity API endpoint.
   * - ``auth_version`` = ``None``
     - (String) API version of the admin Identity API endpoint.
   * - ``cache`` = ``None``
     - (String) Env key for the swift cache.
   * - ``cafile`` = ``None``
     - (String) A PEM encoded Certificate Authority to use when verifying HTTPs connections. Defaults to system CAs.
   * - ``certfile`` = ``None``
     - (String) Required if identity server requires client certificate
   * - ``check_revocations_for_cached`` = ``False``
     - (Boolean) If true, the revocation list will be checked for cached tokens. This requires that PKI tokens are configured on the identity server.
   * - ``delay_auth_decision`` = ``False``
     - (Boolean) Do not handle authorization requests within the middleware, but delegate the authorization decision to downstream WSGI components.
   * - ``enforce_token_bind`` = ``permissive``
     - (String) Used to control the use and type of token binding. Can be set to: "disabled" to not check token binding. "permissive" (default) to validate binding information if the bind type is of a form known to the server and ignore it if not. "strict" like "permissive" but if the bind type is unknown the token will be rejected. "required" any form of token binding is needed to be allowed. Finally the name of a binding method that must be present in tokens.
   * - ``hash_algorithms`` = ``md5``
     - (List) Hash algorithms to use for hashing PKI tokens. This may be a single algorithm or multiple. The algorithms are those supported by Python standard hashlib.new(). The hashes will be tried in the order given, so put the preferred one first for performance. The result of the first hash will be stored in the cache. This will typically be set to multiple values only while migrating from a less secure algorithm to a more secure one. Once all the old tokens are expired this option should be set to a single value for better performance.
   * - ``http_connect_timeout`` = ``None``
     - (Integer) Request timeout value for communicating with Identity API server.
   * - ``http_request_max_retries`` = ``3``
     - (Integer) How many times are we trying to reconnect when communicating with Identity API Server.
   * - ``identity_uri`` = ``None``
     - (String) Complete admin Identity API endpoint. This should specify the unversioned root endpoint e.g. https://localhost:35357/
   * - ``include_service_catalog`` = ``True``
     - (Boolean) (Optional) Indicate whether to set the X-Service-Catalog header. If False, middleware will not ask for service catalog on token validation and will not set the X-Service-Catalog header.
   * - ``insecure`` = ``False``
     - (Boolean) Verify HTTPS connections.
   * - ``keyfile`` = ``None``
     - (String) Required if identity server requires client certificate
   * - ``memcache_pool_conn_get_timeout`` = ``10``
     - (Integer) (Optional) Number of seconds that an operation will wait to get a memcached client connection from the pool.
   * - ``memcache_pool_dead_retry`` = ``300``
     - (Integer) (Optional) Number of seconds memcached server is considered dead before it is tried again.
   * - ``memcache_pool_maxsize`` = ``10``
     - (Integer) (Optional) Maximum total number of open connections to every memcached server.
   * - ``memcache_pool_socket_timeout`` = ``3``
     - (Integer) (Optional) Socket timeout in seconds for communicating with a memcached server.
   * - ``memcache_pool_unused_timeout`` = ``60``
     - (Integer) (Optional) Number of seconds a connection to memcached is held unused in the pool before it is closed.
   * - ``memcache_secret_key`` = ``None``
     - (String) (Optional, mandatory if memcache_security_strategy is defined) This string is used for key derivation.
   * - ``memcache_security_strategy`` = ``None``
     - (String) (Optional) If defined, indicate whether token data should be authenticated or authenticated and encrypted. If MAC, token data is authenticated (with HMAC) in the cache. If ENCRYPT, token data is encrypted and authenticated in the cache. If the value is not one of these options or empty, auth_token will raise an exception on initialization.
   * - ``memcache_use_advanced_pool`` = ``False``
     - (Boolean) (Optional) Use the advanced (eventlet safe) memcached client pool. The advanced pool will only work under python 2.x.
   * - ``region_name`` = ``None``
     - (String) The region in which the identity server can be found.
   * - ``revocation_cache_time`` = ``10``
     - (Integer) Determines the frequency at which the list of revoked tokens is retrieved from the Identity service (in seconds). A high number of revocation events combined with a low cache duration may significantly reduce performance.
   * - ``signing_dir`` = ``None``
     - (String) Directory used to cache files related to PKI tokens.
   * - ``token_cache_time`` = ``300``
     - (Integer) In order to prevent excessive effort spent validating tokens, the middleware caches previously-seen tokens for a configurable duration (in seconds). Set to -1 to disable caching completely.
