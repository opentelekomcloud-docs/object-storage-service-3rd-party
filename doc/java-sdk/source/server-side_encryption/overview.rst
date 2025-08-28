:original_name: obs_21_1901.html

.. _obs_21_1901:

Overview
========

OBS provides server-side encryption for objects, so that they will be encrypted or decrypted when you upload them to or download them from a bucket.

The encryption and decryption happen on the server side.

There are different encryption methods for you to choose from.

With SSE-KMS, OBS uses the keys provided by Key Management Service (KMS) for server-side encryption. You can create custom keys for SSE-KMS encryption.

With SSE-C, OBS uses the keys and MD5 values of the keys provided by customers for server-side encryption.

When server-side encryption is used, the returned ETag value is not the object's MD5 value. OBS will verify the object's MD5 value as long as the upload request includes the **Content-MD5** header, no matter whether server-side encryption is used or not.

When server-side encryption is used, you are advised to use HTTPS to transmit and receive data.
