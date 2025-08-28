:original_name: obs_21_2114.html

.. _obs_21_2114:

How Can I Perform a Multipart Upload?
=====================================

In a multipart upload, you can specify a part of the file to be uploaded by performing the following steps:

#. Initialize an instance of ObsClient based on the AK, SK, and endpoint.
#. Specify the bucket name and object name to initialize **InitiateMultipartUploadRequest**. Call **InitiateMultipartUploadRequest.setMetadata** to specify the metadata of the object to be uploaded. Then, call **ObsClient.initiateMultipartUpload** to initiate a multipart upload task. A globally unique identifier (upload ID) for this task will be returned.
#. Specify the bucket name and object name to initialize **UploadPartRequest**. Call **UploadPartRequest.setUploadId** to specify the upload ID to which the part to be uploaded corresponds. Call **setPartNumber** to specify the part number of the part. Call **setFile** to specify the large file to which the part belongs. Call **setPartSize** to specify the part size. Then, call **ObsClient.uploadPart** to upload the part. The ETag value of the uploaded part is returned.
#. After all parts are uploaded, specify the bucket name, object name, **uploadId**, and **partEtags** to initialize a **CompleteMultipartUploadRequest** request. Then, call **ObsClient.completeMultipartUpload** to assemble parts.

For details, see :ref:`Multipart Upload <obs_21_0607>`.
