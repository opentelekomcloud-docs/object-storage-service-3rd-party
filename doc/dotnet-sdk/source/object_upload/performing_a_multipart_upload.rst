:original_name: obs_25_0408.html

.. _obs_25_0408:

Performing a Multipart Upload
=============================

To upload a large file, multipart upload is recommended. Multipart upload is applicable to many scenarios, including:

-  Files to be uploaded are larger than 100 MB.
-  The network condition is poor. Connection to the OBS server is constantly down.
-  Sizes of files to be uploaded are uncertain.

Multipart upload consists of three phases:

#. Initialize a multipart upload (**ObsClient.InitiateMultipartUpload**).
#. Upload parts one by one or concurrently (**ObsClient.UploadPart**).
#. Combine parts (**ObsClient.CompleteMultipartUpload**) or abort the multipart upload (**ObsClient.AbortMultipartUpload**).

Initiating a Multipart Upload
-----------------------------

Before using a multipart upload, you need to first initiate it. This operation will return an upload ID (globally unique identifier) created by the OBS server to identify the multipart upload. You can use this upload ID to initiate related operations, such as aborting a multipart upload, listing multipart uploads, and listing uploaded parts.

You can call **ObsClient.InitiateMultipartUpload** to initiate a multipart upload.

.. note::

   -  Call **InitiateMultipartUploadRequest** to specify the name and owning bucket of the uploaded object.
   -  In **InitiateMultipartUploadRequest**, you can specify the MIME type, storage class, and customized metadata for the object.
   -  The upload ID of the multipart upload returned by **InitiateMultipartUploadResponse.UploadId** will be used in follow-up operations.

Uploading Parts
---------------

After initiating a multipart upload, you can specify the object name and upload ID to upload a part. Each upload part has a part number (ranging from **1** to **10000**). For parts with the same upload ID, their part numbers are unique and identify their relative location in the object. If you use the same part number to upload two parts, the latter one uploaded will overwrite the former one. Except for the last uploaded part whose size ranges from 0 to 5 GB, sizes of the other parts range from 100 KB to 5 GB. Parts can be uploaded in random order, or even through different processes or machines. OBS will combine them into the final object based on their part numbers.

You can call **ObsClient.UploadPart** to upload a part.

.. note::

   -  Except the part last uploaded, other parts must be larger than 100 KB. Part sizes will not be verified during upload because which one is last uploaded is not identified until parts are combined.
   -  OBS will return ETags (MD5 values) of the received parts to users.
   -  Part numbers range from 1 to 10000. If a part number exceeds this range, OBS will return error **400 Bad Request**.
   -  The minimum part size supported by an OBS 3.0 bucket is 100 KB, and the minimum part size supported by an OBS 2.0 bucket is 5 MB. You are advised to perform multipart upload to OBS 3.0 buckets.

Combining Parts
---------------

After all parts are uploaded, call the API for combining parts to generate the object. Before this operation, valid part numbers and ETags of all parts must be sent to OBS. After receiving this information, OBS verifies the validity of each part one by one. After all parts pass the verification, OBS combines these parts to form the final object.

You can call **ObsClient.CompleteMultipartUpload** to combine parts.

.. note::

   Part numbers can be inconsecutive.

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
   try
   {
       // 1. Initialize a multipart upload.
       InitiateMultipartUploadRequest initiateRequest = new InitiateMultipartUploadRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname"
       };

       InitiateMultipartUploadResponse initResponse = client.InitiateMultipartUpload(initiateRequest);
       Console.WriteLine("InitiateMultipartUpload status: {0}", initResponse.StatusCode);
       Console.WriteLine("InitiateMultipartUpload UploadId: {0}", initResponse.UploadId);

       // 2. Upload parts.
           string filePath = "localfile";// Path of the local file uploaded. The file name must be specified.
       long contentLength = new FileInfo(filePath).Length;
       long partSize = 15 * (long)Math.Pow(2, 20); // The part size is 15 MB.
       List<UploadPartResponse> uploadResponses = new List<UploadPartResponse>();
       long filePosition = 0;
       for (int i = 1; filePosition < contentLength; i++)
       {
           UploadPartRequest uploadRequest = new UploadPartRequest
           {
               BucketName = "bucketname",
               ObjectKey = "objectname",
               UploadId = initResponse.UploadId,
               PartNumber = i,
               PartSize = partSize,
               Offset = filePosition,
               FilePath = filePath
           };
           uploadResponses.Add(client.UploadPart(uploadRequest));
           Console.WriteLine("UploadPart count: {0}", uploadResponses.Count);
           filePosition += partSize;
       }

       // 3. Combine parts.

       CompleteMultipartUploadRequest completeRequest = new CompleteMultipartUploadRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           UploadId = initResponse.UploadId,
       };
       completeRequest.AddPartETags(uploadResponses);
       CompleteMultipartUploadResponse completeUploadResponse = client.CompleteMultipartUpload(completeRequest);
       Console.WriteLine("CompleteMultipartUpload status: {0}", completeUploadResponse.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("Exception:{0}", ex.ErrorCode);
       Console.WriteLine("Exception Message:{0}", ex.ErrorMessage);
   }

