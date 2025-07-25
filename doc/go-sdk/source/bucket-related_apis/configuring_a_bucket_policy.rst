:original_name: obs_33_0420.html

.. _obs_33_0420:

Configuring a Bucket Policy
===========================

Function
--------

OBS provides access control over buckets. You can use an access policy to define whether a user can perform certain operations on a specific bucket. OBS access control can be implemented using IAM permissions, bucket policies, and ACLs.

A bucket policy is applied to a configured bucket and the objects in it. You can use a bucket policy to grant permissions for the bucket and the objects in it to IAM users or other accounts. If you want IAM users to have different permissions for different buckets, you can configure required bucket policies.

This API configures a policy for a bucket.

Restrictions
------------

-  Due to data caching, after a bucket policy is configured, it takes 5 minutes at most for the policy to take effect.
-  To configure a bucket policy, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketPolicy** in IAM or **PutBucketPolicy** in a bucket policy).

Method
------

**func** (obsClient ObsClient) SetBucketPolicy(input \*\ :ref:`SetBucketPolicyInput <obs_33_0420>`) (output \*\ :ref:`BaseModel <obs_33_0420__table16605114417504>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+--------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                         | Mandatory (Yes/No) | Description                                                                                                     |
   +=================+==============================================================+====================+=================================================================================================================+
   | input           | \*\ :ref:`SetBucketPolicyInput <obs_33_0420__table14455523>` | Yes                | **Explanation:**                                                                                                |
   |                 |                                                              |                    |                                                                                                                 |
   |                 |                                                              |                    | Input parameters for configuring a bucket policy. For details, see :ref:`Table 2 <obs_33_0420__table14455523>`. |
   +-----------------+--------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------+

.. _obs_33_0420__table14455523:

.. table:: **Table 2** SetBucketPolicyInput

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
   | Policy          | string          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Policy information in JSON format                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  The bucket name contained in the **Resource** parameter of the policy must be the one specified for the current bucket policy.                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** List of returned results

   +-----------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------+
   | Parameter             | Type                                                    | Description                                                                           |
   +=======================+=========================================================+=======================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0420__table16605114417504>` | **Explanation:**                                                                      |
   |                       |                                                         |                                                                                       |
   |                       |                                                         | Returned results. For details, see :ref:`Table 4 <obs_33_0420__table16605114417504>`. |
   +-----------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------+
   | err                   | error                                                   | **Explanation:**                                                                      |
   |                       |                                                         |                                                                                       |
   |                       |                                                         | Error messages returned by the API                                                    |
   +-----------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------+

.. _obs_33_0420__table16605114417504:

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

This example configures a policy for bucket **examplebucket**.

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
       input := &obs.SetBucketPolicyInput{}
       // Specify a bucket name.
       input.Bucket = "exampleBucket"
       // Create a bucket policy.
       input.Policy = "{\"Statement\":[{\"Sid\":\"Custom policy-2482\",\"Effect\":\"Allow\",\"Principal\":{\"ID\":[\"*\"]},\"Action\":[\"*\",\"ListBucket\"],\"Resource\":[\"" + input.Bucket + "\"]}]}"
       // Configure the bucket policy.
       output, err := obsClient.SetBucketPolicy(input)
       if err == nil {
           fmt.Printf("SetBucketPolicy:%s successful!\n", input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("SetBucketPolicy:%s fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
