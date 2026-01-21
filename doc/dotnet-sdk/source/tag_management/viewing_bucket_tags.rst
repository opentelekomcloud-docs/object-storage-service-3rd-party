:original_name: obs_25_1303.html

.. _obs_25_1303:

Viewing Bucket Tags
===================

You can call **ObsClient.GetBucketTagging** to view bucket tags. The following code shows how to view bucket tags.

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
   // Obtain bucket tags.
   try
   {
       GetBucketTaggingRequest request = new GetBucketTaggingRequest
       {
           BucketName = "bucketname",
       };
       GetBucketTaggingResponse response = client.GetBucketTagging(request);
       foreach (Tag tag in response.Tags)
       {
           Console.WriteLine("Get bucket Tagging response Key: {0}" + tag.Key);
           Console.WriteLine("Get bucket Tagging response Value:{0} " + tag.Value);
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
