:original_name: obs_25_0407.html

.. _obs_25_0407:

Setting Object Properties
=========================

You can set properties for an object when uploading it. Object properties include the MIME type, MD5 value (for verification), storage class, and customized metadata. You can set properties for an object that is being uploaded in streaming, file-based, or multipart mode or when :ref:`copying the object <obs_25_0605>`.

The following table describes object properties.

+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| Property Name       | Description                                                                                                                                                                                                        | Default Value       |
+=====================+====================================================================================================================================================================================================================+=====================+
| Content-Type        | Indicates the MIME type of the object, which defines the type and network code of the object as well as in which mode and coding will the browser read the object.                                                 | binary/octet-stream |
+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| Content-MD5         | Indicates the base64-encoded digest of the object data. It is provided to the OBS server to verify data integrity.                                                                                                 | N/A                 |
+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| Storage class       | Indicates the storage class of the object. Different storage classes meet different needs for storage performance and costs. The value defaults to be the same as the object's residing bucket and can be changed. | N/A                 |
+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+
| Customized metadata | Indicates the user-defined description of the object. It is used to facilitate the customized management on the object.                                                                                            | N/A                 |
+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+

Setting the MIME Type for an Object
-----------------------------------

You can call **PutObjectRequest.ContentType** to set the MIME type for an object. Sample code is as follows:

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
   // Upload a file.
   try
   {
       PutObjectRequest request = new PutObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           FilePath = "localfile",//Path of the local file to upload. The path must contain the file name.
           ContentType = "image/jpeg",//MIME type of the object
       };
       PutObjectResponse response = client.PutObject(request);
       Console.WriteLine("put object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   If the MIME type is not specified, the SDK will automatically identify the MIME type according to the name suffix of the uploaded object. For example, if the name suffix of an object is **.xml** (**.html**), the object will be identified as an application/xml (text/html) file.

Setting the MD5 Value for an Object
-----------------------------------

You can call **PutObjectRequest.ContentMd5** to set the MD5 value for an object. Sample code is as follows:

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
   // Upload a file.
   try
   {
       PutObjectRequest request = new PutObjectRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           FilePath = "localfile",// Path of the local file uploaded. The file name must be specified.
           ContentMd5 = "your md5 which should be encoded by base64"
       };
       PutObjectResponse response = client.PutObject(request);
       Console.WriteLine("put object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  The MD5 value of an object must be a base64-encoded digest.
   -  The OBS server will compare this MD5 value with the MD5 value obtained by object data calculation. If the two values are not the same, the upload fails with HTTP status code **400** returned.
   -  If the MD5 value is not specified, the OBS server will skip MD5 value verification.

Setting the Storage Class for an Object
---------------------------------------

You can call **PutObjectRequest.StorageClass** to set the storage class for an object. Sample code is as follows:

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
   // Upload a file.
   try
   {
       PutObjectRequest request = new PutObjectRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           FilePath = "localfile",// Path of the local file uploaded. The file name must be specified.
           StorageClass = StorageClassEnum.Warm,//Object storage class
       };
       PutObjectResponse response = client.PutObject(request);
       Console.WriteLine("put object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  If you have not set the storage class for an object, the storage class of the object will be the same as that of its residing bucket.
   -  OBS provides objects with three storage classes which are consistent with :ref:`those <obs_25_0311>` provided for buckets.
   -  Before downloading a Cold object, you must restore it first.

Customizing Metadata for an Object
----------------------------------

You can call **PutObjectRequest.Metadata** to customize metadata for an object. Sample code is as follows:

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
   // Upload a file.
   try
   {
       PutObjectRequest request = new PutObjectRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           FilePath = "localfile",// Path of the local file uploaded. The file name must be specified.
       };
       request.Metadata.Add("meta1", "value1");
       PutObjectResponse response = client.PutObject(request);
       Console.WriteLine("put object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  An object can have multiple pieces of metadata. The total metadata size cannot exceed 8 KB.
   -  The customized object metadata can be obtained by using **ObsClient.GetObjectMetadata**. For details, see :ref:`Obtaining Object Properties <obs_25_0601>`.
   -  When you call **ObsClient.GetObject** to download an object, its customized metadata will also be downloaded.
