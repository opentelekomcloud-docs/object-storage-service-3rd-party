:original_name: obs_25_0304.html

.. _obs_25_0304:

Identifying Whether a Bucket Exists
===================================

You can call **ObsClient.HeadBucket** to identify whether a bucket exists.

This example checks whether bucket **bucketname** exists.

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
   ObsClient client = new ObsClient(accessKey, secretKey, config
   // Identify whether a bucket exists.
   try
   {
       HeadBucketRequest request = new HeadBucketRequest
       {
           BucketName = "bucketname",
       };
       bool exists = client.HeadBucket(request);
       Console.WriteLine("Bucket exists: {0}", exists);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("StatusCode: {0}", ex.StatusCode);
   }

.. note::

   If an exception is thrown and the returned HTTP status code is **404**, the bucket does not exist.
