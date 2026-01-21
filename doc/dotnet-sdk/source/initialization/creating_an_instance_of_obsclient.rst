:original_name: obs_25_0202.html

.. _obs_25_0202:

Creating an Instance of ObsClient
=================================

**ObsClient** functions as the .NET client for accessing OBS. It offers callers a series of APIs for interaction with OBS and is used for managing and operating resources, such as buckets and objects, stored in OBS. To use OBS .NET SDK to send a request to OBS, you need to initialize an instance of **ObsClient** and modify the default configurations in **ObsConfig** based on needs.

-  If you use the endpoint to create an instance of **ObsClient**, all parameters are in their default values and cannot be modified.

   -  Using permanent AK (access key ID)/SK(secret access key)

   .. code-block::

      // Initialize configuration parameters.
      // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
      // Obtain an AK/SK pair on the management console.
      string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
      string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
      // Create an instance of ObsClient.
      ObsClient client = new ObsClient(accessKey, secretKey, "https://your-endpoint");
      // Use the instance to access OBS.

   -  Using temporary access credentials (AKs/SKs and security tokens)

   .. code-block::

      // Initialize configuration parameters.
      // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
      // Obtain an AK/SK pair on the management console.
      string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
      string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
      string securityToken= "your_securityToken"
      // Create an instance of ObsClient.
      ObsClient client = new ObsClient(accessKey, secretKey,securityToken, "https://your-endpoint");
      // Use the instance to access OBS.

-  If you use the **ObsConfig** configuration class to create an instance of **ObsClient**, you can set any parameters as needed during the creation. After the instance has been created, the parameters cannot be modified. For parameter details, see :ref:`Configuring an Instance of ObsClient <obs_25_0203>`

.. code-block::

   // Create an instance of ObsConfig.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an instance of ObsClient.
   ObsClient client = new ObsClient(accessKey, secretKey, config);
   // Use the instance to access OBS.

.. note::

   -  The project can contain one or more instances of **ObsClient**.

   -  **ObsClient** is thread-safe and can be simultaneously used by multiple threads.
