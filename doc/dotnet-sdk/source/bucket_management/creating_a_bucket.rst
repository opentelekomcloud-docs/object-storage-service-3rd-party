:original_name: obs_25_0301.html

.. _obs_25_0301:

Creating a Bucket
=================

You can call **ObsClient.CreateBucket** to create a bucket.

Creating a Bucket with Parameters Specified
-------------------------------------------

When creating a bucket, you can specify the ACL, storage class, and location for the bucket. OBS provides three storage classes for buckets. For details, see :ref:`Setting or Obtaining the Storage Class of a Bucket <obs_25_0311>`. Sample code is as follows:

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
   // Create a bucket.
   try
   {
       CreateBucketRequest request = new CreateBucketRequest
       {
           BucketName = "bucketname",
           // Set the bucket location.
           Location = "bucketLocation",
   // Set the storage class to Cold.
           StorageClass = StorageClassEnum.Cold,
           // Set the ACL for the bucket to public read (the default state is private).
           CannedAcl = CannedAclEnum.Private
       };
       CreateBucketResponse response = client.CreateBucket(request);
       Console.WriteLine("Create bucket response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  Bucket names are globally unique. Ensure that the bucket you create is named differently from any other bucket.
   -  A bucket name must comply with the following rules:

      -  Contains 3 to 63 characters, chosen from lowercase letters, digits, hyphens (-), and periods (.), and starts with a digit or letter.
      -  Cannot be an IP address or similar.
      -  Cannot start or end with a hyphen (-) or period (.)
      -  Cannot contain two consecutive periods (.), for example, **my..bucket**.
      -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.

   -  If you create buckets of the same name in a region, no error will be reported and the bucket properties comply with those set in the first creation request.
   -  The bucket created in the previous example is of the default :ref:`ACL <obs_25_0306>` (**private**), in the OBS Standard storage class, and in the default region.

Creating a Bucket Directly
--------------------------

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
   // Create a bucket.
   try
   {
       CreateBucketRequest request = new CreateBucketRequest
       {
           BucketName = "bucketname",
       };
       CreateBucketResponse response = client.CreateBucket(request);
       Console.WriteLine("Create bucket response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
