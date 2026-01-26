:original_name: obs_25_0809.html

.. _obs_25_0809:

Deleting Versioning Objects
===========================

Deleting a Single Versioning Object
-----------------------------------

You can call **ObsClient.DeleteObject** to pass a version ID (**VersionId**) to delete an object version.

This example deletes object **objectname** from bucket **bucketname** by specifying **VersionId**.

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
   // Delete a versioning object.
   try
   {
       DeleteObjectRequest request = new DeleteObjectRequest()
       {
           BucketName = "buckername",
           ObjectKey = "objectname",
           VersionId = "versionId"
       };
       DeleteObjectResponse response = client.DeleteObject(request);
       Console.WriteLine("Delete object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Deleting Versioning Objects in a Batch
--------------------------------------

You can call **ObsClient.DeleteObjects** to batch delete specific versions of an object by passing the **VersionId** value of each version to delete.

This example deletes objects **objectname1** and **objectname2** from bucket **bucketname** in a batch by specifying their version IDs.

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
   // Delete two versioning objects.
   try
   {
       DeleteObjectsRequest request = new DeleteObjectsRequest();
       request.BucketName = "bucketname";
       request.Quiet = true;
       request.AddKey("objectName1", "versionId1");
       request.AddKey("objectName2", "versionId2");
       DeleteObjectsResponse response = client.DeleteObjects(request);
       Console.WriteLine("Delete objects response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
