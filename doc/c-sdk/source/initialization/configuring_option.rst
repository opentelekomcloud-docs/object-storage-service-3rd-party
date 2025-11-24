:original_name: obs_20_0203.html

.. _obs_20_0203:

Configuring **option**
======================

When the function of SDK for C is called, the **obs_options** parameter must be passed. You can use function **init_obs_options** to initialize the **obs_options** configuration, including the AK, SK, endpoint, bucket, timeout, and temporary authentication. **obs_options** consists of **obs_bucket_context** and **obs_http_request_option**. The following table describes the parameters that can be set.

.. table:: **Table 1** obs_options.obs_bucket_context parameters

   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------+
   | Parameter         | Description                                                                                                                          | Default Value                            | Recommended Value  |
   +===================+======================================================================================================================================+==========================================+====================+
   | host_name         | The requested host name, which is the domain name (the endpoint) of the server where the requested resource is stored.               | NULL                                     | ``-``              |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------+
   | bucket_name       | Name of the bucket where the operation is performed                                                                                  | NULL                                     | ``-``              |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------+
   | protocol          | The protocol used for sending requests. Possible values include HTTP and HTTPS. For security purposes, you are advised to use HTTPS. | HTTPS protocol: OBS_PROTOCOL_HTTPS       | OBS_PROTOCOL_HTTPS |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------+
   | access_key        | AK of OBS                                                                                                                            | NULL                                     | ``-``              |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------+
   | secret_access_key | SK used for authentication. It can be used to sign a character string.                                                               | NULL                                     | ``-``              |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------+
   | obs_storage_class | Set this parameter when the storage class needs to be configured in the PUT or POST request.                                         | OBS Standard: OBS_STORAGE_CLASS_STANDARD | Default value      |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------+
   | token             | Security token of the temporary access key                                                                                           | NULL                                     | ``-``              |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+--------------------+

.. table:: **Table 2** obs_options.obs_http_request_option parameters

   +--------------------+----------------------------------------------------------------------------------------------------------------+---------------+-------------------+
   | Parameter          | Description                                                                                                    | Default Value | Recommended Value |
   +====================+================================================================================================================+===============+===================+
   | connect_time       | Timeout period for establishing an HTTP/HTTPS connection, in ms. The default value is **60,000**.              | 60000         | 10000 to 60000    |
   +--------------------+----------------------------------------------------------------------------------------------------------------+---------------+-------------------+
   | max_connected_time | Timeout period (in seconds) of an HTTP/HTTPS request. The value 0 indicates that there is never disconnection. | 0             | 0                 |
   +--------------------+----------------------------------------------------------------------------------------------------------------+---------------+-------------------+
   | proxy_auth         | Proxy authentication information, in the format *username*\ **:**\ *password*                                  | NULL          | ``-``             |
   +--------------------+----------------------------------------------------------------------------------------------------------------+---------------+-------------------+
   | proxy_host         | Proxy server                                                                                                   | NULL          | ``-``             |
   +--------------------+----------------------------------------------------------------------------------------------------------------+---------------+-------------------+

.. note::

   If the network is unstable, you are advised to set larger values for **connect_time** and **max_connected_time**.
