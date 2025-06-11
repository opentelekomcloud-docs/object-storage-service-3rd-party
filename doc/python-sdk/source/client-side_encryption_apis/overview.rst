:original_name: obs_22_1010.html

.. _obs_22_1010:

Overview
========

Client-side encryption is a process where data is encrypted using the selected encryption method and information on your local PC before it is transmitted to an OBS server. During this process, the encryption method used and necessary information required for decryption will be stored in object metadata. During a download, the OBS SDK decrypts the data based on the key provided and the information stored in object metadata, and then returns the decrypted data.

.. warning::

   -  OBS does not store your master key in any way. Keep your master key correct and intact. If your master key is lost or mistakenly used, your data cannot be decrypted.
   -  Do not modify the information required for decryption in object metadata when moving or replicating an encrypted object or modifying the object metadata. If you do so, your data cannot be decrypted.

Encryption Process and Cipher Suites
------------------------------------

The OBS Python SDK offers two cipher suite generators: CTRCipherGenerator based on AES-CTR and CtrRSACipherGenerator based on RSA and AES-CTR.

If CTRCipherGenerator is used to upload objects, you need to provide a data key. The SDK then randomly generates an initial value for each object and uses the data key and initial value to encrypt the object. After the encryption, the SDK uploads the encrypted object to OBS and stores its initial value in object metadata. To download this object, you need to provide the corresponding data key. The SDK then automatically obtains the initial value from object metadata, uses the data key provided and initial value to decrypt the object, and returns the decrypted data. If a different data key is provided for download, the SDK returns an unavailable decrypted file.

If CtrRSACipherGenerator is used to upload objects, you need to provide an RSA public or private key. The SDK then randomly generates a data key and initial value for each object and uses the data key and initial value to encrypt the object. After that, the SDK uploads the encrypted object to OBS and then uses the RSA key to encrypt the data key. The encrypted data key and initial value are stored in the object metadata. To download this object, you need to provide the same RSA public or private key as you provided for the upload. The SDK then automatically obtains the data key and initial value stored in the object metadata and uses the provided key to decrypt the data key. If the provided key does not match the key used for the upload, an error will be reported. After the data key is decrypted, the SDK uses the decrypted data key and initial value to decrypt the object and returns the decrypted data.

API Changes
-----------

CryptoObsClient is inherited from ObsClient. Except the APIs listed in the following table, all other APIs of CryptoObsClient are the same as those of ObsClient.

.. table:: **Table 1**

   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | API                              | ObsClient API Action                               | CryptoObsClient API Action                                               |
   +==================================+====================================================+==========================================================================+
   | appendObject                     | Append data to an object.                          | Report an error.                                                         |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | copyPart                         | Copy an object part.                               | Report an error.                                                         |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | initiateMultipartUpload          | Initialize a multipart upload.                     | Report an error.                                                         |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | uploadPart                       | Upload object parts.                               | Report an error.                                                         |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | putContent                       | Upload streams or texts.                           | Encrypt streams or texts and then upload them to OBS.                    |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | putFile                          | Upload common files to OBS.                        | Encrypt common files and then upload them to OBS.                        |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | getObject                        | Download files.                                    | Decrypt files and then return the decrypted data.                        |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | uploadFile                       | Upload files in resumable mode to OBS.             | Encrypt files and then upload them in resumable mode to OBS.             |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | downloadFile                     | Download files in resumable mode to your local PC. | Decrypt files and then download them in resumable mode to your local PC. |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | initiateEncryptedMultipartUpload | None                                               | Initialize an encrypted multipart upload.                                |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+
   | uploadEncryptedPart              | None                                               | Encrypt uploaded parts.                                                  |
   +----------------------------------+----------------------------------------------------+--------------------------------------------------------------------------+

Decryption Information in Metadata
----------------------------------

The SDK saves the information required for decryption to the custom metadata of an object and does not back it up. If you modify the stored information, data cannot be decrypted. The table below describes the information required for decryption.

.. table:: **Table 2**

   +--------------------------+------------------------------------------+-------------------------------------------------------------------------+
   | Parameter                | Mandatory (Yes/No)                       | Description                                                             |
   +==========================+==========================================+=========================================================================+
   | encrypted-algorithm      | Yes                                      | Information about a cipher suite                                        |
   +--------------------------+------------------------------------------+-------------------------------------------------------------------------+
   | encrypted-object-key     | Yes (when CtrRSACipherGenerator is used) | Data key encrypted using an RSA key                                     |
   +--------------------------+------------------------------------------+-------------------------------------------------------------------------+
   | encrypted-start          | Yes                                      | String initially encoded using Base64. It is used to encrypt an object. |
   +--------------------------+------------------------------------------+-------------------------------------------------------------------------+
   | master-key-info          | No                                       | Information about an encryption key                                     |
   +--------------------------+------------------------------------------+-------------------------------------------------------------------------+
   | plaintext-sha256         | No                                       | SHA-256 value of an object before encryption                            |
   +--------------------------+------------------------------------------+-------------------------------------------------------------------------+
   | plaintext-content-length | No                                       | Object length before encryption                                         |
   +--------------------------+------------------------------------------+-------------------------------------------------------------------------+
   | encrypted-sha256         | No                                       | SHA-256 of an encrypted object                                          |
   +--------------------------+------------------------------------------+-------------------------------------------------------------------------+
