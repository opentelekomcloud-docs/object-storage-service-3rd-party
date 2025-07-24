:original_name: obs_33_0603.html

.. _obs_33_0603:

Server-Side Encryption
======================

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

**func** (obsClient ObsClient) PutFile(input \*PutFileInput) (output \*PutObjectOutput, err error)

Supported APIs
--------------

The following table lists APIs related to server-side encryption:

+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| Method in OBS SDK for Go          | Description                                                                                                                                      | Supported Encryption Method |
+===================================+==================================================================================================================================================+=============================+
| ObsClient.PutObject               | Sets the encryption algorithm and key during object upload to enable server-side encryption.                                                     | SSE-KMS                     |
|                                   |                                                                                                                                                  |                             |
|                                   |                                                                                                                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.PutFile                 | Sets the encryption algorithm and key during file upload to enable server-side encryption.                                                       | SSE-KMS                     |
|                                   |                                                                                                                                                  |                             |
|                                   |                                                                                                                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.GetObject               | Sets the decryption algorithm and key during object download to decrypt the object.                                                              | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.CopyObject              | #. Sets the decryption algorithm and key for decrypting the source object during object copy.                                                    | SSE-KMS                     |
|                                   | #. Sets the encryption algorithm and key during object copy to enable the encryption algorithm for the target object.                            |                             |
|                                   |                                                                                                                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.GetObjectMetadata       | Sets the decryption algorithm and key when obtaining the object metadata to decrypt the object.                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.InitiateMultipartUpload | Sets the encryption algorithm and key when initializing a multipart upload task to enable server-side encryption for the final object generated. | SSE-KMS                     |
|                                   |                                                                                                                                                  |                             |
|                                   |                                                                                                                                                  | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.UploadPart              | Sets the encryption algorithm and key during multipart upload to enable server-side encryption for parts.                                        | SSE-C                       |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+
| ObsClient.CopyPart                | #. Sets the decryption algorithm and key for decrypting the source object during multipart copy.                                                 | SSE-C                       |
|                                   | #. Sets the encryption algorithm and key during multipart copy to enable the encryption algorithm for the target part.                           |                             |
+-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------+

Code Examples
-------------

This example encrypts object **example/objectname** that is uploaded using streaming.

::

   package main
   import (
       "crypto/md5"
       "encoding/base64"
       "fmt"
       "os"
       "strings"
       "obs-sdk-go/obs"
   )
   func main() {
       //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
       //Obtain an AK/SK pair on the management console.
       ak := os.Getenv("AccessKeyID")
       sk := os.Getenv("SecretAccessKey")
       // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
       // securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint/*, obs.WithSecurityToken(securityToken)*/)
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.PutObjectInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify the object (example/objectname as an example) to upload.
       input.Key = "example/objectname"
       // Specify the content to upload.
       input.Body = strings.NewReader("Hello OBS")
       // Specify a server-side encryption header (obs.SseCHeader as an example).
       key := os.Getenv("Key")
       digest := md5.New()
       digest.Write([]byte(key))
       bodyHash := digest.Sum(nil)
       input.SseHeader = obs.SseCHeader{
           Encryption: "AES256",
           Key:        base64.StdEncoding.EncodeToString([]byte(key)), // 32byteslongsecretkeymustprovided
           KeyMD5:     base64.StdEncoding.EncodeToString(bodyHash),
       }
       // Upload you local file using streaming.
       output, err := obsClient.PutObject(input)
       if err == nil {
           fmt.Printf("Put object(%s) under the bucket(%s) successful!\n", input.Key, input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           fmt.Printf("StorageClass:%s, ETag:%s\n",
               output.StorageClass, output.ETag)
           return
       }
       fmt.Printf("Put object(%s) under the bucket(%s) fail!\n", input.Key, input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }

This example downloads the encrypted object **example/objectname** using streaming.

::

   package main
   import (
       "crypto/md5"
       "encoding/base64"
       "fmt"
       "os"
       "obs-sdk-go/obs"
   )
   func main() {
       // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
       // Obtain an AK/SK pair on the management console.
       ak := os.Getenv("AccessKeyID")
       sk := os.Getenv("SecretAccessKey")
       // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
       // securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint/*, obs.WithSecurityToken(securityToken)*/)
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.GetObjectInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify the object (example/objectname as an example) to download.
       input.Key = "example/objectname"
       // Specify a server-side encryption header (obs.SseCHeader as an example).
       key := os.Getenv("Key")
       digest := md5.New()
       digest.Write([]byte(key))
       bodyHash := digest.Sum(nil)
       input.SseHeader = obs.SseCHeader{
           Encryption: "AES256",
           Key:        base64.StdEncoding.EncodeToString([]byte(key)), // 32byteslongsecretkeymustprovided
           KeyMD5:     base64.StdEncoding.EncodeToString(bodyHash),
       }
       // Download the object using streaming.
       output, err := obsClient.GetObject(input)
       if err == nil {
           // Close output.Body after using it, to avoid connection leakage.
           defer output.Body.Close()
           fmt.Printf("Get object(%s) under the bucket(%s) successful!\n", input.Key, input.Bucket)
           fmt.Printf("StorageClass:%s, ETag:%s, ContentType:%s, ContentLength:%d, LastModified:%s\n",
               output.StorageClass, output.ETag, output.ContentType, output.ContentLength, output.LastModified)
           // Read the object content.
           p := make([]byte, 1024)
           var readErr error
           var readCount int
           for {
               readCount, readErr = output.Body.Read(p)
               if readCount > 0 {
                   fmt.Printf("%s", p[:readCount])
               }
               if readErr != nil {
                   break
               }
           }
           return
       }
       fmt.Printf("List objects under the bucket(%s) fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
