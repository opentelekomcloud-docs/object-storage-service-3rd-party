:original_name: obs_25_0505.html

.. _obs_25_0505:

Obtaining Download Progress
===========================

You can call **GetObjectRequest.DownloadProgress** to register the **System.EventHandler** callback function to obtain download progress.

This example downloads **objectname** from **bucketname** and uses **System.EventHandler** to monitor the download progress.

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
   // Download an object.
   try
   {
       GetObjectRequest request = new GetObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
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
       using (GetObjectResponse response = client.GetObject(request))
       {
           string dest = "savepath";
           if (!File.Exists(dest))
           {
              // Write the data streams into the file.
               response.WriteResponseStreamToFile(dest);
           }
           Console.WriteLine("Get object response: {0}", response.StatusCode);
       }
    }
   catch (ObsException ex)
   {
      Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
      Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  You can obtain the download progress when downloading an object in streaming, partial, asynchronous, or resumable mode.
