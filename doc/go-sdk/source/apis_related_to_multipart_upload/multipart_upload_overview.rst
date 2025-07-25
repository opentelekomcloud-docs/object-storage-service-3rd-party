:original_name: obs_33_0521.html

.. _obs_33_0521:

Multipart Upload Overview
=========================

You can upload large files using multipart upload. Multipart upload is applicable to many scenarios, including:

-  Files to be uploaded are larger than 100 MB.
-  The network condition is poor. Connection to the OBS server is constantly down.
-  Sizes of files to be uploaded are uncertain.

A multipart upload consists of the following steps:

#. :ref:`Initiate a multipart upload <obs_33_0511>` (**ObsClient.InitiateMultipartUpload**).
#. :ref:`Upload parts one by one or concurrently <obs_33_0512>` (**ObsClient.UploadPart**).
#. :ref:`Assemble parts <obs_33_0515>` (**ObsClient.CompleteMultipartUpload**) or :ref:`abort the multipart upload <obs_33_0516>` (**ObsClient.AbortMultipartUpload**).

The following code shows how to perform a multipart upload:

::

   // Import a dependency.
   import (
       "fmt"
       "obs-sdk-go/obs"
   )

   //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
   //Obtain an AK/SK pair on the management console.ak := os.Getenv("AccessKeyID")
   sk := os.Getenv("SecretAccessKey")
   // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import it in other ways.
   // securityToken := os.Getenv("SecurityToken")
   // Enter the endpoint of the region where the bucket is located.
   endPoint := "https://your-endpoint"
   // Create an obsClient instance.
   // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
   obsClient, _:= obs.New(ak, sk, endPoint/*, obs.WithSecurityToken(securityToken)*/)

   func main() {
          var uploadId = ""
          var eTag1 = ""
          var eTag2 = ""
          var partNumber1= 1
          var partNumber2= 2

          // Initiate a multipart upload.
          inputInit := &obs.InitiateMultipartUploadInput{}
          inputInit.Bucket = "bucketname"
          inputInit.Key = "objectkey"
          outputInit, err := obsClient.InitiateMultipartUpload(inputInit)
          if err == nil {
                 fmt.Printf("RequestId:%s\n", outputInit.RequestId)
                 fmt.Printf("UploadId:%s\n", outputInit.UploadId)
                 uploadId = outputInit.UploadId
          } else {
                 if obsError, ok := err.(obs.ObsError); ok {
                        fmt.Println(obsError.Code)
                        fmt.Println(obsError.Message)
                 } else {
                        fmt.Println(err)
                 }
          }

          // Upload a part.
          inputUploadPart := &obs.UploadPartInput{}
          inputUploadPart.Bucket = "bucketname"
          inputUploadPart.Key = "objectkey"
          inputUploadPart.UploadId = uploadId
          inputUploadPart.PartNumber = partNumber1
          inputUploadPart.SourceFile = "localFilePath"
          outputUploadPart, err := obsClient.UploadPart(inputUploadPart)
          if err == nil {
                 fmt.Printf("RequestId:%s\n", outputUploadPart.RequestId)
                 fmt.Printf("ETag:%s\n", outputUploadPart.ETag)
                 eTag1 = outputUploadPart.ETag
          } else {
                 if obsError, ok := err.(obs.ObsError); ok {
                        fmt.Println(obsError.Code)
                        fmt.Println(obsError.Message)
                 } else {
                        fmt.Println(err)
                 }
          }
          inputUploadPart = &obs.UploadPartInput{}
          inputUploadPart.Bucket = "bucketname"
          inputUploadPart.Key = "objectkey"
          inputUploadPart.UploadId = uploadId
          inputUploadPart.PartNumber = partNumber2
          inputUploadPart.SourceFile = "localFilePath"
          outputUploadPart, err = obsClient.UploadPart(inputUploadPart)
          if err == nil {
                 fmt.Printf("RequestId:%s\n", outputUploadPart.RequestId)
                 fmt.Printf("ETag:%s\n", outputUploadPart.ETag)
                 eTag2 = outputUploadPart.ETag
          } else {
                 if obsError, ok := err.(obs.ObsError); ok {
                        fmt.Println(obsError.Code)
                        fmt.Println(obsError.Message)
                 } else {
                        fmt.Println(err)
                 }
          }

          // Assemble parts.
          inputCompleteMultipart := &obs.CompleteMultipartUploadInput{}
          inputCompleteMultipart.Bucket = "bucketname"
          inputCompleteMultipart.Key = "objectkey"
          inputCompleteMultipart.UploadId = uploadId
          inputCompleteMultipart.Parts = []obs.Part{
                 obs.Part{PartNumber: partNumber1, ETag: eTag1},
                 obs.Part{PartNumber: partNumber2, ETag: eTag2},
          }
          outputCompleteMultipart, err := obsClient.CompleteMultipartUpload(inputCompleteMultipart)
          if err == nil {
                 fmt.Printf("RequestId:%s\n", outputCompleteMultipart.RequestId)
                 fmt.Printf("Location:%s, Bucket:%s, Key:%s, ETag:%s\n", outputCompleteMultipart.Location, outputCompleteMultipart.Bucket, outputCompleteMultipart.Key, outputCompleteMultipart.ETag)
          } else {
                 if obsError, ok := err.(obs.ObsError); ok {
                        fmt.Println(obsError.Code)
                        fmt.Println(obsError.Message)
                 } else {
                        fmt.Println(err)
                 }
          }
   }

Below lists other multipart upload operations:

-  :ref:`Listing Multipart Uploads <obs_33_0408>`
-  :ref:`Listing Uploaded Parts <obs_33_0514>`
-  :ref:`Copying a Part <obs_33_0513>`
