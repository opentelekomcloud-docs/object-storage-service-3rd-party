:original_name: obs_25_1103.html

.. _obs_25_1103:

Viewing Bucket Logging
======================

You can call **ObsClient.GetBucketLogging** to view the logging configuration of a bucket.

This example views the logging configuration of bucket **bucketname**.

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
   // View bucket logging.
   try
   {
       GetBucketLoggingRequest request = new GetBucketLoggingRequest
       {
           BucketName = "bucketname",
       };
       GetBucketLoggingResponse response = client.GetBucketLogging(request);
       Console.WriteLine("TargetBucketName is : " + response.Configuration.TargetBucketName);
       Console.WriteLine("TargetPrefix is : " + response.Configuration.TargetPrefix);
       Console.WriteLine("Get bucket logging response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  To handle the error codes possibly returned during the operation, see :ref:`OBS Server-Side Error Codes <obs_25_1601>`.
