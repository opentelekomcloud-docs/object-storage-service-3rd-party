:original_name: obs_21_2302.html

.. _obs_21_2302:

Overview
========

Client-side encryption is a process where data is encrypted using the selected encryption method and information on your local PC before it is transmitted to an OBS server. During this process, the encryption method used and necessary information required for decryption will be stored in object metadata. During a download, the OBS SDK decrypts the data based on the key provided and the information stored in object metadata, and then returns the decrypted data.

.. warning::

   -  OBS does not store your master key in any way. Keep your master key correct and intact. If your master key is lost or mistakenly used, your data cannot be decrypted.
   -  Do not modify the decryption information stored in object metadata when moving or replicating an encrypted object or modifying the object metadata. If you do so, your data cannot be decrypted.
   -  For security purposes, later SDK versions will use RSA/ECB/OAEPWITHSHA-256ANDMGF1PADDING in place of RSA for encryption and, therefore, will be incompatible with earlier versions.
   -  You are advised to add the SDK version information to **master-key-info** to avoid data encryption or decryption failures caused by changes of encryption algorithms and key length restrictions.
   -  Consider both security and performance when determining the RSA key size. Later SDK versions will require the key size be larger than 3,072 bits.
   -  Consider both security and performance when configuring **secureRandom**.
   -  RSA keys in PKCS #8 format are recommended.

Encryption Process and Cipher Suites
------------------------------------

The OBS SDK for Java offers two cipher suite generators: CTRCipherGenerator based on AES-CTR, and CtrRSACipherGenerator based on RSA and AES-CTR.

If CTRCipherGenerator is used to upload objects, you need to provide a data key. The SDK then randomly generates an initial value for each object and uses the data key and initial value to encrypt the object. After the encryption, the SDK uploads the encrypted object to OBS and stores its initial value in object metadata. To download this object, you need to use the same data key used for upload. The SDK automatically obtains the initial value from object metadata, uses the data key provided and initial value to decrypt the object, and returns the decrypted data. If a different data key is provided for download, the SDK returns an unavailable decrypted file.

If CtrRSACipherGenerator is used to upload objects, you need to provide an RSA public key. The SDK then randomly generates a data key and initial value for each object and uses them to encrypt the object. After that, the SDK uploads the encrypted object to OBS and then uses the provided RSA key to encrypt the data key. The encrypted data key and initial value are stored in the object metadata. To download this object, you need to provide the corresponding RSA private key. The SDK then automatically obtains the data key and initial value stored in the object metadata and uses the provided RSA private key to decrypt the data key. If the provided private key does not match the public key used for upload, an error will be reported. After the data key is decrypted, the SDK uses the decrypted data key and initial value to decrypt the object and returns the decrypted data.

API Changes
-----------

CryptoObsClient is inherited from ObsClient. Except the APIs listed in the following table, all other APIs of CryptoObsClient are the same as those of ObsClient.

.. table:: **Table 1** CryptoObsClient

   ========= ======================================================
   API       CryptoObsClient API Action
   ========= ======================================================
   putObject Encrypts streams or files and then upload them to OBS.
   getObject Returns the decrypted data streams.
   ========= ======================================================

Decryption Information in Metadata
----------------------------------

The SDK saves the information required for decryption in the user-defined metadata of an object and does not back it up. If you modify the stored information, data cannot be decrypted. The following table describes the information required for decryption.

.. table:: **Table 2**

   +--------------------------+----------------------------------------+------------------------------------------------------------------------------------------+
   | Parameter                | Mandatory (Yes/No)                     | Description                                                                              |
   +==========================+========================================+==========================================================================================+
   | encrypted-algorithm      | Yes                                    | Information about a cipher suite                                                         |
   +--------------------------+----------------------------------------+------------------------------------------------------------------------------------------+
   | encrypted-object-key     | Yes when CtrRSACipherGenerator is used | Data key encrypted using an RSA key                                                      |
   +--------------------------+----------------------------------------+------------------------------------------------------------------------------------------+
   | encrypted-start          | Yes                                    | String of the Base64-encoded initial value used for encryption                           |
   +--------------------------+----------------------------------------+------------------------------------------------------------------------------------------+
   | master-key-info          | No                                     | Information about encryption keys                                                        |
   +--------------------------+----------------------------------------+------------------------------------------------------------------------------------------+
   | plaintext-sha256         | No                                     | SHA-256 value of the object before being encrypted (not available for streaming uploads) |
   +--------------------------+----------------------------------------+------------------------------------------------------------------------------------------+
   | plaintext-content-length | No                                     | Length of the object before being encrypted (not available for streaming uploads)        |
   +--------------------------+----------------------------------------+------------------------------------------------------------------------------------------+
   | encrypted-sha256         | No                                     | SHA-256 value of the object after being encrypted (not available for streaming uploads)  |
   +--------------------------+----------------------------------------+------------------------------------------------------------------------------------------+
