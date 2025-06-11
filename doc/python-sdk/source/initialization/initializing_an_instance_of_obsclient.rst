:original_name: obs_22_0601.html

.. _obs_22_0601:

Initializing an Instance of ObsClient
=====================================

Function
--------

ObsClient functions as the Python client for accessing OBS. It offers users a series of APIs for interaction with OBS. These APIs are used for managing resources, such as buckets and objects, stored in OBS.

Method
------

.. code-block::

   ObsClient(access_key_id, secret_access_key, server)

Constructor Parameter Description
---------------------------------

+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| Parameter                | Description                                                                                                                                                                                                                            | Recommended Value     |
+==========================+========================================================================================================================================================================================================================================+=======================+
| access_key_id            | Access key ID (AK). It is left blank by default, which indicates that anonymous users are allowed for access.                                                                                                                          | N/A                   |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| secret_access_key        | Secret access key (SK). It is left blank by default, which indicates that anonymous users are allowed for access.                                                                                                                      | N/A                   |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| security_token           | Security token in the temporary access keys.                                                                                                                                                                                           | N/A                   |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| server                   | Server address for accessing OBS. It consists of a protocol type, domain name, and port number, for example, **https://**\ *your-endpoint*\ **:443**. For security purposes, you are advised to use HTTPS.                             | N/A                   |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| max_retry_count          | Maximum number of retries when an HTTP/HTTPS connection is abnormal. The default value is **3**.                                                                                                                                       | [1,5]                 |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| max_redirect_count       | Maximum number of times that the HTTP/HTTPS request is redirected. The default value is **10**.                                                                                                                                        | [1,10]                |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| timeout                  | Timeout period (in seconds) of an HTTP/HTTPS request. The default value is **60**.                                                                                                                                                     | [10,60]               |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| ssl_verify               | Client-to-server certificate verification used to check whether the client certificate matches the server certificate. The options are as follows:                                                                                     | N/A                   |
|                          |                                                                                                                                                                                                                                        |                       |
|                          | -  Path to the server-side root certificate file in PEM format                                                                                                                                                                         |                       |
|                          | -  **True**: The certificate list will be obtained from the root certificate library and the certificates of the operating system (Windows only) will be verified.                                                                     |                       |
|                          | -  **False**: The server-side certificates will not be verified.                                                                                                                                                                       |                       |
|                          |                                                                                                                                                                                                                                        |                       |
|                          | The default value is **False**.                                                                                                                                                                                                        |                       |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| chunk_size               | Chunk size (in bytes) set for reading and writing socket streams. The default value is **65536**.                                                                                                                                      | Default               |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| long_conn_mode           | Whether to enable the persistent connection mode. The default value is **False**.                                                                                                                                                      | N/A                   |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| proxy_host               | Host IP address of the proxy server. This value is left blank by default.                                                                                                                                                              | N/A                   |
|                          |                                                                                                                                                                                                                                        |                       |
|                          | .. note::                                                                                                                                                                                                                              |                       |
|                          |                                                                                                                                                                                                                                        |                       |
|                          |    Do not specify **http://** or **https://** for the proxy server's host address.                                                                                                                                                     |                       |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| proxy_port               | Port number of the proxy server. This value is left blank by default.                                                                                                                                                                  | N/A                   |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| proxy_username           | User name used for connecting to the proxy server. This value is left blank by default.                                                                                                                                                | N/A                   |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| proxy_password           | Password used for connecting to the proxy server. This value is left blank by default.                                                                                                                                                 | N/A                   |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| is_cname                 | Whether to use a user-defined domain name to access OBS. The default value is **False**.                                                                                                                                               | N/A                   |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| security_providers       | How an access key is obtained. The default value is **None**.                                                                                                                                                                          | N/A                   |
|                          |                                                                                                                                                                                                                                        |                       |
|                          | .. note::                                                                                                                                                                                                                              |                       |
|                          |                                                                                                                                                                                                                                        |                       |
|                          |    The value of **security_providers** must be in a list. The default value **None** indicates the default search methods to obtain the access keys from the environment variables or from ECSs.                                       |                       |
|                          |                                                                                                                                                                                                                                        |                       |
|                          |    If this parameter is specified, the default search methods are not provided. Instead, the search methods specified by **security_providers** are used.                                                                              |                       |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| security_provider_policy | Specifies the allowed access key search policy. The default value is **None**.                                                                                                                                                         | N/A                   |
|                          |                                                                                                                                                                                                                                        |                       |
|                          | .. note::                                                                                                                                                                                                                              |                       |
|                          |                                                                                                                                                                                                                                        |                       |
|                          |    -  This parameter is used to set the search policy. The default value **None** indicates the specified access keys are displayed. In addition, if the access key parameters are specified, **security_provider_policy** is ignored. |                       |
|                          |    -  If **security_provider_policy** is set to **OBS_DEFAULT**, the access keys are obtained by searching in sequence.                                                                                                                |                       |
|                          |    -  If **security_provider_policy** is set to the predefined methods (ENV or ECS), the access keys are obtained using the corresponding method.                                                                                      |                       |
+--------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

.. note::

   -  Parameters whose recommended value is **N/A** need to be set according to the actual conditions.
   -  If the network is unstable, you are advised to set a larger value for **timeout**.
   -  If the value of **server** does not contain any protocol, HTTPS is used by default.

