:original_name: obs_25_0310.html

.. _obs_25_0310:

Setting or Obtaining a Bucket Quota
===================================

Setting a Bucket Quota
----------------------

You can call **ObsClient.SetBucketQuota** to set the bucket quota. Sample code is as follows:

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
   // Set the bucket quota.
   try
   {
       SetBucketQuotaRequest request = new SetBucketQuotaRequest
       {
           BucketName = "bucketname",
           StorageQuota = 0L,
       };
       SetBucketQuotaResponse response = client.SetBucketQuota(request);
       Console.WriteLine("Set bucket quota response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   A bucket quota must be a non-negative integer expressed in bytes. The maximum value is 2\ :sup:`63` - 1.

Obtaining the Bucket Quota
--------------------------

You can call **ObsClient.GetBucketQuota** to obtain the bucket quota. Sample code is as follows:

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
   // Obtain the bucket quota.
   try
   {
       GetBucketQuotaRequest request = new GetBucketQuotaRequest
       {
           BucketName = "bucketname",
       };
       GetBucketQuotaResponse response = client.GetBucketQuota(request);
       Console.WriteLine("Get bucket quota response: {0}", response.StatusCode);
       Console.WriteLine("StorageQuota: {0}", response.StorageQuota);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
