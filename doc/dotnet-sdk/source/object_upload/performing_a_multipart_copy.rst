:original_name: obs_25_0411.html

.. _obs_25_0411:

Performing a Multipart Copy
===========================

As a special case of multipart upload, multipart copy implements multipart upload by copying the whole or part of an object in a bucket. You can call **ObsClient.CopyPart** to copy parts.

This example copies object **sourceobjectname** from bucket **sourcebucketname** to bucket **destbucketname** as object **destobjectname**.

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
   ObsClient client = new ObsClient(accessKey, secretKey, config);
   // Copy parts.
   try
   {
       CopyPartRequest request = new CopyPartRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       request.UploadId = "uploadId";
       request.PartNumber = 1;
       request.SourceBucketName = "sourcebucketname";
       request.SourceObjectKey = "sourceobjectname";
       CopyPartResponse response = client.CopyPart(request);
       Console.WriteLine("Copy part response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
