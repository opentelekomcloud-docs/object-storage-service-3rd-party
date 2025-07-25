:original_name: obs_33_0430.html

.. _obs_33_0430:

Obtaining the Versioning Status of a Bucket
===========================================

Function
--------

You can enable versioning to automatically maintain previous versions of an object. When versioning is enabled, you can access earlier versions of an object to recover your data in the event of accidental actions or application failures.

This API obtains the versioning status of a bucket.

Restrictions
------------

-  To obtain the versioning status of a bucket, you must be the bucket owner or have the required permission (**obs:bucket:GetBucketVersioning** in IAM or **GetBucketVersioning** in a bucket policy).

Method
------

**func** (obsClient ObsClient) GetBucketVersioning(:ref:`bucketName <obs_33_0430__table13982202>` string) (output \*\ :ref:`GetBucketVersioningOutput <obs_33_0430__table14455523>`, err error)

Request Parameters
------------------

.. _obs_33_0430__table13982202:

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=================+====================+===================================================================================================================================================================================+
   | bucketName      | string          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Bucket name                                                                                                                                                                       |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                 |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                 |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 2** List of returned results

   +-----------------------+-------------------------------------------------------------------+---------------------------------------------------------------------------------+
   | Parameter             | Type                                                              | Description                                                                     |
   +=======================+===================================================================+=================================================================================+
   | output                | \*\ :ref:`GetBucketVersioningOutput <obs_33_0430__table14455523>` | **Explanation:**                                                                |
   |                       |                                                                   |                                                                                 |
   |                       |                                                                   | Returned results. For details, see :ref:`Table 3 <obs_33_0430__table14455523>`. |
   +-----------------------+-------------------------------------------------------------------+---------------------------------------------------------------------------------+
   | err                   | error                                                             | **Explanation:**                                                                |
   |                       |                                                                   |                                                                                 |
   |                       |                                                                   | Error messages returned by the API                                              |
   +-----------------------+-------------------------------------------------------------------+---------------------------------------------------------------------------------+

.. _obs_33_0430__table14455523:

.. table:: **Table 3** GetBucketVersioningOutput

   +-----------------------+----------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                           | Description                                                                                                                                                                 |
   +=======================+================================================================+=============================================================================================================================================================================+
   | StatusCode            | int                                                            | **Explanation:**                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | HTTP status code                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Value range**:                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Default value**:                                                                                                                                                          |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | None                                                                                                                                                                        |
   +-----------------------+----------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                                                         | **Explanation:**                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | Request ID returned by the OBS server                                                                                                                                       |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Default value**:                                                                                                                                                          |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | None                                                                                                                                                                        |
   +-----------------------+----------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ResponseHeaders       | map[string][]string                                            | **Explanation:**                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | HTTP response headers                                                                                                                                                       |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Default value**:                                                                                                                                                          |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | None                                                                                                                                                                        |
   +-----------------------+----------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                | :ref:`VersioningStatusType <obs_33_0430__table16933639201013>` | **Explanation:**                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | Versioning status of the bucket                                                                                                                                             |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Value range**:                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | See :ref:`Table 4 <obs_33_0430__table16933639201013>`.                                                                                                                      |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Default value**:                                                                                                                                                          |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | None                                                                                                                                                                        |
   +-----------------------+----------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0430__table16933639201013:

.. table:: **Table 4** VersioningStatusType

   ========================= ============= ===========
   Constant                  Default Value Description
   ========================= ============= ===========
   VersioningStatusEnabled   Enabled       Enabled
   VersioningStatusSuspended Suspended     Suspended
   ========================= ============= ===========

Code Examples
-------------

This example returns the versioning status of bucket **examplebucket**.

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
       obsClient, err := obs.New(ak, sk, endPoint, obs.WithSignature(obs.SignatureObs)/*, obs.WithSecurityToken(securityToken)*/)
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       // Specify a bucket name.
       bucketname := "examplebucket"
       // Obtain the bucket's versioning status.
       output, err := obsClient.GetBucketVersioning(bucketname)
       if err == nil {
           fmt.Printf("Get bucket(%s)'s versioning status successful!\n", bucketname)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           fmt.Printf("VersioningStatus:%s\n", output.Status)
           return
       }
       fmt.Printf("Get bucket(%s)'s versioning status fail!\n", bucketname)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
