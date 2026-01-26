:original_name: obs_25_1503.html

.. _obs_25_1503:

Example of Encryption
=====================

Encrypting an Object to Be Uploaded
-----------------------------------

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
   // Generate an encryption key.
   System.Security.Cryptography.Aes aesEncryption = System.Security.Cryptography.Aes.Create();
   aesEncryption.KeySize = 256;
   aesEncryption.GenerateKey();
   string customerkey = Convert.ToBase64String(aesEncryption.Key);
   // Configure the local file to be encrypted before an upload based on the site requirements.
   string filePathKms = "D:\\test\\testSseC.zip";
   string filePathSseC = "D:\\test\\testSseC.zip";
   // Upload the object.
   try
   {
       // When uploading an object, use the SSE-KMS algorithm to encrypt the object.
       SseKmsHeader kms = new SseKmsHeader();
       kms.Algorithm = SseKmsAlgorithmEnum.Kms;
       PutObjectRequest request1 = new PutObjectRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname1",
           FilePath = filePathKms,
           SseHeader = kms,
       };
       client.PutObject(request1);
       // When uploading an object, use the SSE-C algorithm to encrypt the object.
       PutObjectRequest request2 = new PutObjectRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname2",
           FilePath = filePathSseC,
           SseHeader = new SseCHeader()
           {
               Algorithm = SseCAlgorithmEnum.Aes256,
               KeyBase64 = customerkey
           }
       };
       client.PutObject(request2);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Decrypting a To-Be-Download Object
----------------------------------

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
       // When downloading an object, use the SSE-C algorithm to decrypt it.
       GetObjectRequest request = new GetObjectRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname2",
           // The key used here must be the one used for uploading the object.
           SseCHeader = new SseCHeader()
           {
               Algorithm = SseCAlgorithmEnum.Aes256,
               KeyBase64 = "customerkey"
           }
       };
       client.GetObject(request);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
