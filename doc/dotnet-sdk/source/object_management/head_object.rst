:original_name: obs_25_0606.html

.. _obs_25_0606:

HEAD Object
===========

You can call **ObsClient.HeadObject** to check whether a specified object exists.

The example code is as follows:

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
   // Check whether the specified object exists.
   try
   {
       HeadObjectRequest request = new HeadObjectRequest()
       {
           BucketName = "bucketName",
           ObjectKey = "objectKey"
       };
       bool response = client.HeadObject(request);
       Console.WriteLine("Head object response: {0}", response);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("Exception errorcode: {0}, when head object.", ex.ErrorCode);
       Console.WriteLine("Exception errormessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  If an exception is thrown and the returned HTTP status code is **404**, the bucket does not exist.
