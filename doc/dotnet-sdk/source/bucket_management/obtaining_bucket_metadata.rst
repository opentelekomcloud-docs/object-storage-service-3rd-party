:original_name: obs_25_0305.html

.. _obs_25_0305:

Obtaining Bucket Metadata
=========================

You can call **ObsClient.GetBucketMetadata** to obtain the metadata of a bucket.

This example returns the metadata of bucket **bucketname**.

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
   // Obtain the bucket metadata.
   try
   {
       List<string> headers = new List<string>();
       headers.Add("x-obs-header");
       GetBucketMetadataRequest request = new GetBucketMetadataRequest
       {
           BucketName = "bucketname",
           Origin = "http://www.a.com",
           AccessControlRequestHeaders = headers,
       };
       GetBucketMetadataResponse response = client.GetBucketMetadata(request);
       Console.WriteLine("StorageClass: {0}", response.StorageClass);
       Console.WriteLine("Location: {0}", response.Location);
   }
   catch (ObsException ex)
   {
     Console.WriteLine("StatusCode: {0}", ex.StatusCode);
   }

.. note::

   -  To handle the error codes possibly returned during the operation, see :ref:`OBS Server-Side Error Codes <obs_25_1601>`.
