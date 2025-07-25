:original_name: obs_33_0506.html

.. _obs_33_0506:

Deleting an Object
==================

Function
--------

This API deletes an object in the specified bucket to save space and costs.

Restrictions
------------

-  To delete an object, you must be the bucket owner or have the required permission (**obs:object:DeleteObject** in IAM or **DeleteObject** in a bucket policy).
-  If versioning is not enabled for a bucket, deleted objects cannot be recovered.

Method
------

**func** (obsClient ObsClient) DeleteObject(input \*\ :ref:`DeleteObjectInput <obs_33_0506__table14455523>`) (output \*\ :ref:`DeleteObjectOutput <obs_33_0506__table4418114211447>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------+-----------------------------------------------------------+--------------------+-------------------------------------------+
   | Parameter | Type                                                      | Mandatory (Yes/No) | Description                               |
   +===========+===========================================================+====================+===========================================+
   | input     | \*\ :ref:`DeleteObjectInput <obs_33_0506__table14455523>` | Yes                | Request parameters for deleting an object |
   +-----------+-----------------------------------------------------------+--------------------+-------------------------------------------+

.. _obs_33_0506__table14455523:

.. table:: **Table 2** DeleteObjectInput

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
   | Key             | string          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Target object name An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                       |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId       | string          | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | ID of the object version to delete, for example, **G001117FCE89978B0000401205D5DC9**                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | The value must contain 32 characters.                                                                                                                                             |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None. If this parameter is left blank, the latest version of the object is deleted.                                                                                               |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** List of returned results

   +-----------------------+-----------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Parameter             | Type                                                            | Description                                                                          |
   +=======================+=================================================================+======================================================================================+
   | output                | \*\ :ref:`DeleteObjectOutput <obs_33_0506__table4418114211447>` | **Explanation:**                                                                     |
   |                       |                                                                 |                                                                                      |
   |                       |                                                                 | Returned results. For details, see :ref:`Table 4 <obs_33_0506__table4418114211447>`. |
   +-----------------------+-----------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | err                   | error                                                           | **Explanation:**                                                                     |
   |                       |                                                                 |                                                                                      |
   |                       |                                                                 | Error messages returned by the API                                                   |
   +-----------------------+-----------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_33_0506__table4418114211447:

.. table:: **Table 4** DeleteObjectOutput

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
   | DeleteMarker          | bool                  | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Whether the deleted object is a delete marker                                                                                                                               |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | -  **true**: The deleted object is a delete marker.                                                                                                                         |
   |                       |                       | -  **false**: The deleted object is not a delete marker.                                                                                                                    |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | false                                                                                                                                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId             | string                | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | ID of the object version to delete, for example, **G001117FCE89978B0000401205D5DC9**                                                                                        |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | The value must contain 32 characters.                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None. If this parameter is left blank, the latest version of the object is deleted.                                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example deletes object **example/objectname** from bucket **examplebucket**.

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
       input := &obs.DeleteObjectInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify the object (example/objectname as an example) to delete.
       input.Key = "example/objectname"
       // Delete the object.
       output, err := obsClient.DeleteObject(input)
       if err == nil {
           fmt.Printf("Delete object(%s) under the bucket(%s) successful!\n", input.Key, input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Delete object(%s) under the bucket(%s) fail!\n", input.Key, input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
