:original_name: obs_25_0409.html

.. _obs_25_0409:

Configuring Lifecycle Management
================================

When uploading an object or initializing a multipart upload, you can directly set the expiration time for the object. Sample code is as follows:

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
       PutObjectRequest request = new PutObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           FilePath = "localfile",// Path of the local file uploaded. The file name must be specified.
           Expires = 30 // When uploading an object, set the object to expire after 30 days.
       };
       PutObjectResponse response = client.PutObject(request);
       Console.WriteLine("put object response: {0}", response.StatusCode);

       InitiateMultipartUploadRequest initiateRequest = new InitiateMultipartUploadRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           // When initializing a multipart upload, set the object to expire 60 days after combination.
           Expires = 60
       };

       InitiateMultipartUploadResponse initResponse = client.InitiateMultipartUpload(initiateRequest);
       Console.WriteLine("InitiateMultipartUpload status: {0}", initResponse.StatusCode);
       Console.WriteLine("InitiateMultipartUpload UploadId: {0}", initResponse.UploadId);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  The previous mode specifies the time duration in days after which an object will expire. The OBS server automatically clears expired objects.
   -  The object expiration time set in the preceding method takes precedence over the bucket lifecycle rule.
