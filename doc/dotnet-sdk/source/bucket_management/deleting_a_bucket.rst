:original_name: obs_25_0303.html

.. _obs_25_0303:

Deleting a Bucket
=================

You can call **ObsClient.DeleteBucket** to delete a bucket. Sample code is as follows:

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
   //Delete a bucket.
   try
   {
       DeleteBucketRequest request = new DeleteBucketRequest
       {
           BucketName = "bucketname",
       };
       DeleteBucketResponse response = client.DeleteBucket(request);
       Console.WriteLine("Delete bucket response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  Only empty buckets (without objects and part fragments) can be deleted.
   -  Bucket deletion is a non-idempotence operation and an error will be reported if the to-be-deleted bucket does not exist.
