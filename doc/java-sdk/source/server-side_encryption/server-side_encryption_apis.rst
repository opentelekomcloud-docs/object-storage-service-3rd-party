:original_name: obs_21_1902.html

.. _obs_21_1902:

Server-Side Encryption APIs
===========================

The following table lists APIs related to server-side encryption:

+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| Method in OBS Java SDK            | Description                                                                                                                                                                                       | Supported Encryption Type |
+===================================+===================================================================================================================================================================================================+===========================+
| ObsClient.putObject               | Sets the encryption algorithm and key during object upload to enable server-side encryption.                                                                                                      | SSE-KMS                   |
|                                   |                                                                                                                                                                                                   |                           |
|                                   |                                                                                                                                                                                                   | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.getObject               | Users with the **KMS Administrator** permission can directly download objects encrypted using KMS. During a download, the backend decrypts KMS-encrypted objects before returning them. (SSE-KMS) | SSE-KMS                   |
|                                   |                                                                                                                                                                                                   |                           |
|                                   | Sets the decryption algorithm and key during object download to decrypt the object. (SSE-C)                                                                                                       | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.copyObject              | #. Sets the decryption algorithm and key for decrypting the source object during object copy.                                                                                                     | SSE-KMS                   |
|                                   | #. Sets the encryption algorithm and key during object copy to enable the encryption algorithm for the target object.                                                                             |                           |
|                                   |                                                                                                                                                                                                   | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.getObjectMetadata       | Sets the decryption algorithm and key when obtaining the object metadata to decrypt the object.                                                                                                   | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.initiateMultipartUpload | Sets the encryption algorithm and key when initializing a multipart upload to enable server-side encryption for the final object generated.                                                       | SSE-KMS                   |
|                                   |                                                                                                                                                                                                   |                           |
|                                   |                                                                                                                                                                                                   | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.uploadPart              | Sets the encryption algorithm and key during multipart upload to enable server-side encryption for parts.                                                                                         | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.copyPart                | #. Sets the decryption algorithm and key for decrypting the source object during multipart copy.                                                                                                  | SSE-C                     |
|                                   | #. Sets the encryption algorithm and key during multipart copy to enable the encryption algorithm for the target part.                                                                            |                           |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
