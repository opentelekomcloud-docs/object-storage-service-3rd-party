:original_name: obs_25_0309.html

.. _obs_25_0309:

Obtaining Storage Information About a Bucket
============================================

The storage information about a bucket includes the used capacity of and the number of objects in the bucket.

You can call **ObsClient.GetBucketStorageInfo** to obtain the bucket storage information.

This example returns the storage information of bucket **bucketname**.

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
   // Obtain the storage information about a bucket.
   try
   {
       GetBucketStorageInfoRequest request = new GetBucketStorageInfoRequest
       {
           BucketName = "bucketname",
       };
       GetBucketStorageInfoResponse response = client.GetBucketStorageInfo(request);
       Console.WriteLine("Get bucket storageinfo response: {0}", response.StatusCode);
       Console.WriteLine("ObjectNumber: {0}", response.ObjectNumber);
       Console.WriteLine("Size: {0}", response.Size);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  To handle the error codes possibly returned during the operation, see :ref:`OBS Server-Side Error Codes <obs_25_1601>`.