Aborting a Multipart Upload
---------------------------

After a multipart upload is aborted, you cannot use its upload ID to perform any operation and the uploaded parts will be deleted by OBS.

When an object is being uploaded in multi-part mode or an object fails to be uploaded, parts are generated in the bucket. These parts occupy your storage space. You can cancel the multi-part uploading task to delete unnecessary parts, thereby saving the storage space.

You can call **ObsClient.AbortMultipartUpload** to abort a multipart upload. Sample code is as follows:

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
   //Abort a multipart upload.
   try
   {
       AbortMultipartUploadRequest request = new AbortMultipartUploadRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           UploadId = "uploadId",//ID of the multipart upload to be aborted
       };
       AbortMultipartUploadResponse response = client.AbortMultipartUpload(request);
       Console.WriteLine("Abort multipart upload response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing Uploaded Parts
----------------------

You can call **ObsClient.ListParts** to list successfully uploaded parts of a multipart upload.

The following table describes the parameters involved in this API.

+------------------+------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
| Parameter        | Description                                                                                                                  | Property in OBS .NET SDK          |
+==================+==============================================================================================================================+===================================+
| BucketName       | Bucket name                                                                                                                  | ListPartsRequest.BucketName       |
+------------------+------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
| ObjectKey        | Object name                                                                                                                  | ListPartsRequest.ObjectKey        |
+------------------+------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
| UploadId         | Upload ID, which globally identifies a multipart upload. The value is in the returned result of **InitiateMultipartUpload**. | ListPartsRequest.UploadId         |
+------------------+------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
| MaxParts         | Maximum number of parts that can be listed per page.                                                                         | ListPartsRequest.MaxParts         |
+------------------+------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
| PartNumberMarker | Part number after which listing parts begins. Only parts whose part numbers are larger than this value will be listed.       | ListPartsRequest.PartNumberMarker |
+------------------+------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+

-  Listing parts in simple mode

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
   // Simple listing
   try
   {
       ListPartsRequest request = new ListPartsRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       request.UploadId = "uploadId";
       ListPartsResponse response = client.ListParts(request);
       Console.WriteLine("List parts response: {0}", response.StatusCode);
       foreach (PartDetail part in response.Parts)
       {
           Console.WriteLine("PartNumber: " + part.PartNumber);
           Console.WriteLine("Size: " + part.Size);
           Console.WriteLine("ETag: " + part.ETag);
           Console.WriteLine("LastModified: " + part.LastModified);
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   Information about a maximum of 1000 parts can be listed each time. If an upload of the specific upload ID contains more than 1000 parts and **ListPartsResult.isTruncated** is **true** in the returned result, not all parts are listed. In such cases, you can use **ListPartsRespon.NextPartNumberMarker** to obtain the start position for next listing.

-  Listing all parts

The following sample code lists more than 1,000 parts:

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
   // List all parts.
   try
   {
       ListPartsRequest request = new ListPartsRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       request.UploadId = "uploadId";
       ListPartsResponse response;
       do
       {
           response = client.ListParts(request);
           Console.WriteLine("List parts response: {0}", response.StatusCode);
           foreach (PartDetail part in response.Parts)
           {
               Console.WriteLine("PartNumber: " + part.PartNumber);
               Console.WriteLine("Size: " + part.Size);
               Console.WriteLine("ETag: " + part.ETag);
               Console.WriteLine("LastModified: " + part.LastModified);
           }
           request.PartNumberMarker = response.NextPartNumberMarker;
       }
       while (response.IsTruncated);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing Multipart Uploads
-------------------------

You can call **ObsClient.ListMultipartUploads** to list multipart uploads. The following table describes related parameters.

+----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+
| Parameter      | Description                                                                                                                                                                                                                                                                                                                                                                  | Property in OBS .NET SDK                   |
+================+==============================================================================================================================================================================================================================================================================================================================================================================+============================================+
| BucketName     | Bucket name                                                                                                                                                                                                                                                                                                                                                                  | ListMultipartUploadsRequest.BucketName     |
+----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+
| Prefix         | Prefix that the object names in the multipart uploads to be listed must contain                                                                                                                                                                                                                                                                                              | ListMultipartUploadsRequest.Prefix         |
+----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+
| Delimiter      | Character used to group object names involved in multipart uploads. If the object name contains the **Delimiter** parameter, the character string from the first character to the first delimiter in the object name is grouped under a single result element, **CommonPrefix**. (If a prefix is specified in the request, the prefix must be removed from the object name.) | ListMultipartUploadsRequest.Delimiter      |
+----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+
| MaxUploads     | Maximum number of multipart uploads listed in the response body. The value ranges from **1** to **1000**. If the value exceeds **1000**, only 1,000 multipart uploads are returned.                                                                                                                                                                                          | ListMultipartUploadsRequest.MaxUploads     |
+----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+
| KeyMarker      | Object name to start with when listing multipart uploads                                                                                                                                                                                                                                                                                                                     | ListMultipartUploadsRequest.KeyMarker      |
+----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+
| UploadIdMarker | Upload ID after which the multipart upload listing begins. It is effective only when used with **KeyMarker** so that multipart uploads after **UploadIdMarker** of **KeyMarker** will be listed.                                                                                                                                                                             | ListMultipartUploadsRequest.UploadIdMarker |
+----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+

-  Listing multipart uploads in simple mode

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
   //List multipart uploads in simple mode.
   try
   {
       ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest();
       listMultipartUploadsRequest.BucketName = "bucketname";
       ListMultipartUploadsResponse listMultipartUploadsResponse = client.ListMultipartUploads(listMultipartUploadsRequest);
       Console.WriteLine("ListMultipartUploadsResponse status code: " + listMultipartUploadsResponse.StatusCode);
       foreach (MultipartUpload upload in listMultipartUploadsResponse.MultipartUploads)
       {
           Console.WriteLine("ObjectKey {0}: " , upload.ObjectKey);
           Console.WriteLine("Initiated {0}: " , upload.Initiated);
           Console.WriteLine("\n");
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  Information about a maximum of 1000 multipart uploads can be listed each time. If a bucket contains more than 1000 multipart uploads and **ListMultipartUploadsResponse.isTruncated** is **true**, not all uploads are listed. In such cases, you can use **ListMultipartUploadsResponse.NextKeyMarker** and **ListMultipartUploadsResponse.NextUploadIdMarker** to obtain the start position for next listing.
   -  If you want to obtain all multipart uploads in a bucket, you can list them in paging mode.

-  Listing all multipart uploads in paging mode

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
   //List all multipart uploads.
   try
   {
       ListMultipartUploadsRequest request = new ListMultipartUploadsRequest();
       request.BucketName = "bucketname";
       ListMultipartUploadsResponse response;
       do
       {
           response = client.ListMultipartUploads(request);
           Console.WriteLine("ListMultipartUploadsResponse status code: " + response.StatusCode);
           foreach (MultipartUpload upload in response.MultipartUploads)
           {
               Console.WriteLine("ObjectKey {0}: " , upload.ObjectKey);
               Console.WriteLine("Initiated {0}: " , upload.Initiated);
               Console.WriteLine("\n");
           }
           request.KeyMarker = response.NextKeyMarker;
           request.UploadIdMarker = response.NextUploadIdMarker;
       }
       while (response.IsTruncated);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
