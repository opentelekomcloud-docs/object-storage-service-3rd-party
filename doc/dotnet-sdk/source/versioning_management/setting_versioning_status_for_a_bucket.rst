:original_name: obs_25_0802.html

.. _obs_25_0802:

Setting Versioning Status for a Bucket
======================================

You can call **ObsClient.SetBucketVersioning** to set the versioning status for a bucket. OBS supports two versioning statuses.

+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| Versioning Status     | Description                                                                                                                                                                                                                       | Value in OBS .NET SDK       |
+=======================+===================================================================================================================================================================================================================================+=============================+
| Enabled               | #. OBS creates a unique version ID for each uploaded object. Namesake objects are not overwritten and are distinguished by their own version IDs.                                                                                 | VersionStatusEnum.Enabled   |
|                       | #. Objects can be downloaded by specifying the version ID. By default, the latest object is downloaded if no version ID is specified.                                                                                             |                             |
|                       | #. Objects can be deleted by specifying the version ID. If an object is deleted with no version ID specified, the object will generate a delete marker with a unique version ID but is not physically deleted.                    |                             |
|                       | #. Objects of the latest version in a bucket are returned by default after **ObsClient.ListObjects** is called. You can call **ObsClient.ListVersions** to list a bucket's objects with all version IDs.                          |                             |
|                       | #. Except for delete markers, storage space occupied by objects with all version IDs is billed.                                                                                                                                   |                             |
+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| Suspended             | #. Existing objects with version IDs are not affected.                                                                                                                                                                            | VersionStatusEnum.Suspended |
|                       | #. OBS creates version ID **null** to an uploaded object and the object will be overwritten after a namesake one is uploaded                                                                                                      |                             |
|                       | #. Objects can be downloaded by specifying the version ID. By default, the latest object is downloaded if no version ID is specified.                                                                                             |                             |
|                       | #. Objects can be deleted by version ID. If an object is deleted with no version ID specified, the object is only attached with a deletion mark and version ID **null**. Objects with version ID **null** are physically deleted. |                             |
|                       | #. Except for delete markers, storage space occupied by objects with all version IDs is billed.                                                                                                                                   |                             |
+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+

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
   // Set the versioning status.
   try
   {
       SetBucketVersioningRequest request = new SetBucketVersioningRequest();
       request.BucketName = "bucketname";
       request.Configuration = new VersioningConfiguration();
       //Enabling versioning.
       request.Configuration.Status = VersionStatusEnum.Enabled;
       SetBucketVersioningResponse response = client.SetBucketVersioning(request);
       Console.WriteLine("Set bucket version response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
