:original_name: obs_25_0302.html

.. _obs_25_0302:

Listing Buckets
===============

You can call **ObsClient.ListBuckets** to list buckets. Sample code is as follows:

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
   // List buckets.
   try
   {
       ListBucketsRequest request = new ListBucketsRequest();
       ListBucketsResponse response = client.ListBuckets(request);
       request.IsQueryLocation = true;
       foreach (ObsBucket bucket in response.Buckets)
       {
           Console.WriteLine("Bucket name is : {0}", bucket.BucketName);
           Console.WriteLine("Bucket creationDate is : {0}", bucket.CreationDate);
           Console.WriteLine("Bucket location is : {0}", bucket.Location);
           Console.WriteLine("\n");
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  Obtained bucket names are listed in the lexicographical order.
   -  Set **ListBucketsRequest.IsQueryLocation** to **true** and then you can query the bucket location when listing buckets.
