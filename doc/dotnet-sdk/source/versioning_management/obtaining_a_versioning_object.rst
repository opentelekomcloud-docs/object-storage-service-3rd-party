:original_name: obs_25_0804.html

.. _obs_25_0804:

Obtaining a Versioning Object
=============================

You can call **ObsClient.GetObject** to obtain an object version by specifying the version ID (**VersionId**).

This example downloads object **objectname** from bucket **bucketname** by specifying **VersionId**.

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
   // Obtain versioning objects.
   try
   {
       GetObjectRequest getObjectRequest = new GetObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           VersionId = "versionId",
       };
       using (GetObjectResponse response = client.GetObject(getObjectRequest))
       {
           Console.WriteLine("Get object response: {0}", response.StatusCode);
           //Save the file locally.
           if (!File.Exists("savePath"))
           {
               response.WriteResponseStreamToFile("savePath");
           }
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  If the version ID is null, the object of the latest version will be downloaded, by default.
