:original_name: obs_33_0102.html

.. _obs_33_0102:

ObsClient Initialization
========================

Function
--------

**ObsClient** functions as the Go client for accessing OBS. It offers users a series of APIs for interaction with OBS. These APIs are used for managing and operating resources, such as buckets and objects, stored in OBS. To use the OBS Go SDK to send a request to OBS, you need to initialize an instance of ObsClient and modify configuration parameters of the instance based on actual needs.

Initialization Method
---------------------

.. code-block::

   func New(ak, sk, endpoint string, configurers ...configurer) (*ObsClient, error)

Parameters
----------

+---------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter     | Type                                                       | Mandatory (Yes/No) | Description                                                                                                                                                                                          |
+===============+============================================================+====================+======================================================================================================================================================================================================+
| ak            | string                                                     | Yes                | Access key ID (AK)                                                                                                                                                                                   |
+---------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| sk            | string                                                     | Yes                | Secret access key (SK)                                                                                                                                                                               |
+---------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| endpoint      | string                                                     | Yes                | Endpoint for accessing OBS, which contains the protocol type, domain name (or IP address), and port ID. For example, https://your-endpoint:443. For security purposes, you are advised to use HTTPS. |
+---------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| securityToken | string                                                     | No                 | The security token in temporary security credentials.                                                                                                                                                |
+---------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| configurers   | configurer (private type contained in the **obs** package) | No                 | A group of parameters used to configure **ObsClient**, including connection timeout period, maximum retries, and maximum number of connections.                                                      |
+---------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Available Configurers
---------------------

You can use configurers (private type provided by the **obs** namespace) to configure **ObsClient**. The following table lists available configurers:

+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| Configurer                                                | Description                                                                                                              | Recommended Value |
+===========================================================+==========================================================================================================================+===================+
| WithSslVerifyAndPemCerts(sslVerify bool, pemCerts []byte) | Specifies whether to verify server-side certificates. Server-side certificates will not be verified by default.          | N/A               |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithHeaderTimeout(headerTimeout int)                      | Specifies the timeout period of obtaining the response headers. The default value is **60**, in seconds.                 | [10, 60]          |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithMaxConnections(maxIdleConns int)                      | Specifies the maximum number of idle HTTP connections. The default value is 1000.                                        | N/A               |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithConnectTimeout(connectTimeout int)                    | Specifies the timeout period for establishing an HTTP/HTTPS connection, in seconds. The default value is **60**.         | [10, 60]          |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithSocketTimeout(socketTimeout int)                      | Specifies the timeout duration for transmitting data at the socket layer, in seconds. The default value is **60**.       | [10, 60]          |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithIdleConnTimeout(idleConnTimeout int)                  | Specifies the timeout period of an idle HTTP connection in the connection pool, in seconds. The default value is **30**. | Default           |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithMaxRetryCount(maxRetryCount int)                      | Specifies the maximum number of retries when an HTTP/HTTPS connection is abnormal. The default value is **3**.           | [1, 5]            |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithProxyUrl(proxyUrl string)                             | Configures the HTTP proxy.                                                                                               | N/A               |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithCustomDomainName(cname bool)                          | Whether to use a custom domain name to access OBS. The default value is **false**.                                       | Default           |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithHttpTransport(transport \*http.Transport)             | Configures custom structs of the **Transport** type.                                                                     | Default           |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithRequestContext(ctx context.Context)                   | Configures the context for each HTTP request.                                                                            | N/A               |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithMaxRedirectCount(maxRedirectCount int)                | Specifies the maximum number of times that the HTTP/HTTPS request is redirected. The default value is **3**.             | [1, 5]            |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+
| WithSecurityToken(securityToken string)                   | Specifies security token in the temporary access keys.                                                                   | N/A               |
+-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+-------------------+

