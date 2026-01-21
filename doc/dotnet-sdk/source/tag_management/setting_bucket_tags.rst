:original_name: obs_25_1302.html

.. _obs_25_1302:

Setting Bucket Tags
===================

You can call **ObsClient.SetBucketTagging** to set bucket tags. Sample code is as follows:

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
   // Set bucket tags.
   try
   {
       SetBucketTaggingRequest request = new SetBucketTaggingRequest();
       request.BucketName = "bucketname";
       Tag tag1 = new Tag();
       tag1.Key = "tag1";
       tag1.Value = "value1";
       Tag tag2 = new Tag();
       tag2.Key = "tag2";
       tag2.Value = "value2";
       request.Tags.Add(tag2);
       request.Tags.Add(tag1);
       SetBucketTaggingResponse response = client.SetBucketTagging(request);
       Console.WriteLine("Set bucket tag response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  A bucket can have up to 10 tags.
   -  The key and value pair of a tag can be composed of Unicode characters.
