:original_name: obs_25_0502.html

.. _obs_25_0502:

Performing a Streaming Download
===============================

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

   **GetObjectResponse.OutputStream** (**System.IO.Stream** type) is the response stream in **GetObjectResponse**. You can obtain the object content to a local file or memory via **GetObjectResponse.OutputStream**. Alternatively, you can call **GetObjectResponse.WriteResponseStreamToFile** provided by OBS .NET SDK to download the object content to a local file.

.. important::

   Object response streams obtained by **GetObjectResponse.OutputStream** must be closed explicitly using a **GetObjectResponse.OutputStream.Close()** call. Otherwise, resource leakage may occur.
