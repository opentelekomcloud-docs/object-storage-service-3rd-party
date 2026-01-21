:original_name: obs_25_0805.html

.. _obs_25_0805:

Copying a Versioning Object
===========================

You can call **ObsClient.CopyObject** to copy an object version by specifying the version ID (**SourceVersionId**).

This example specifies **SourceVersionId** to copy **sourceobjectname** from **sourcebucketname** to **destbucketname** as **destobjectname**.

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
   // Copy a versioning object.
   try
   {
       CopyObjectRequest request = new CopyObjectRequest();
       request.SourceBucketName = "sourcebucketname";
       request.SourceObjectKey = "sourceobjectname";
       request.BucketName = "destbucketname";
       request.ObjectKey = "destobjectName";
       request.SourceVersionId = "sourceversionId";
       CopyObjectResponse response = client.CopyObject(request);
       Console.WriteLine("copy object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  To handle the error codes possibly returned during the operation, see :ref:`OBS Server-Side Error Codes <obs_25_1601>`.