.. note::

   -  Parameters whose recommended value is **N/A** need to be set according to the actual conditions.
   -  If the network is unstable, you are advised to set larger values for **WithConnectTimeout** and **WithSocketTimeout**.

Code Examples
-------------

-  You can call **New** to create an instance of ObsClient. Sample code for creating an instance of ObsClient using permanent access keys (AK/SK):

   ::

      // Import the dependency package.
      import (
          "obs-sdk-go/obs"
      )

      func main() {
          //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
          //Obtain an AK/SK pair on the management console.    ak := os.Getenv("AccessKeyID")
          sk := os.Getenv("SecretAccessKey")
          // Enter the endpoint of the region where the bucket is located.
          endPoint := "https://your-endpoint"
          // Create an obsClient instance.
          obsClient, err := obs.New(ak, sk, endPoint)
          if err == nil {
               // Use the obsClient to access OBS.

               // Close the obsClient.
               obsClient.Close()
          }
      }

-  Sample code for creating an ObsClient instance with a proxy:

   ::

      // Import the dependency package.
      import (
             "obs"
      )

      func main() {
          //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
          //Obtain an AK/SK pair on the management console.    ak := os.Getenv("AccessKeyID")
          sk := os.Getenv("SecretAccessKey")
          // Enter the endpoint of the region where the bucket is located.
          endPoint := "https://your-endpoint"
          // Create an obsClient instance.
          obsClient, err := obs.New(ak, sk, endPoint, obs.WithProxyUrl("https://username:password!@yourProxy"))
          if err == nil {
               // Use the obsClient to access OBS.

               // Close the obsClient.
               obsClient.Close()
          }
      }

-  Sample code for creating an instance of ObsClient using temporary access keys (AK/SK and security token):

   ::

      // Import the dependency package.
      import (
          "obs-sdk-go/obs"
      )

      func main() {
          //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
          //Obtain an AK/SK pair on the management console.    ak := os.Getenv("AccessKeyID")
          sk := os.Getenv("SecretAccessKey")
          // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import it in other ways.
          // securityToken := os.Getenv("SecurityToken")
          // Enter the endpoint of the region where the bucket is located.
          endPoint := "https://your-endpoint"
          // Create an obsClient instance.
          // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
          obsClient, err := obs.New(ak, sk, endPoint, obs.WithSecurityToken(securityToken))
          if err == nil {
               // Use the obsClient to access OBS.

               // Close the obsClient.
               obsClient.Close()
          }
      }

