:original_name: obs_33_0412.html

.. _obs_33_0412:

Configuring a Storage Quota
===========================

Function
--------

A quota limits the maximum capacity allowed in a bucket. By default, there is no limit on the storage capacity of the entire OBS system or a single bucket, and any number of objects can be stored. You can set a storage quota to control the total size of objects that can be uploaded to the bucket. After the storage quota has been reached, object upload will fail.

A quota limit does not apply to the objects uploaded before the quota is configured. If the specified quota is already smaller than the total size of existing objects in the bucket, the existing objects in the bucket will not be deleted, but no more object can be uploaded to the bucket later. In this case, to upload new objects, you must delete some existing objects to make the used space below the quota limit.

Restrictions
------------

-  A bucket storage quota must be a non-negative integer expressed in bytes. The maximum value is as follows: 2\ :sup:`63` - 1.
-  OBS does not provide an API for deleting bucket storage quotas. You can set the bucket storage quota to **0** to cancel the limit.
-  To configure a storage quota for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketQuota** in IAM or **PutBucketQuota** in a bucket policy).

Method
------

**func** (obsClient ObsClient) SetBucketQuota(input \*\ :ref:`SetBucketQuotaInput <obs_33_0412__table14455523>`) (output \*\ :ref:`BaseModel <obs_33_0412__table119725162462>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                        | Mandatory (Yes/No) | Description                                                                                                     |
   +=================+=============================================================+====================+=================================================================================================================+
   | input           | \*\ :ref:`SetBucketQuotaInput <obs_33_0412__table14455523>` | Yes                | **Explanation:**                                                                                                |
   |                 |                                                             |                    |                                                                                                                 |
   |                 |                                                             |                    | Input parameters for configuring a storage quota. For details, see :ref:`Table 2 <obs_33_0412__table14455523>`. |
   +-----------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------+

.. _obs_33_0412__table14455523:

.. table:: **Table 2** SetBucketQuotaInput

   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=================+====================+===================================================================================================================================================================================+
   | Bucket          | string          | Yes                | **Explanation:**                                                                                                                                                                  |
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
   | Quota           | int64           | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Bucket storage quota                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | 0 to (2\ :sup:`63` - 1), in bytes                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **0**, indicating that there is no limit on the bucket quota.                                                                                                                     |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** List of returned results

   +-----------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+
   | Parameter             | Type                                                  | Description                                                                         |
   +=======================+=======================================================+=====================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0412__table119725162462>` | **Explanation:**                                                                    |
   |                       |                                                       |                                                                                     |
   |                       |                                                       | Returned results. For details, see :ref:`Table 4 <obs_33_0412__table119725162462>`. |
   +-----------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+
   | err                   | error                                                 | **Explanation:**                                                                    |
   |                       |                                                       |                                                                                     |
   |                       |                                                       | Error messages returned by the API                                                  |
   +-----------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+

.. _obs_33_0412__table119725162462:

.. table:: **Table 4** BaseModel

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

This example configures a 1 GB quota for bucket **examplebucket**.

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
       input := &obs.SetBucketQuotaInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify a 1 GB quota (measured in bytes) for the bucket.
       input.Quota = 1024 * 1024 * 1024
       // Configures a quota for the bucket.
       output, err := obsClient.SetBucketQuota(input)
       if err == nil {
           fmt.Printf("Set bucket(%s)'s quota successful!\n", input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Set bucket(%s)'s quota fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
