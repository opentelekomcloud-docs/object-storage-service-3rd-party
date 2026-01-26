:original_name: obs_25_0503.html

.. _obs_25_0503:

Performing a Partial Download
=============================

When only partial data of an object is required, you can download data falling within a specific range.

If the specified range is from 0 to 1,000, data from byte 0 to byte 1,000, 1,001 bytes in total, are returned. If the specified range is invalid, the entire object will be returned.

This example downloads the content of **objectname** in **bucketname** from byte 10 to byte 200.

The sample code is as follows:

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
       ByteRange byteRange = new ByteRange(10, 200);
       GetObjectRequest request = new GetObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           ByteRange = byteRange,
       };
       using (GetObjectResponse response = client.GetObject(request))
       {
           string dest = "savepath";
           if (!File.Exists(dest))
           {
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
