:original_name: obs_25_0113.html

.. _obs_25_0113:

General Examples of ObsClient
=============================

When you call an API using an instance of **ObsClient**, if no exception is thrown, the return value is valid, and a sub-class instance of :ref:`ObsWebServiceResponse <obs_25_1605>` (SDK common response headers) is returned. If any exception is thrown, the operation failed, and you can obtain the exception details from the returned instance of :ref:`ObsException <obs_25_1606>`. **ObsClient** supports synchronous and asynchronous API callings. Examples are as follows:

Synchronous Call
----------------

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

   // Call the API for creating a bucket in synchronous mode.
   try
   {
       CreateBucketRequest request = new CreateBucketRequest
       {
           BucketName = "bucketname",
       };
       CreateBucketResponse response = client.CreateBucket(request);

       Console.WriteLine("Create bucket response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Asynchronous Call
-----------------

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

   // Call the API for creating a bucket in asynchronous mode.
   CreateBucketRequest request = new CreateBucketRequest
   {
       BucketName = "bucketname",
   };
   client.BeginCreateBucket(request, delegate(IAsyncResult ar){
      try
      {
           CreateBucketResponse response = client.EndCreateBucket(ar);
           Console.WriteLine("Create bucket response: {0}", response.StatusCode);
       }
       catch (ObsException ex)
       {
           Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
           Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
       }
   }, null);
   Console.ReadKey();
