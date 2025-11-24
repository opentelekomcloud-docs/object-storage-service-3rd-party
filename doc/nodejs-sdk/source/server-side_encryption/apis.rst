:original_name: obs_29_1502.html

.. _obs_29_1502:

APIs
====

The following table lists APIs related to server-side encryption:

+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| Method in OBS Node.js SDK         | Description                                                                                                                                 | Supported Encryption Type |
+===================================+=============================================================================================================================================+===========================+
| ObsClient.putObject               | Sets the encryption algorithm and key during object upload to enable server-side encryption.                                                | SSE-KMS                   |
|                                   |                                                                                                                                             |                           |
|                                   |                                                                                                                                             | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.appendObject            | Sets the encryption algorithm and key during appendable upload to enable server-side encryption.                                            | SSE-KMS                   |
|                                   |                                                                                                                                             |                           |
|                                   |                                                                                                                                             | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.getObject               | Sets the decryption algorithm and key during object download to decrypt the object.                                                         | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.copyObject              | #. Sets the decryption algorithm and key for decrypting the source object during object copy.                                               | SSE-KMS                   |
|                                   | #. Sets the encryption algorithm and key during object copy to enable the encryption algorithm for the target object.                       |                           |
|                                   |                                                                                                                                             | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.getObjectMetadata       | Sets the decryption algorithm and key when obtaining the object metadata to decrypt the object.                                             | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.initiateMultipartUpload | Sets the encryption algorithm and key when initializing a multipart upload to enable server-side encryption for the final object generated. | SSE-KMS                   |
|                                   |                                                                                                                                             |                           |
|                                   |                                                                                                                                             | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.uploadPart              | Sets the encryption algorithm and key during multipart upload to enable server-side encryption for parts.                                   | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.copyPart                | #. Sets the decryption algorithm and key for decrypting the source object during partial object copy.                                       | SSE-C                     |
|                                   | #. Sets the encryption algorithm and key during partial object copy to enable the encryption algorithm for the target object part.          |                           |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+

OBS Node.js SDK supports the following two types of encryption/decryption mode:

+----------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Encryption/Decryption Type | Request Parameter | Description                                                                                                                                                                                               |
+============================+===================+===========================================================================================================================================================================================================+
| SSE-KMS                    | SseKms            | Indicates that SSE-KMS mode is used. Currently, only **kms** is supported.                                                                                                                                |
+----------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|                            | SseKmsKey         | Indicates the master key used in SSE-KMS mode. The value can be null.                                                                                                                                     |
+----------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| SSE-C                      | SseC              | Indicates that SSE-C mode is used. Currently, only **AES256** is supported.                                                                                                                               |
+----------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|                            | SseCKey           | Indicates the key in SSE-C mode. It is calculated using the AES256 algorithm. This parameter can be used to encrypt an object to be uploaded and decrypt an object to be downloaded.                      |
+----------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|                            | CopySourceSseC    | Indicates the source object decrypted in SSE-C mode. The value can only be AES256. This parameter is applicable to **ObsClient.copyObject** and **ObsClient.copyPart**.                                   |
+----------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|                            | CopySourceSseCKey | Indicates the key used by a source object for decryption in SSE-C mode. It is calculated using the AES256 algorithm. This parameter is applicable to **ObsClient.copyObject** and **ObsClient.copyPart**. |
+----------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
