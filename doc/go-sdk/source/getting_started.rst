:original_name: obs_23_0103.html

.. _obs_23_0103:

Getting Started
===============

Preparing Access Keys
---------------------

OBS employs access keys (AK and SK) for signature verification to ensure that only authorized accounts can access specified OBS resources. Detailed explanations of access keys are as follows:

-  AK is short for Access Key ID. One AK maps to only one user but one user can have multiple AKs. OBS authenticates users by their AKs.
-  SK is short for Secret Access Key, which is used to access OBS. You can generate authentication information based on SKs and request headers. An SK maps to an AK, and they group into a pair.

Access keys are permanent. There are also temporary security credentials (consisting of an AK/SK pair and a security token). Each user can create a maximum of two valid AK/SK pairs. Temporary security credentials can only be used to access OBS within the specified validity period. Once they expire, they must be requested again. For security purposes, you are advised to use temporary security credentials to access OBS. If you want to use permanent access keys, periodically update them.

#. Log in to the management console.
#. In the upper right corner, hover your cursor over the username and choose **My Credentials**.
#. On the **My Credentials** page, click **Access Keys** in the navigation pane.
#. On the **Access Keys** page, click **Create Access Key**.
#. In the **Create Access Key** dialog box, enter a description (recommended), and click **OK**.
#. In the displayed dialog box, click **Download** to save the access keys to your browser's default download path.
#. Open the downloaded **credentials.csv** file to obtain the access keys (AK and SK).

.. note::

   -  In the **credentials.csv** file, the AK is the value in the **Access Key ID** column, and the SK is the one in the **Secret Access Key** column.
   -  Keep the access keys properly to prevent information leakage. If you click **Cancel** in the download dialog box, the access keys will not be downloaded and cannot be downloaded later. You can create new access keys if required.

Obtaining Endpoints
-------------------

-  View the `endpoints and regions <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__ available for OBS.

.. important::

   OBS SDK for Go allows you to pass endpoints with or without a protocol. Suppose the endpoint you obtained is **your-endpoint**. You can pass **http://your-endpoint**, **https://your-endpoint**, or **your-endpoint** when initializing an obsClient instance.

Initializing an obsClient Instance
----------------------------------

Each time you want to send an HTTP or HTTPS request to OBS, you must create an ObsClient struct first. Sample code is as follows:

::

   // Import the dependency package.
   import (
       "obs-sdk-go/obs"
   )

   func main() {
       //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
       //Obtain an AK/SK pair on the management console.    ak := os.Getenv("AccessKeyID")
       sk := os.Getenv("SecretAccessKey")
       // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import it in other ways.
       // securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket is located.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint, obs.WithSignature(obs.SignatureObs)/*, obs.WithSecurityToken(securityToken)*/)
       if err == nil {
           // Use the obsClient to access OBS.

           // Close the obsClient.
           obsClient.Close()
       }
   }

.. note::

   -  For more information, see section "Initializing OBS SDK for Go."
   -  To learn log configuration, see :ref:`Log Initialization <obs_33_0103>`.
   -  If the **endpoint** you specified does not contain a protocol, HTTPS is used by default.
   -  For the sake of high DNS resolution performance and OBS reliability, you can set **endpoint** only to an OBS domain name, instead of an IP address.

Creating a Bucket
-----------------

A bucket is a global namespace of OBS. It is a container for storing objects and functions as a root directory of a file system.

This example creates a bucket named **examplebucket**. For bucket details, see the code comments below.

::

   package main

   import (
       "fmt"
       "os"
       "obs-sdk-go/obs"
   )

   func main() {
       //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
       //Obtain an AK/SK pair on the management console.
       ak := os.Getenv("AccessKeyID")
       sk := os.Getenv("SecretAccessKey")
       // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
       // securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint corresponding to the region where the bucket is to be created.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint/*, obs.WithSecurityToken(securityToken)*/)
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.CreateBucketInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify the region where the bucket is to be created. The region must be the same as that in the endpoint passed.
       input.Location = "region"
       // Specify the bucket ACL. obs.AclPrivate is used as an example.
       input.ACL = obs.AclPrivate
       // Specify a storage class for the bucket. obs.StorageClassWarm is used as an example. If this parameter is not specified, the created bucket is in the Standard storage class.
       input.StorageClass = obs.StorageClassWarm
      // Create a bucket.
       output, err := obsClient.CreateBucket(input)
       if err == nil {
           fmt.Printf("Create bucket:%s successful!\n", input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Create bucket:%s fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }

.. note::

   -  A bucket name must be unique across all accounts and regions.
   -  A bucket name:

      -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.
      -  Cannot be formatted as an IP address.
      -  Cannot start or end with a hyphen (-) or period (.).
      -  Cannot contain two consecutive periods (..), for example, **my..bucket**.
      -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.

   -  If you repeatedly create buckets of the same name, no error will be reported and the bucket attributes comply with those specified in the first creation request.
   -  For more information, see :ref:`Creating a Bucket <obs_33_0402>`.

Uploading an Object
-------------------

After creating a bucket, you can upload objects to it.

This example uploads **localfile** to **examplebucket** as an object named **example/objectname**.

::

   package main
   import (
       "fmt"
       "os"
       "obs-sdk-go/obs"
   )
   func main() {
       //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
       //Obtain an AK/SK pair on the management console.
       ak := os.Getenv("AccessKeyID")
       sk := os.Getenv("SecretAccessKey")
       // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
       securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint, obs.WithSecurityToken(securityToken))
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.PutFileInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify the object (example/objectname as an example) to upload.
       input.Key = "example/objectname"
       // Specify a local file (localfile as an example).
       input.SourceFile = "localfile"
       // Perform the file-based upload.
       output, err := obsClient.PutFile(input)
       if err == nil {
           fmt.Printf("Put file(%s) under the bucket(%s) successful!\n", input.Key, input.Bucket)
           fmt.Printf("StorageClass:%s, ETag:%s\n",
               output.StorageClass, output.ETag)
           return
       }
       fmt.Printf("Put file(%s) under the bucket(%s) fail!\n", input.Key, input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }

.. note::

   For more information, see :ref:`Object Upload Overview <obs_23_0401>`.
