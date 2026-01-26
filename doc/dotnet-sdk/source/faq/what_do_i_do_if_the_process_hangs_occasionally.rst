:original_name: en-us_topic_0000001831623237.html

.. _en-us_topic_0000001831623237:

What Do I Do If the Process Hangs Occasionally?
===============================================

**Symptom**: The process occasionally hangs when you invoke .NET SDK methods.

**Solution:** Add "using" before the method.

See the example below.

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
       // Specify an object (example/objectname is an example here).
       request.ObjectKey = "example/objectname";
       // Obtain the object metadata.
       using (GetObjectMetadataResponse response = client.GetObjectMetadata(request)) {
          Console.WriteLine("Get object metadata response: {0}", response.StatusCode);
          // Obtain the ETag of the object.
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
