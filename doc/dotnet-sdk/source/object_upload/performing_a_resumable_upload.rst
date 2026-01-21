:original_name: obs_25_0412.html

.. _obs_25_0412:

Performing a Resumable Upload
=============================

Uploading large files often fails due to poor network conditions or program breakdowns. It is a waste of resources to restart the upload process upon an upload failure, and the restarted upload process may still suffer from the unstable network. To resolve such issues, you can use the API for resumable upload, whose working principle is to divide the to-be-uploaded file into multiple parts and upload them separately. The upload result of each part is recorded in a checkpoint file in real time. Only when all parts are successfully uploaded, the result indicating a successful upload is returned. Otherwise, an exception is thrown to remind you of calling the API again for re-uploading. Based on the upload status of each part recorded in the checkpoint file, the re-uploading will upload the parts failed to be uploaded previously, instead of uploading all parts. By virtue of this, resources are saved and efficiency is improved.

You can call **ObsClient.UploadFile** to perform a resumable upload. The following table describes the parameters involved in this API.

+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| Parameter          | Description                                                                                                                                                                                                     | Property in OBS .NET SDK             |
+====================+=================================================================================================================================================================================================================+======================================+
| BucketName         | (Mandatory) Bucket name                                                                                                                                                                                         | UploadFileRequest.BucketName         |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| ObjectKey          | (Mandatory) Object name                                                                                                                                                                                         | UploadFileRequest.ObjectKey          |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| UploadFile         | (Mandatory) Path to the local file to be uploaded                                                                                                                                                               | UploadFileRequest.UploadFile         |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| UploadPartSize     | Part size, in bytes. The value ranges from 5 MB (default) to 5 GB.                                                                                                                                              | UploadFileRequest.UploadPartSize     |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| EnableCheckpoint   | Whether to enable the resumable upload mode. The default value is **false**, which indicates that this mode is disabled.                                                                                        | UploadFileRequest.EnableCheckpoint   |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| CheckpointFile     | File used to record the upload progress. This parameter is effective only in the resumable upload mode. If the value is null, the file is in the same directory as the local file to be uploaded.               | UploadFileRequest.CheckpointFile     |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| Metadata           | Customized metadata of the object                                                                                                                                                                               | UploadFileRequest.Metadata           |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| EnableCheckSum     | Whether to verify the content of the to-be-uploaded file. This parameter is effective only in the resumable upload mode. The default value is **false**, which indicates that the content will not be verified. | UploadFileRequest.EnableCheckSum     |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| TaskNum            | Maximum number of parts that can be concurrently uploaded. The default value is **1**.                                                                                                                          | UploadFileRequest.TaskNum            |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| UploadProgress     | Upload progress callback function                                                                                                                                                                               | UploadFileRequest.UploadProgress     |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| ProgressType       | Mode for representing the upload progress                                                                                                                                                                       | UploadFileRequest.ProgressType       |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| ProgressInterval   | Interval for refreshing the upload progress                                                                                                                                                                     | UploadFileRequest.ProgressInterval   |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
| UploadEventHandler | Upload event callback function                                                                                                                                                                                  | UploadFileRequest.UploadEventHandler |
+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+

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
   // Perform a resumable upload.
   try
   {
       UploadFileRequest request = new UploadFileRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           // Specify the local file to be uploaded.
           UploadFile = "localpath",
           // Set the part size to 10 MB.
           UploadPartSize = 10 * 1024 * 1024,
           // Enable the resumable download mode.
           EnableCheckpoint = true,
       };
       // Represent the progress by showing how many bytes have been uploaded.
       request.ProgressType = ProgressTypeEnum.ByBytes;
       // Refresh the upload progress each time 1 MB data is uploaded.
       request.ProgressInterval = 1024 * 1024;

       // Register the upload progress callback function.
       request.UploadProgress += delegate(object sender, TransferStatus status){
           // Obtain the average upload rate.
           Console.WriteLine("AverageSpeed: {0}", status.AverageSpeed / 1024  + "KB/S");
           // Obtain the upload progress in percentage.
           Console.WriteLine("TransferPercentage: {0}", status.TransferPercentage);
       };

       // Register the upload event callback function.
       request.UploadEventHandler += delegate(object sender, ResumableUploadEvent e){
           // Obtain the upload events.
           Console.WriteLine("EventType: {0}", e.EventType);
       };

       CompleteMultipartUploadResponse response = client.UploadFile(request);
       Console.WriteLine("Upload File response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
      Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
      Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  The API for resumable upload, which is implemented based on :ref:`multipart upload <obs_25_0408>`, is an encapsulated and enhanced version of multipart upload.
   -  This API saves resources and improves efficiency upon the re-upload, and speeds up the upload process by concurrently uploading parts. Because this API is transparent to users, users are free from concerns about internal service details, such as the creation and deletion of checkpoint files, division of objects, and concurrent upload of parts.

   -  The default value of the **EnableCheckpoint** parameter is **false**, which indicates that the resumable upload mode is disabled. In such cases, the API for resumable upload degrades to the simple encapsulation of multipart upload, and no checkpoint file will be generated.
   -  The **CheckpointFile** and **EnableCheckSum** parameters are valid only when **EnableCheckpoint** is **true**.
