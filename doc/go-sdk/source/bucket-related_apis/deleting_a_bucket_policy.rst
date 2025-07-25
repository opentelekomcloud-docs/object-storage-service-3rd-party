:original_name: obs_33_0422.html

.. _obs_33_0422:

Deleting a Bucket Policy
========================

Function
--------

OBS provides access control over buckets. You can use an access policy to define whether a user can perform certain operations on a specific bucket. OBS access control can be implemented using IAM permissions, bucket policies, and ACLs.

A bucket policy is applied to a configured bucket and the objects in it. You can use a bucket policy to grant permissions for the bucket and the objects in it to IAM users or other accounts. If you want IAM users to have different permissions for different buckets, you can configure required bucket policies.

This API deletes the policy of a bucket. OBS returns "204 No Content" upon a successful deletion, regardless of whether the requested bucket policy exists or not.

Restrictions
------------

-  To delete the policy of a bucket, you must be the bucket owner or have the required permission (**obs:bucket:DeleteBucketPolicy** in IAM or **DeleteBucketPolicy** in a bucket policy).

Method
------

**func** (obsClient ObsClient) DeleteBucketPolicy(:ref:`bucketName <obs_33_0422__table26561495>` string) (output \*\ :ref:`BaseModel <obs_33_0422__table1201244276>`, err error)

Request Parameters
------------------

.. _obs_33_0422__table26561495:

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

   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                       |
   +=======================+=====================================================+===================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0422__table1201244276>` | **Explanation:**                                                                  |
   |                       |                                                     |                                                                                   |
   |                       |                                                     | Returned results. For details, see :ref:`Table 3 <obs_33_0422__table1201244276>`. |
   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------+
   | err                   | error                                               | **Explanation:**                                                                  |
   |                       |                                                     |                                                                                   |
   |                       |                                                     | Error messages returned by the API                                                |
   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------+

.. _obs_33_0422__table1201244276:

.. table:: **Table 3** BaseModel

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

This example deletes the policy of bucket **examplebucket**.

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
       obsClient, err := obs.New(ak, sk, endPoint /*, obs.WithSecurityToken(securityToken)*/)
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       // Specify a bucket name.
       bucketname := "examplebucket"
       // Delete the bucket policy.
       output, err := obsClient.DeleteBucketPolicy(bucketname)
       if err == nil {
           fmt.Printf("Delete policy successful with bucket:%s!\n", bucketname)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Delete policy fail with bucket:%s!\n", bucketname)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
