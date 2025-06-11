:original_name: obs_22_1303.html

.. _obs_22_1303:

Server-Side Encryption (SDK for Python)
=======================================

Function
--------

This API configures server-side encryption for objects, so that they will be encrypted or decrypted when you upload them to or download them from a bucket.

The encryption and decryption happen on the server side.

There are different encryption methods for you to choose from. Available encryption methods include server-side encryption with KMS-managed keys (SSE-KMS) and server-side encryption with customer-provided keys (SSE-C). Both of the two methods use the AES-256 algorithm.

With SSE-KMS, OBS uses the keys provided by KMS for server-side encryption.

With SSE-C, OBS uses the keys and MD5 values provided by customers for server-side encryption.

When server-side encryption is used, the returned ETag value is not the object's MD5 value. OBS will verify the object's MD5 value as long as the upload request includes the **Content-MD5** header, no matter whether server-side encryption is used or not.

Restrictions
------------

-  To upload an object, you must be the bucket owner or have the required permission (**obs:object:PutObject** in IAM or **PutObject** in a bucket policy).

Method
------

.. code-block::

   ObsClient.putFile(bucketName, objectKey, file_path, metadata, headers, extensionHeaders)

Supported APIs
--------------

The following table lists APIs related to server-side encryption:

+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| Method in OBS SDK for Python      | Description                                                                                                                                      | Supported Encryption Method |
+===================================+==================================================================================================================================================+=============================+
| ObsClient.putContent              | Sets the encryption algorithm and key during object upload to enable server-side encryption.                                                     | SSE-KMS                     |
|                                   |                                                                                                                                                  |                             |
|                                   |                                                                                                                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.putFile                 | Sets the encryption algorithm and key during file upload to enable server-side encryption.                                                       | SSE-KMS                     |
|                                   |                                                                                                                                                  |                             |
|                                   |                                                                                                                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.getObject               | Sets the decryption algorithm and key during object download to decrypt the object.                                                              | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.copyObject              | #. Sets the decryption algorithm and key for decrypting the source object during object copy.                                                    | SSE-KMS                     |
|                                   | #. Sets the encryption algorithm and key during object copy to enable the encryption algorithm for the target object.                            |                             |
|                                   |                                                                                                                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.getObjectMetadata       | Sets the decryption algorithm and key when obtaining the object metadata to decrypt the object.                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.initiateMultipartUpload | Sets the encryption algorithm and key when initializing a multipart upload task to enable server-side encryption for the final object generated. | SSE-KMS                     |
|                                   |                                                                                                                                                  |                             |
|                                   |                                                                                                                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.uploadPart              | Sets the encryption algorithm and key during multipart upload to enable server-side encryption for parts.                                        | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.copyPart                | #. Sets the decryption algorithm and key for decrypting the source object during multipart copy.                                                 | SSE-C                       |
|                                   | #. Sets the encryption algorithm and key during part copy to enable the encryption for the target part.                                          |                             |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+

Responses
---------

.. table:: **Table 1** List of returned results

   +---------------------------------------------------+-----------------------------------+
   | Type                                              | Description                       |
   +===================================================+===================================+
   | :ref:`GetResult <obs_22_1303__table133284282414>` | **Explanation:**                  |
   |                                                   |                                   |
   |                                                   | SDK common results                |
   +---------------------------------------------------+-----------------------------------+

.. _obs_22_1303__table133284282414:

.. table:: **Table 2** GetResult

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                                                        |
   +=======================+=======================+====================================================================================================================================================================================================================================================================================================================================+
   | status                | int                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | HTTP status code                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Value range**:                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | A status code is a group of digits ranging from 2\ *xx* (indicating successes) to 4\ *xx* or 5\ *xx* (indicating errors). It indicates the status of a response.                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | reason                | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Reason description.                                                                                                                                                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | errorCode             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Error code returned by the OBS server. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | errorMessage          | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Error message returned by the OBS server. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | requestId             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Request ID returned by the OBS server                                                                                                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | indicator             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Error indicator returned by the OBS server.                                                                                                                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hostId                | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Requested server ID. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource              | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Error source (a bucket or an object). If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | header                | list                  | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Response header list, composed of tuples. Each tuple consists of two elements, respectively corresponding to the key and value of a response header.                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | body                  | object                | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Result content returned after the operation is successful. If the value of **status** is larger than **300**, the value of **body** is null. The value varies with the API being called. For details, see :ref:`Bucket-Related APIs (SDK for Python) <obs_22_0800>` and :ref:`Object-Related APIs (SDK for Python) <obs_22_0900>`. |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example uploads and downloads an encrypted file using SSE-KMS.

