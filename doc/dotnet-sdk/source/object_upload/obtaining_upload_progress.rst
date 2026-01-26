:original_name: obs_25_0405.html

.. _obs_25_0405:

Obtaining Upload Progress
=========================

You can call **PutObjectRequest.UploadProgress** to register a **System.EventHandler** callback function to obtain upload progress.

This example uploads local file **localfile** to bucket **bucketname** as object **objectname** and uses **System.EventHandler** to monitor the upload progress.

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
   // Upload a file.
   try
   {
       PutObjectRequest request = new PutObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           FilePath = "localfile",// Path of the local file uploaded. The file name must be specified.
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
       PutObjectResponse response = client.PutObject(request);
       Console.WriteLine("put object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  You can query the upload progress when uploading an object in streaming, file-based, asynchronous, resumable, or appendable mode, or uploading a part.
