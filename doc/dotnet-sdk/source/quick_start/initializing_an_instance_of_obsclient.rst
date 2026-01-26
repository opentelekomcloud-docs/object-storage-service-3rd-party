:original_name: obs_25_0107.html

.. _obs_25_0107:

Initializing an Instance of ObsClient
=====================================

Each time you want to send an HTTP/HTTPS request to OBS, you must create an instance of **ObsClient**. Sample code is as follows:

.. code-block::

   // Initialize configuration parameters.
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

   For more information, see chapter "Initialization."

   For details about logging configuration, see :ref:`Configuring SDK Logging <obs_25_0204>`.
