:original_name: obs_25_0504.html

.. _obs_25_0504:

Performing an Asynchronous Download
===================================

You can call **ObsClient.BeginGetObject** and **ObsClient.EndGetObject** to download an object asynchronously.

This example downloads object **objectname** from bucket **bucketname** asynchronously.

Sample code is as follows:

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
   // Download an object in asynchronous mode.
   try
   {
       GetObjectRequest request = new GetObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
       };
       client.BeginGetObject(request, delegate(IAsyncResult ar){
           try
           {
               using (GetObjectResponse response = client.EndGetObject(ar))
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
       }, null);

   }
   catch (ObsException ex)
   {
      Console.WriteLine("Message: {0}", ex.Message);
   }

.. note::

   -  For more information, see :ref:`Performing a Streaming Download <obs_25_0502>`.
