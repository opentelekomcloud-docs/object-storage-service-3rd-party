:original_name: obs_22_1001.html

.. _obs_22_1001:

Multipart Upload Overview
=========================

You can upload large files using multipart upload. Multipart upload is applicable to many scenarios, including:

-  Files to be uploaded are larger than 100 MB.
-  The network condition is poor. Connection to the OBS server is constantly down.
-  Sizes of files to be uploaded are uncertain.

A multipart upload consists of the following steps:

#. :ref:`Initiate a multipart upload <obs_22_1002>` (**ObsClient.initiateMultipartUpload**).
#. :ref:`Upload parts one by one or concurrently <obs_22_1003>` (**ObsClient.uploadPart**).
#. :ref:`Assemble parts <obs_22_1006>` (**ObsClient.completeMultipartUpload**) or :ref:`abort the multipart upload <obs_22_1008>` (**ObsClient.abortMultipartUpload**).

This example shows a complete multipart upload, including initiating a multipart upload, uploading parts, and assembling parts.

::

   # -*- coding:utf-8 -*-
   from obs import ObsClient,CompleteMultipartUploadRequest, CompletePart
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
       #Bucket name
       bucketName = "examplebucket"
       #Object name
       objectKey = "objectname"
       # Specify the MIME type for the object.
       contentType = 'text/plain'
       # Initiate a multipart upload.
       resp = obsClient.initiateMultipartUpload(bucketName, objectKey,
                                                contentType=contentType)
       #Obtain the uploadId.
       uploadId = resp.body["uploadId"]
       #Specify the size of the part to upload.
       partSize = 512 * 1024 * 1024
       #Specify the part number.
       partNum = 1
       # Specify whether object indicates the file path. True is used here. The default value is False.
       isFile = True
       #Specify the local object file to upload.
       filepath = r"D:\tmp\file.txt"
       contentLength = os.path.getsize(filepath)
       #Start offset of a part in the source file.
       offset = 0
       etags = {}

       while offset < contentLength:
           partSize = min(partSize, (contentLength - offset));
           # Upload parts.
           resp1 = obsClient.uploadPart(bucketName, objectKey, partNum, uploadId, filepath, isFile, partSize, offset)
           etags[partNum] = resp1.body.etag
           offset = offset + partSize
           partNum = partNum + 1

       completes = []
       for i in range(1, partNum):
           completes.append(CompletePart(i, etags[i]))
       # Assemble parts.
       completeMultipartUploadRequest = CompleteMultipartUploadRequest(parts = completes)
       resp = obsClient.completeMultipartUpload(bucketName, objectKey, uploadId, completeMultipartUploadRequest)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Upload Part Succeeded')
           print('requestId:', resp.requestId)
           print('etag:', resp.body.etag)
       else:
           print('Upload Part Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('multPartsUpload Failed')
       print(traceback.format_exc())

Below lists other multipart upload operations:

-  :ref:`Listing Uploaded Parts <obs_22_1004>`
-  :ref:`Listing Multipart Uploads <obs_22_1005>`
-  :ref:`Copying a Part <obs_22_1007>`
-  :ref:`Aborting a Multipart Upload <obs_22_1008>`
