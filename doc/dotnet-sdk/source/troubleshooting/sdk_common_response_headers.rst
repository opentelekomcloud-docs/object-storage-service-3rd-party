:original_name: obs_25_1605.html

.. _obs_25_1605:

SDK Common Response Headers
===========================

After you call an API in an instance of ObsClient, a sub-class of ObsWebServiceResponse will be returned.

It includes HTTP/HTTPS response headers.

This example obtains **request-id** from the common response headers when creating a bucket.

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
   // Create a bucket.
   try
   {
       CreateBucketRequest request = new CreateBucketRequest()
       {
           BucketName = "bucketname",
       };
       ObsWebServiceResponse response = client.CreateBucket(request);
       // Obtain the request ID from the common response headers.
       Console.WriteLine("RequestId: {0}", response.RequestId);
       foreach(KeyValuePair<string,string> entry in res.Headers)
       {
           Console.WriteLine("{0}:{1}", entry.Key, entry.Value);
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
