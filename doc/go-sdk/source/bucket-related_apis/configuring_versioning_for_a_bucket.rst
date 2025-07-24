:original_name: obs_33_0429.html

.. _obs_33_0429:

Configuring Versioning for a Bucket
===================================

Function
--------

You can enable versioning to automatically maintain previous versions of an object. When versioning is enabled, you can access earlier versions of an object to recover your data in the event of accidental actions or application failures.

This API configures the versioning status for a bucket.

Restrictions
------------

-  To configure versioning for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketVersioning** in IAM or **PutBucketVersioning** in a bucket policy).

Method
------

**func** (obsClient ObsClient) SetBucketVersioning(input \*\ :ref:`SetBucketVersioningInput <obs_33_0429__table14455523>`) (output \*\ :ref:`BaseModel <obs_33_0429__table1201244276>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                             | Mandatory (Yes/No) | Description                                                                                                         |
   +=================+==================================================================+====================+=====================================================================================================================+
   | input           | \*\ :ref:`SetBucketVersioningInput <obs_33_0429__table14455523>` | Yes                | **Explanation:**                                                                                                    |
   |                 |                                                                  |                    |                                                                                                                     |
   |                 |                                                                  |                    | Input parameters for bucket versioning configuration. For details, see :ref:`Table 2 <obs_33_0429__table14455523>`. |
   +-----------------+------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0429__table14455523:

.. table:: **Table 2** SetBucketVersioningInput

   +-----------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                          | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+===============================================================+====================+===================================================================================================================================================================================+
   | Bucket          | string                                                        | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | Bucket name                                                                                                                                                                       |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                               |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                               |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                               |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                               |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                               |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | None                                                                                                                                                                              |
   +-----------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status          | :ref:`VersioningStatusType <obs_33_0429__table7973154517515>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | Versioning status of the bucket                                                                                                                                                   |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | See :ref:`Table 3 <obs_33_0429__table7973154517515>`.                                                                                                                             |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | None                                                                                                                                                                              |
   +-----------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0429__table7973154517515:

.. table:: **Table 3** VersioningStatusType

   ========================= ============= ===========
   Constant                  Default Value Description
   ========================= ============= ===========
   VersioningStatusEnabled   Enabled       Enabled
   VersioningStatusSuspended Suspended     Suspended
   ========================= ============= ===========

Responses
---------

.. table:: **Table 4** List of returned results

   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                       |
   +=======================+=====================================================+===================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0429__table1201244276>` | **Explanation:**                                                                  |
   |                       |                                                     |                                                                                   |
   |                       |                                                     | Returned results. For details, see :ref:`Table 5 <obs_33_0429__table1201244276>`. |
   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------+
   | err                   | error                                               | **Explanation:**                                                                  |
   |                       |                                                     |                                                                                   |
   |                       |                                                     | Error messages returned by the API                                                |
   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------+

.. _obs_33_0429__table1201244276:

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

This example enables versioning for bucket **examplebucket**.

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
       input := &obs.SetBucketVersioningInput{}
       // Specify a bucket name.
       input.Bucket = "bucketname"
       // Specify the versioning status (obs.VersioningStatusEnabled as an example) for the bucket.
       input.Status = obs.VersioningStatusEnabled
       // Configure versioning for the bucket.
       output, err := obsClient.SetBucketVersioning(input)
       if err == nil {
           fmt.Printf("Set bucket(%s)'s versioning status successful!\n", input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Set bucket(%s)'s versioning status fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
