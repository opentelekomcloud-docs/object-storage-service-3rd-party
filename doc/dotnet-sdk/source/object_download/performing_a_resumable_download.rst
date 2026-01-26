:original_name: obs_25_0510.html

.. _obs_25_0510:

Performing a Resumable Download
===============================

Downloading large files often fails due to poor network conditions or program breakdowns. It is a waste of resources to restart the download process upon a download failure, and the restarted download process may still suffer from the unstable network. To resolve such issues, you can use the API for resumable download, whose working principle is to divide the to-be-downloaded file into multiple parts and download them separately. The download result of each part is recorded in a checkpoint file in real time. Only when all parts are successfully downloaded, the result indicating a successful download is returned. Otherwise, an exception is thrown to remind you of calling the API again for re-downloading. Based on the download status of each part recorded in the checkpoint file, the re-downloading will download the parts failed to be downloaded previously, instead of downloading all parts. By virtue of this, resources are saved and efficiency is improved.

You can call **ObsClient.DownloadFile** to perform a resumable download. The following table describes the parameters involved in this API.

+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| Parameter            | Description                                                                                                                                                                                         | Property in OBS .NET SDK                 |
+======================+=====================================================================================================================================================================================================+==========================================+
| BucketName           | (Mandatory) Bucket name                                                                                                                                                                             | DownloadFileRequest.BucketName           |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| ObjectKey            | (Mandatory) Object name                                                                                                                                                                             | DownloadFileRequest.ObjectKey            |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| DownloadFile         | Full path of the local directory to which the object is downloaded. If the value is null, the downloaded object is saved in the directory where the program is executed.                            | DownloadFileRequest.DownloadFile         |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| DownloadPartSize     | Part size, in bytes. The value ranges from 5 MB (default) to 5 GB.                                                                                                                                  | DownloadFileRequest.DownloadPartSize     |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| EnableCheckpoint     | Whether to enable the resumable upload mode. The default value is **false**, which indicates that this mode is disabled.                                                                            | DownloadFileRequest.EnableCheckpoint     |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| CheckpointFile       | File used to record the download progress. This parameter is effective only in the resumable download mode. If the value is null, the file is in the same local directory as the downloaded object. | DownloadFileRequest.CheckpointFile       |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| VersionId            | Object version ID                                                                                                                                                                                   | DownloadFileRequest.VersionId            |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| TaskNum              | Maximum number of parts that can be concurrently downloaded. The default value is **1**.                                                                                                            | DownloadFileRequest.TaskNum              |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| DownloadProgress     | Download progress callback function                                                                                                                                                                 | DownloadFileRequest.DownloadProgress     |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| ProgressType         | Mode for representing the download progress                                                                                                                                                         | DownloadFileRequest.ProgressType         |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| ProgressInterval     | Interval for refreshing the download progress                                                                                                                                                       | DownloadFileRequest.ProgressInterval     |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
| DownloadEventHandler | Download event callback function                                                                                                                                                                    | DownloadFileRequest.DownloadEventHandler |
+----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+

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
   // Perform a resumable download.
   try
   {
       DownloadFileRequest request = new DownloadFileRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           // Specify the local file to be downloaded.
           DownloadFile = "savepath",
           // Set the part size to 10 MB.
           DownloadPartSize = 1024 * 1024 * 10,
           // Enable the resumable download mode.
           EnableCheckpoint = true,
       };

       // Represent the progress by showing how many bytes have been downloaded.
       request.ProgressType = ProgressTypeEnum.ByBytes;
       // Refresh the download progress each time 1 MB data is downloaded.
       request.ProgressInterval = 1024 * 1024;

       // Register the download progress callback function.
       request.DownloadProgress += delegate(object sender, TransferStatus status){
           // Obtain the average download rate.
           Console.WriteLine("AverageSpeed: {0}", status.AverageSpeed / 1024  + "KB/S");
           // Obtain the download progress in percentage.
           Console.WriteLine("TransferPercentage: {0}", status.TransferPercentage);
       };

       // Register the download event callback function.
       request.DownloadEventHandler += delegate(object sender, ResumableDownloadEvent e){
           // Obtain the download events.
           Console.WriteLine("EventType: {0}", e.EventType);
       };

       GetObjectMetadataResponse response = client.DownloadFile(request);
       Console.WriteLine("Download File response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
      Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
      Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  The API for resumable download, which is implemented based on :ref:`partial download <obs_25_0503>`, is an encapsulated and enhanced version of partial download.
   -  This API saves resources and improves efficiency upon the re-download, and speeds up the download process by concurrently downloading parts. Because this API is transparent to users, users are free from concerns about internal service details, such as the creation and deletion of checkpoint files, division of objects, and concurrent download of parts.

   -  The default value of the **EnableCheckpoint** parameter is **false**, which indicates that the resumable download mode is disabled. In such cases, the API for resumable download degrades to the simple encapsulation of partial download, and no checkpoint file will be generated.
   -  **CheckpointFile** is effective only when **EnableCheckpoint** is **true**.