.. important::

   -  If the persistent connection mode is enabled, you must call **ObsClient.close** to close ObsClient explicitly to reclaim connection resources.
   -  For the sake of high DNS resolution performance and OBS reliability, you can set **server** only to the domain name of OBS, instead of the IP address.

Code Examples
-------------

-  You can create an instance of ObsClient by using a constructor function. Sample code for creating an instance of ObsClient using permanent access keys (AK/SK):

   .. code-block::

      # Import the module.
      from obs import ObsClient

      # Obtain an AK and SK pair using environment variables or import the AK and SK pair in other ways. Using hard coding may result in leakage.
      # Obtain an AK and SK pair on the management console.
      ak = os.getenv("AccessKeyID")
      sk = os.getenv("SecretAccessKey")
      # Set server to the endpoint of the region where the bucket is located.
      server = "https://your-endpoint"

      # Create an obsClient instance.
      Specify a security token.
      obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)

      # Use the instance to access OBS.

      # Close ObsClient.
      obsClient.close()

-  Sample code for creating an instance of ObsClient using temporary access keys (AK/SK and security token):

   .. code-block::

      # Import the module.
      from obs import ObsClient

      # Obtain an AK and SK pair using environment variables or import the AK and SK pair in other ways. Using hard coding may result in leakage.
      # Obtain an AK and SK pair on the management console.
      ak = os.getenv("AccessKeyID")
      sk = os.getenv("SecretAccessKey")
      # (Optional) If you use a temporary AK and SK pair and a security token to access OBS, obtain them from environment variables.
      security_token = os.getenv("SecurityToken")
      # Set server to the endpoint of the region where the bucket is located.
      server = "https://your-endpoint"

      # Create an obsClient instance.
      # If you use a temporary AK and SK pair and a security token to access OBS, you must specify security_token when creating an instance.
      obsClient = ObsClient(
          access_key_id=ak,
          secret_access_key=sk,
          server=server,
          security_token=security_token
      )

      # Use the instance to access OBS.

      # Close ObsClient.
      obsClient.close()

-  Specify the method of obtaining temporary access keys:

   -  Sample code for obtaining the access key from environment variables using a single method:

      .. code-block::

         # Import the module.
         from obs import ObsClient
         from obs import loadtoken

         # Create an instance of ObsClient.
         # Provide ENV to obtain the access keys.
         obsClient = ObsClient(
             server='https://your-endpoint',
             security_providers=[loadtoken.ENV]
         )

         # Use the instance to access OBS.

         # Close ObsClient.
         obsClient.close()

-  You can also create an instance of ObsClient by using temporary access keys obtained by configuring system environment variables or by accessing an ECS.

   -  Sample code for creating an instance of ObsClient using ENV:

      .. code-block::

         # Import the module.
         from obs import ObsClient

         # Create an instance of ObsClient.
         # Provide ENV to obtain the access keys.
         obsClient = ObsClient(
             server='https://your-endpoint',
             security_provider_policy='ENV'
         )

         # Use the instance to access OBS.

         # Close ObsClient.
         obsClient.close()

      .. note::

         In the preceding method, access keys are searched from the environment variables of the current system. The **OBS_ACCESS_KEY_ID** and **OBS_SECRET_ACCESS_KEY** fields need to be defined in the corresponding environment variables. If temporary access keys are used, the **OBS_SECURITY_TOKEN** field must also be defined in the environment variables.

   -  Sample code for creating an instance of ObsClient using ECS:

      .. code-block::

         # Import the module.
         from obs import ObsClient

         # Create an instance of ObsClient.
         # Provide ECS to obtain the temporary access keys.
         obsClient = ObsClient(
             server='https://your-endpoint',
             security_provider_policy='ECS'
         )

         # Use the instance to access OBS.

         # Close ObsClient.
         obsClient.close()

      .. note::

         When an application is deployed on an ECS, temporary access keys can be obtained automatically using the preceding methods and updated periodically.

         If the client reports error 401, check whether an agency has been added during ECS creation.

      .. important::

         When obtaining temporary access keys using this method, ensure that the UTC time of the server is the same as that of the environment where the application is deployed. Otherwise, the temporary access keys may fail to be updated.

-  In addition to the preceding methods, you can also search in sequence to obtain the corresponding access keys from the environment variables and ECSs.

   -  You can set **security_provider_policy** to **OBS_DEFAULT** to specify that ObsClient searches for access keys in sequence.

      .. code-block::

         # Import the module.
         from obs import ObsClient

         # Create an instance of ObsClient.
         # Search for access keys from environment variables and ECSs in sequence.
         obsClient = ObsClient(
             server='https://your-endpoint',
             security_provider_policy='OBS_DEFAULT'
         )

         # Use the instance to access OBS.

         # Close ObsClient.
         obsClient.close()

      .. note::

         In the preceding method, **security_provider_policy** is set to **OBS_DEFAULT**, which specifies that ObsClient searches for access keys in sequence from the predefined list. By default, the system provides two predefined search methods: obtaining the access keys from the environment variables and obtaining from ECSs. ObsClient searches for the access keys from the environment variables first and then from ECSs. In this case, ObsClient is created using the first pair of access keys obtained in the search.

.. note::

   -  The project can contain one or more instances of **ObsClient**.

   -  ObsClient is thread secure and can be simultaneously used by multiple threads.
