:original_name: obs_25_1502.html

.. _obs_25_1502:

Encryption Description
======================

The following table lists APIs related to server-side encryption:

+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| OBS .NET SDK API Function         | Description                                                                                                                                 | Supported Encryption Type |
+===================================+=============================================================================================================================================+===========================+
| ObsClient.PutObject               | Sets the encryption algorithm and key during object upload to enable server-side encryption.                                                | SSE-KMS                   |
|                                   |                                                                                                                                             |                           |
|                                   |                                                                                                                                             | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.GetObject               | Sets the decryption algorithm and key during object download to decrypt the object.                                                         | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.CopyObject              | #. Sets the decryption algorithm and key for decrypting the source object during object copy.                                               | SSE-KMS                   |
|                                   | #. Sets the encryption algorithm and key during object copy to enable the encryption algorithm for the target object.                       |                           |
|                                   |                                                                                                                                             | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.GetObjectMetadata       | Sets the decryption algorithm and key when obtaining the object metadata to decrypt the object.                                             | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.InitiateMultipartUpload | Sets the encryption algorithm and key when initializing a multipart upload to enable server-side encryption for the final object generated. | SSE-KMS                   |
|                                   |                                                                                                                                             |                           |
|                                   |                                                                                                                                             | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.UploadPart              | Sets the encryption algorithm and key during multipart upload to enable server-side encryption for parts.                                   | SSE-C                     |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| ObsClient.CopyPart                | #. Sets the decryption algorithm and key for decrypting the source object during partial object copy.                                       | SSE-C                     |
|                                   | #. Sets the encryption algorithm and key during partial object copy to enable the encryption algorithm for the target object part.          |                           |
+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
