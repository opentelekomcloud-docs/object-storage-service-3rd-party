:original_name: obs_25_0601.html

.. _obs_25_0601:

Obtaining Object Properties
===========================

You can call **ObsClient.GetObjectMetadata** to obtain object properties, including the last modification time, version ID, and customized metadata. Sample code is as follows:

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
       GetObjectMetadataRequest request = new GetObjectMetadataRequest();
       // Specify a bucket name.
       request.BucketName = "bucketname";
       // Specify an object (example/objectname as an example).
       request.ObjectKey = "example/objectname";
       // Obtain the object metadata.
       using (GetObjectMetadataResponse response = client.GetObjectMetadata(request)) {
          Console.WriteLine("Get object metadata response: {0}", response.StatusCode);
       // Obtain ETag of the object.
          Console.WriteLine("Object etag {0}:  ", response.ETag);
       // Obtain the object version ID.
          Console.WriteLine("Object versionId {0}:  ", response.VersionId);
       // Obtain the length of the object data, in bytes.
          Console.WriteLine("Object contentLength {0}:  ", response.ContentLength);
       }
   }
   catch (ObsException ex)
   {
      Console.WriteLine("Message: {0}", ex.Message);
   }

.. note::

   -  Due to HTTP coding restrictions, non-ASCII characters cannot be sent. The SDK will decode the information in response headers using URL decoding rules.