::

   from obs import ObsClient
   from obs import PutObjectHeader, GetObjectHeader
   from obs import SseKmsHeader
   import os
   import traceback

   # Obtain an AK and SK pair using environment variables or import the AK and SK pair in other ways. Using hard coding may result in leakage.
   # Obtain an AK and SK pair on the management console.
   ak = os.getenv("AccessKeyID")
   sk = os.getenv("SecretAccessKey")
   # (Optional) If you use a temporary AK and SK pair and a security token to access OBS, obtain them from environment variables.
   # security_token = os.getenv("SecurityToken")
   # Set server to the endpoint of the region where the bucket is located.
   server = "https://your-endpoint"

   # Create an obsClient instance.
   # If you use a temporary AK and SK pair and a security token to access OBS, you must specify security_token when creating an instance.
   obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)
   try:
       put_headers = PutObjectHeader()
       # Specify the SSE-KMS encryption header for the object upload request.
       put_headers.sseHeader = SseKmsHeader.getInstance()

       bucketName = "examplebucket"
       # Specify an object name (the name displayed after the file is uploaded to the bucket).
       objectKey = "objectname"
       # Specify the full path of the file or folder to be uploaded, for example, aa/bb.txt or aa/.
       file_path = 'localfile'
       # Upload the object.
       resp = obsClient.putFile(bucketName, objectKey, file_path, headers=put_headers)


       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Put File Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Put File Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)

   # ---------------------------------------------------------------------------------------------------------------------

       get_headers = GetObjectHeader()
       # Specify the SSE-KMS decryption header for the object download request.
       get_headers.sseHeader = SseKmsHeader.getInstance()

       bucketName = "examplebucket"
       objectKey = "objectname"
       # Specify the full path (localfile as an example) to which objects are downloaded. The full path contains the local file name.
       downloadPath = 'localfile'
       # Download the object.
       resp2 = obsClient.getObject(bucketName, objectKey, downloadPath, headers=get_headers)

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp2.status < 300:
           print('Get Object Succeeded')
           print('requestId:', resp2.requestId)
       else:
           print('Get Object Failed')
           print('requestId:', resp2.requestId)
           print('errorCode:', resp2.errorCode)
           print('errorMessage:', resp2.errorMessage)
   except:
       print(traceback.format_exc())

This example uploads and downloads an encrypted file using SSE-C.

::

   from obs import ObsClient
   from obs import PutObjectHeader, GetObjectHeader
   from obs import SseCHeader
   import os
   import traceback

   # Obtain an AK and SK pair using environment variables or import the AK and SK pair in other ways. Using hard coding may result in leakage.
   # Obtain an AK and SK pair on the management console.
   ak = os.getenv("AccessKeyID")
   sk = os.getenv("SecretAccessKey")
   # (Optional) If you use a temporary AK and SK pair and a security token to access OBS, obtain them from environment variables.
   # security_token = os.getenv("SecurityToken")
   # Set server to the endpoint of the region where the bucket is located.
   server = "https://your-endpoint"

   # Create an obsClient instance.
   # If you use a temporary AK and SK pair and a security token to access OBS, you must specify security_token when creating an instance.
   obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)
   try:
       put_headers = PutObjectHeader()
       # Specify the SSE-C encryption header for the object upload request. encryption indicates the encryption method and key indicates the SSE-C key generated by the AES 256 algorithm.
       put_headers.sseHeader = SseCHeader(encryption='AES256', key='your sse-c key generated by AES-256 algorithm')

       bucketName = "examplebucket"
       # Specify an object name (the name displayed after the file is uploaded to the bucket).
       objectKey = "objectname"
       # Specify the full path of the file or folder to be uploaded, for example, aa/bb.txt or aa/.
       file_path = 'localfile'
       # Upload the object.
       resp = obsClient.putFile(bucketName, objectKey, file_path, headers=put_headers)

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Put File Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Put File Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)

   # ---------------------------------------------------------------------------------------------------------------------

       get_headers = GetObjectHeader()
       # Specify the SSE-C decryption header for an object download request. The key used here must be the one used for uploading the object.
       get_headers.sseHeader = SseCHeader(encryption='AES256', key='your sse-c key generated by AES-256 algorithm')

       bucketName = "examplebucket"
       objectKey = "objectname"
       # Specify the full path (localfile as an example) to which objects are downloaded. The full path contains the local file name.
       downloadPath = 'localfile'
       # Download the object.
       resp2 = obsClient.getObject(bucketName, objectKey, downloadPath, headers=get_headers)

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp2.status < 300:
           print('Get Object Succeeded')
           print('requestId:', resp2.requestId)
       else:
           print('Get Object Failed')
           print('requestId:', resp2.requestId)
           print('errorCode:', resp2.errorCode)
           print('errorMessage:', resp2.errorMessage)
   except:
       print(traceback.format_exc())
