:original_name: obs_25_0311.html

.. _obs_25_0311:

Setting or Obtaining the Storage Class of a Bucket
==================================================

OBS allows you to set storage classes for buckets. The storage class of an object defaults to be that of its residing bucket. Different storage classes meet different needs for storage performance and costs. There are three types of storage class for buckets, as described in the following table:

+---------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| Storage Class       | Description                                                                                                                                                                                                                           | Value in OBS .NET SDK               |
+=====================+=======================================================================================================================================================================================================================================+=====================================+
| OBS Standard        | Features low access latency and high throughput and is applicable to storing frequently-accessed (multiple times per month) hotspot or small objects (< 1 MB) requiring quick response.                                               | StorageClassEnum.Standard           |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| OBS Warm            | Is applicable to storing semi-frequently accessed (less than 12 times a year) data requiring quick response.                                                                                                                          | StorageClassEnum.Warm               |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| OBS Cold            | Is applicable to archiving rarely-accessed (once a year) data.                                                                                                                                                                        | StorageClassEnum.Cold               |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| Intelligent Tiering | Is designed to optimize storage costs by automatically moving data to a more economical access tier when data access patterns change. This storage class is ideal for data with constantly changing or unpredictable access patterns. | StorageClassEnum.INTELLIGENTTIERING |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+

For more information, see `Bucket Storage Classes <https://docs.otc.t-systems.com/en-us/usermanual/obs/en-us_topic_0050937852.html>`__.

Setting the Storage Class for a Bucket
--------------------------------------

You can call **ObsClient.SetBucketStoragePolicy** to set the storage class for a bucket. Sample code is as follows:

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
   // Set the storage class for a bucket.
   try
   {
       SetBucketStoragePolicyRequest request = new SetBucketStoragePolicyRequest
       {
           BucketName = "bucketname",
           StorageClass = StorageClassEnum.Cold,
       };
       SetBucketStoragePolicyResponse response = client.SetBucketStoragePolicy(request);
       Console.WriteLine("Set bucket storage policy response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Obtaining the Storage Class of a Bucket
---------------------------------------

You can call **ObsClient.GetBucketStoragePolicy** to obtain the storage class. Sample code is as follows:

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
   // Obtain the storage class of a bucket.
   try
   {
       GetBucketStoragePolicyRequest request = new GetBucketStoragePolicyRequest()
       {
           BucketName = "bucketName",
       };
       GetBucketStoragePolicyResponse response = client.GetBucketStoragePolicy(request);
       Console.WriteLine("Get bucket storage policy response: {0}", response.StatusCode);
       Console.WriteLine("StorageClass: {0}", response.StorageClass);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
