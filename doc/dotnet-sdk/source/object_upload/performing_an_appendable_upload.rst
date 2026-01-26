:original_name: obs_25_0410.html

.. _obs_25_0410:

Performing an Appendable Upload
===============================

Appendable upload allows you to upload an object in appendable mode and then append data to the object. You can call **ObsClient.AppendObject** to perform an appendable upload. Sample code is as follows:

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
   try
   {
       // Upload an object in appendable mode.
       AppendObjectRequest request = new AppendObjectRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectkey";
       request.InputStream = new MemoryStream(Encoding.UTF8.GetBytes("Hello OBS"));

       AppendObjectResponse response = client.AppendObject(request);

       // Append data to the object.
       request.Position = response.NextPosition;
       request.InputStream = new MemoryStream(Encoding.UTF8.GetBytes("Hello OBS Again"));
       response = client.AppendObject(request);
       Console.WriteLine("NextPosition:{0}", response.NextPosition);
       Console.WriteLine("ETag:{0}", response.ETag);

       // Use the API for obtaining object properties to get the start position for next appending.
       GetObjectMetadataResponse metadataResponse = client.GetObjectMetadata("bucketname", "objectkey");
       Console.WriteLine("NextPosition from metadata:{0}", metadataResponse.NextPosition);

   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  Objects uploaded using **ObsClient.PutObject**, referred to as normal objects, can overwrite objects uploaded using **ObsClient.AppendObject**, referred to as appendable objects. Data cannot be appended to an appendable object once the object has been overwritten by a normal object.
   -  When you upload an object for the first time in append mode, an exception will be reported (HTTP status code **409**) if an object of the same name exists.
   -  The ETag returned for each append upload is the ETag for the uploaded content, rather than that of the whole object.
   -  Data appended each time can be up to 5 GB, and 10000 times of appendable uploads can be performed on a single object.
   -  After an appendable upload is successful, you can use **AppendObjectResponse.NextPosition** or call **ObsClient.GetObjectMetadata** to get the start position for next appending.
