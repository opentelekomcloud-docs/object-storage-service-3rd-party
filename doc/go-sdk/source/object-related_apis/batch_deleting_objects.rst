:original_name: obs_33_0507.html

.. _obs_33_0507:

Batch Deleting Objects
======================

Function
--------

This API deletes objects in batches from a specific bucket. Deleted objects cannot be recovered.

In a batch delete operation, OBS concurrently deletes the specified objects and returns the deletion result of each object.

Restrictions
------------

-  To delete objects in a batch, you must be the bucket owner or have the required permission (**obs:object:DeleteObject** in IAM or **DeleteObject** in a bucket policy).
-  If versioning is not enabled for a bucket, deleted objects cannot be recovered.
-  A maximum of 1,000 objects can be deleted at a time. If you send a request for deleting more than 1,000 objects, OBS returns an error message.
-  After concurrent tasks are assigned, OBS may encounter an internal error during cyclic deletion of multiple objects. In that case, the metadata still exists when the object index data is deleted, which means data inconsistency.

Method
------

**func** (obsClient ObsClient) DeleteObjects(input \*\ :ref:`DeleteObjectsInput <obs_33_0507__table14455523>`) (output \*\ :ref:`DeleteObjectsOutput <obs_33_0507__table4418114211447>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                       | Mandatory (Yes/No) | Description                                                                                                |
   +=================+============================================================+====================+============================================================================================================+
   | input           | \*\ :ref:`DeleteObjectsInput <obs_33_0507__table14455523>` | Yes                | **Explanation:**                                                                                           |
   |                 |                                                            |                    |                                                                                                            |
   |                 |                                                            |                    | Input parameters for batch deleting objects. For details, see :ref:`Table 2 <obs_33_0507__table14455523>`. |
   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------+

.. _obs_33_0507__table14455523:

.. table:: **Table 2** DeleteObjectsInput

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
   | Quiet           | bool                                                          | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | Response to the request for deleting objects in a batch                                                                                                                           |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | -  **false**: The detailed mode. Results of both successful and failed deletions are returned.                                                                                    |
   |                 |                                                               |                    | -  **true**: The quiet mode. Only results of failed deletions are returned.                                                                                                       |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | false                                                                                                                                                                             |
   +-----------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Objects         | []\ :ref:`ObjectToDelete <obs_33_0507__table137571218103915>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                               |                    |                                                                                                                                                                                   |
   |                 |                                                               |                    | List of objects to be deleted. For details, see :ref:`Table 3 <obs_33_0507__table137571218103915>`.                                                                               |
   +-----------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0507__table137571218103915:

.. table:: **Table 3** ObjectToDelete

   +-----------------+-----------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                          |
   +=================+=================+====================+======================================================================================================================================================+
   | Key             | string          | Yes                | **Explanation:**                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | Object name An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name. |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                        |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                 |
   +-----------------+-----------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId       | string          | No                 | **Explanation:**                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | ID of the object version to delete, for example, **G001117FCE89978B0000401205D5DC9**                                                                 |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | The value must contain 32 characters.                                                                                                                |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                      |
   |                 |                 |                    | None. If this parameter is left blank, the latest version of the object is deleted.                                                                  |
   +-----------------+-----------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 4** List of returned results

   +-----------------------+------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Parameter             | Type                                                             | Description                                                                          |
   +=======================+==================================================================+======================================================================================+
   | output                | \*\ :ref:`DeleteObjectsOutput <obs_33_0507__table4418114211447>` | **Explanation:**                                                                     |
   |                       |                                                                  |                                                                                      |
   |                       |                                                                  | Returned results. For details, see :ref:`Table 5 <obs_33_0507__table4418114211447>`. |
   +-----------------------+------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | err                   | error                                                            | **Explanation:**                                                                     |
   |                       |                                                                  |                                                                                      |
   |                       |                                                                  | Error messages returned by the API                                                   |
   +-----------------------+------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_33_0507__table4418114211447:

.. table:: **Table 5** DeleteObjectsOutput

   +-----------------------+------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                 | Description                                                                                                                                                                 |
   +=======================+======================================================+=============================================================================================================================================================================+
   | StatusCode            | int                                                  | **Explanation:**                                                                                                                                                            |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | HTTP status code                                                                                                                                                            |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | **Value range**:                                                                                                                                                            |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | **Default value**:                                                                                                                                                          |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | None                                                                                                                                                                        |
   +-----------------------+------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                                               | **Explanation:**                                                                                                                                                            |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | Request ID returned by the OBS server                                                                                                                                       |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | **Default value**:                                                                                                                                                          |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | None                                                                                                                                                                        |
   +-----------------------+------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ResponseHeaders       | map[string][]string                                  | **Explanation:**                                                                                                                                                            |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | HTTP response headers                                                                                                                                                       |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | **Default value**:                                                                                                                                                          |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | None                                                                                                                                                                        |
   +-----------------------+------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleteds              | []\ :ref:`Deleted <obs_33_0507__table1486510774515>` | **Explanation:**                                                                                                                                                            |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | List of objects that are successfully deleted. For details, see :ref:`Table 6 <obs_33_0507__table1486510774515>`.                                                           |
   +-----------------------+------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Errors                | []\ :ref:`Error <obs_33_0507__table17613583454>`     | **Explanation:**                                                                                                                                                            |
   |                       |                                                      |                                                                                                                                                                             |
   |                       |                                                      | List of objects that fail to be deleted. For details, see :ref:`Table 7 <obs_33_0507__table17613583454>`.                                                                   |
   +-----------------------+------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0507__table1486510774515:

.. table:: **Table 6** Deleted

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                          |
   +=======================+=======================+======================================================================================================================================================================================================================+
   | Key                   | string                | **Explanation:**                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                                                                |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | **Value range**:                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | The value must contain 1 to 1,024 characters.                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | **Default value**:                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | None                                                                                                                                                                                                                 |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId             | string                | **Explanation:**                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | ID of the object version to delete, for example, **G001117FCE89978B0000401205D5DC9**                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | **Value range**:                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | The value must contain 32 characters.                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | **Default value**:                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | None. If this parameter is left blank, the latest version of the object is deleted.                                                                                                                                  |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DeleteMarker          | bool                  | **Explanation:**                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | Whether the deleted object is a delete marker                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | **Value range**:                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | -  **true**: The deleted object is a delete marker.                                                                                                                                                                  |
   |                       |                       | -  **false**: The deleted object is not a delete marker.                                                                                                                                                             |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | **Default value**:                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | false                                                                                                                                                                                                                |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DeleteMarkerVersionId | string                | **Explanation:**                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | Version ID of the delete marker to create or delete.                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | If the request either creates or deletes a delete marker, OBS returns this element in response with the version ID of the delete marker. This element will be returned in either of the following cases:             |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | -  You send a delete request with no version ID specified. In this case, OBS creates the delete marker and returns its version ID in the response.                                                                   |
   |                       |                       | -  You send a delete request with an object name and a version ID specified, but this version ID represents a delete marker. In this case, OBS deletes the delete marker and returns its version ID in the response. |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | **Default value**:                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                      |
   |                       |                       | None                                                                                                                                                                                                                 |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0507__table17613583454:

.. table:: **Table 7** Error

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                           |
   +=======================+=======================+=======================================================================================================================================================+
   | Key                   | string                | **Explanation:**                                                                                                                                      |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name. |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | **Value range**:                                                                                                                                      |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | The value must contain 1 to 1,024 characters.                                                                                                         |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | **Default value**:                                                                                                                                    |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | None                                                                                                                                                  |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId             | string                | **Explanation:**                                                                                                                                      |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | ID of the object version to delete, for example, **G001117FCE89978B0000401205D5DC9**                                                                  |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | **Value range**:                                                                                                                                      |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | The value must contain 32 characters.                                                                                                                 |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | **Default value**:                                                                                                                                    |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | None. If this parameter is left blank, the latest version of the object is deleted.                                                                   |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Code                  | string                | **Explanation:**                                                                                                                                      |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | Error code of the deletion failure.                                                                                                                   |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Message               | string                | **Explanation:**                                                                                                                                      |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | Error message of the deletion failure.                                                                                                                |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example deletes objects **key1**, **key2**, and **key3** from bucket **examplebucket** in a batch.

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
       input := &obs.DeleteObjectsInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify the list of objects to delete.
       var objects [3]obs.ObjectToDelete
       objects[0] = obs.ObjectToDelete{Key: "key1", VersionId: ""}
       objects[1] = obs.ObjectToDelete{Key: "key2", VersionId: ""}
       objects[2] = obs.ObjectToDelete{Key: "key3", VersionId: ""}
       input.Objects = objects[:]
       // Batch delete the objects.
       output, err := obsClient.DeleteObjects(input)
       if err == nil {
           fmt.Printf("Delete objects under the bucket(%s) successful!\n", input.Bucket)
           for index, deleted := range output.Deleteds {
               fmt.Printf("Deleted[%d]-Key:%s, VersionId:%s\n", index, deleted.Key, deleted.VersionId)
           }
           for index, err := range output.Errors {
               fmt.Printf("Error[%d]-Key:%s, Code:%s\n", index, err.Key, err.Code)
           }
           return
       }
       fmt.Printf("Delete objects under the bucket(%s) fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