-  You can also create an instance of ObsClient by using temporary access keys obtained by configuring system environment variables or by accessing an ECS.

   -  Sample code for creating an instance of ObsClient using access keys obtained from environment variables:

      ::

         // Import the dependency package.
         import (
             "obs-sdk-go/obs"
         )

         func main() {
             //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
             //Obtain an AK/SK pair on the management console.    ak := os.Getenv("AccessKeyID")
             sk := os.Getenv("SecretAccessKey")
             // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import it in other ways.
             // securityToken := os.Getenv("SecurityToken")
             // Enter the endpoint of the region where the bucket is located.
             endPoint := "https://your-endpoint"
             // Create an obsClient instance.
             // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
             obsClient, err := obs.New(ak, sk, endPoint, obs.WithSecurityProviders(obs.NewEnvSecurityProvider(""))
             if err == nil {
                  // Use the obsClient to access OBS.

                  // Close the obsClient.
                  obsClient.Close()
             }
         }

      .. note::

         In the preceding method, access keys are searched from the environment variables in the current system. The **OBS_ACCESS_KEY_ID** and **OBS_SECRET_ACCESS_KEY** fields need to be defined in the corresponding environment variables. If temporary access keys are also used, the **OBS_SECURITY_TOKEN** field must also be defined in the environment variables.

   -  Sample code for creating an instance of ObsClient by obtaining temporary access keys from an ECS:

      ::

         // Import the dependency package.
         import (
             "obs-sdk-go/obs"
         )

         func main() {
             //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
             //Obtain an AK/SK pair on the management console.    ak := os.Getenv("AccessKeyID")
             sk := os.Getenv("SecretAccessKey")
             // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import it in other ways.
             // securityToken := os.Getenv("SecurityToken")
             // Enter the endpoint of the region where the bucket is located.
             endPoint := "https://your-endpoint"
             // Create an obsClient instance.
             // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
             obsClient, err := obs.New(ak, sk, endPoint, obs.WithSecurityProviders(obs.NewEcsSecurityProvider(1))
             if err == nil {
                  // Use the obsClient to access OBS.

                  // Close the obsClient.
                  obsClient.Close()
             }
         }

      .. note::

         If an application is deployed on an ECS and the ECS has relevant agencies bound, you can use the preceding method to automatically obtain temporary access keys from the ECS.

   -  Sample code for creating an instance of ObsClient by obtaining access keys from system environment variables or ECSs in sequence:

      ::

         // Import the dependency package.
         import (
             "obs-sdk-go/obs"
         )

         func main() {
             //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
             //Obtain an AK/SK pair on the management console.    ak := os.Getenv("AccessKeyID")
             sk := os.Getenv("SecretAccessKey")
             // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import it in other ways.
             // securityToken := os.Getenv("SecurityToken")
             // Enter the endpoint of the region where the bucket is located.
             endPoint := "https://your-endpoint"
             // Create an obsClient instance.
             // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
             obsClient, err := obs.New(ak, sk, endPoint,
               obs.WithSecurityProviders(obs.NewEnvSecurityProvider(""), obs.NewEcsSecurityProvider(1))
             )
             if err == nil {
                  // Use the obsClient to access OBS.

                  // Close the obsClient.
                  obsClient.Close()
             }
         }

      .. note::

         In the preceding initialization process, access keys are obtained from environment variables and ECSs in sequence, and the first group of obtained access keys is used to create an ObsClient.

.. note::

   -  The project can contain one or more instances of ObsClient.

   -  ObsClient is thread-safe and can be simultaneously used by multiple threads.
   -  After you call the **ObsClient.close** method to close an instance of **ObsClient**, the instance cannot be used anymore.

-  You can call **WithHttpTransport** to pass a user-defined **Transport** parameter that specifies maximum connections for a single host. The sample code is as follows:

   ::

      // Import the dependency package.
      import (
             "time"
          "obs-sdk-go/obs"
      )

      // Create an obsClient struct.
      var obsClient, err = obs.New(ak, sk, endpoint, obs.WithHttpTransport(transport))

      func main() {
          //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
          //Obtain an AK/SK pair on the management console.    ak := os.Getenv("AccessKeyID")
          sk := os.Getenv("SecretAccessKey")
          // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import it in other ways.
          // securityToken := os.Getenv("SecurityToken")
          // Enter the endpoint of the region where the bucket is located.
          endPoint := "https://your-endpoint"
          // Initialize the user-defined transport.
          var maxIdleConns = 1000
          var maxConnsPerHost = 1000
          var idleConnTimeout = 30
          var transport = &http.Transport{
              MaxIdleConns:        maxIdleConns,
              MaxIdleConnsPerHost: maxIdleConns,
              MaxConnsPerHost:     maxConnsPerHost,
              IdleConnTimeout:     time.Second * time.Duration(idleConnTimeout),
          }
          // Create an obsClient instance.
          // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
          obsClient, err := obs.New(ak, sk, endPoint,obs.WithHttpTransport(transport))

          if err == nil {
              // Use the obsClient to access OBS.
              // Close the obsClient.
              obsClient.Close()
          }
      }

   .. important::

      -  The **MaxConnsPerHost** parameter can be specified in the **Transport** struct only in Golang 1.11 and later versions.
      -  If a user-defined **Transport** is specified, the maximum number of idle connections and proxy can only be configured in **Transport**, rather than through the methods **WithMaxConnections** and **WithProxyUrl**.
