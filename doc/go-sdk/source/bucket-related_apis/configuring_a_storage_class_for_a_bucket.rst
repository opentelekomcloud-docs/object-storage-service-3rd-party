:original_name: obs_33_0414.html

.. _obs_33_0414:

Configuring a Storage Class for a Bucket
========================================

Function
--------

This API configures a storage class for a bucket. If you do not specify a storage class when uploading or copying an object, or initiating a multipart upload, the object will inherit the bucket's storage class.

Restrictions
------------

-  To configure a storage class for a bucket, you must be the bucket owner or have the required permission (**obs:PutBucketStoragePolicy** in IAM or **PutBucketStoragePolicy** in a bucket policy).

Method
------

**func** (obsClient ObsClient) SetBucketStoragePolicy(input \*\ :ref:`SetBucketStoragePolicyInput <obs_33_0414__table14455523>`) (output \*\ :ref:`BaseModel <obs_33_0414__table1548013398476>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+---------------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                                | Mandatory (Yes/No) | Description                                                                                                            |
   +=================+=====================================================================+====================+========================================================================================================================+
   | input           | \*\ :ref:`SetBucketStoragePolicyInput <obs_33_0414__table14455523>` | Yes                | **Explanation:**                                                                                                       |
   |                 |                                                                     |                    |                                                                                                                        |
   |                 |                                                                     |                    | Input parameters for configuring a bucket storage class. For details, see :ref:`Table 2 <obs_33_0414__table14455523>`. |
   +-----------------+---------------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0414__table14455523:

.. table:: **Table 2** SetBucketStoragePolicyInput

   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                      | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+===========================================================+====================+===================================================================================================================================================================================+
   | Bucket          | string                                                    | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | Bucket name                                                                                                                                                                       |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                           |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                           |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                           |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                           |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                           |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | The value must contain 3 to 63 characters.                                                                                                                                        |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClass    | :ref:`StorageClassType <obs_33_0414__table1038544124819>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | Storage class of the bucket                                                                                                                                                       |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | For details about storage classes, see :ref:`Table 3 <obs_33_0414__table1038544124819>`.                                                                                          |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0414__table1038544124819:

.. table:: **Table 3** StorageClassType

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Constant              | Default Value         | Description                                                                                                                                                                       |
   +=======================+=======================+===================================================================================================================================================================================+
   | StorageClassStandard  | STANDARD              | OBS Standard                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                   |
   |                       |                       | Features low access latency and high throughput and is used for storing massive, frequently accessed (multiple times a month) or small objects (< 1 MB) requiring quick response. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClassWarm      | WARM                  | OBS Warm                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                   |
   |                       |                       | Used for storing data that is semi-frequently accessed (fewer than 12 times a year) but is instantly available when needed.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClassCold      | COLD                  | OBS Cold                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                   |
   |                       |                       | Used for storing rarely accessed (once a year) data.                                                                                                                              |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 4** List of returned results

   +-----------------------+--------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Parameter             | Type                                                   | Description                                                                          |
   +=======================+========================================================+======================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0414__table1548013398476>` | **Explanation:**                                                                     |
   |                       |                                                        |                                                                                      |
   |                       |                                                        | Returned results. For details, see :ref:`Table 5 <obs_33_0414__table1548013398476>`. |
   +-----------------------+--------------------------------------------------------+--------------------------------------------------------------------------------------+
   | err                   | error                                                  | **Explanation:**                                                                     |
   |                       |                                                        |                                                                                      |
   |                       |                                                        | Error messages returned by the API                                                   |
   +-----------------------+--------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_33_0414__table1548013398476:

.. table:: **Table 5** BaseModel

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================+
   | StatusCode            | int                   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP status code                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Request ID returned by the OBS server                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ResponseHeaders       | map[string][]string   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP response headers                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example returns the storage class of bucket **examplebucket**.

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
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint/*, obs.WithSecurityToken(securityToken)*/)
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.SetBucketStoragePolicyInput{}
       // Specify a bucket name.
       input.Bucket = "bucketname"
       // Specify a storage class (obs.StorageClassWarm as an example) for the bucket.
       input.StorageClass = obs.StorageClassWarm
       // Configure a storage class for the bucket.
       output, err := obsClient.SetBucketStoragePolicy(input)
       if err == nil {
           fmt.Printf("Set bucket(%s)'s storage-class successful!\n", input.Bucket)
           fmt.Printf("Set bucket storage-class successful!\n")
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Set bucket(%s)'s storage-class fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
