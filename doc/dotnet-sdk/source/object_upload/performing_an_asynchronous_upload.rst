:original_name: obs_25_0404.html

.. _obs_25_0404:

Performing an Asynchronous Upload
=================================

You can call **ObsClient.BeginPutObject** and **ObsClient.EndPutObject** to upload an object asynchronously.

This example asynchronously uploads local file **localfile** to bucket **bucketname** as object **objectname**.

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
   // Upload a file in asynchronous mode.
   try
   {
       PutObjectRequest request = new PutObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           FilePath = "localfile",// Path of the local file to be uploaded. The file name must be specified.
       };
       client.BeginPutObject(request, delegate(IAsyncResult ar){
           try
           {
               PutObjectResponse response = client.EndPutObject(ar);
               Console.WriteLine("put object response: {0}", response.StatusCode);
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

   -  For more information, see :ref:`Object Upload Overview <obs_25_0401>`.
