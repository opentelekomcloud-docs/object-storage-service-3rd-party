:original_name: obs_25_0403.html

.. _obs_25_0403:

Performing a File-Based Upload
==============================

File-based upload uses local files as the data source of objects.

This example uploads local file **localfile** to bucket **bucketname** as object **objectname**.

The example code is as follows:

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an ObsClient instance.
   ObsClient client = new ObsClient(accessKey, secretKey, config);
   // Upload a file.
   try
   {
       PutObjectRequest request = new PutObjectRequest()
       {
           BucketName = "bucketname",  //Name of the bucket for storing the file to be uploaded
           ObjectKey = "objectname",   //Name of the file to be uploaded (The file name is the complete path of the file in the bucket, for example, folder/test.txt. The path does not contain the bucket name.)
           FilePath = "localfile",//Path of the local file to be uploaded, in which the file name must be specified
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

   -  The content to be uploaded cannot exceed 5 GB.
