:original_name: obs_25_1102.html

.. _obs_25_1102:

Enabling Bucket Logging
=======================

You can call **ObsClient.SetBucketLogging** to enable bucket logging

.. important::

   The source bucket and target bucket of logging must be in the same region.

.. note::

   If the bucket is in the OBS Warm or Cold storage class, it cannot be used as the target bucket.


Enabling Bucket Logging
-----------------------

Sample code:

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
   try
   {
       // Set the source bucket logging.
       SetBucketLoggingRequest putrequest = new SetBucketLoggingRequest();
       putrequest.BucketName = "bucketname";
       putrequest.Configuration = new LoggingConfiguration();
       putrequest.Configuration.TargetBucketName = "targetbucketname";
       putrequest.Configuration.TargetPrefix = "access-log.";
       putrequest.Configuration.Agency= "your agency";
       SetBucketLoggingResponse putresponse = client.SetBucketLogging(putrequest);
       Console.WriteLine("Set bucket logging response: {0}", putresponse.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
