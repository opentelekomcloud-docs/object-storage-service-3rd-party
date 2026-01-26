:original_name: obs_25_0508.html

.. _obs_25_0508:

Obtaining Custom Metadata
=========================

After an object is successfully downloaded, its custom data is returned.

This example obtains the custom metadata of **objectname** in **bucketname**.

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
       using (GetObjectResponse response = client.GetObject(request))
       {
           //Obtain the custom metadata of the object.
           foreach (string key in response.Metadata.Keys)
           {
               Console.WriteLine("key is :" + key + " value is: " + response.Metadata[key]);
           }
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
