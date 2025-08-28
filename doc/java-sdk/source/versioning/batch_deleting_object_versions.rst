:original_name: obs_21_1011.html

.. _obs_21_1011:

Batch Deleting Object Versions
==============================

Function
--------

This API deletes objects in batches from a specific bucket. Deleted objects cannot be recovered.

In a batch delete operation, OBS concurrently deletes the specified objects and returns the deletion result of each object.

You can call **ObsClient.deleteObjects** to pass version IDs (**versionId**) to delete object versions.

Restrictions
------------

-  To delete objects in a batch, you must be the bucket owner or have the required permission (**obs:object:DeleteObject** in IAM or **DeleteObject** in a bucket policy).
-  If versioning is not enabled for a bucket, deleted objects cannot be recovered.
-  A maximum of 1,000 objects can be deleted at a time. If you send a request for deleting more than 1,000 objects, OBS returns an error message.
-  After concurrent tasks are assigned, if an internal error occurs during cyclic deletion of multiple objects, an object may be deleted in the index data but still exist in the metadata.

Method
------

obsClient.deleteObjects(:ref:`DeleteObjectsRequest <obs_21_1011__table421218296302>` :ref:`deleteRequest <obs_21_1011__table72121329103020>`)

Request Parameters
------------------

.. _obs_21_1011__table72121329103020:

.. table:: **Table 1** List of request parameters

   +-----------------+--------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                         | Mandatory (Yes/No) | Description                                                                                                           |
   +=================+==============================================================+====================+=======================================================================================================================+
   | deleteRequest   | :ref:`DeleteObjectsRequest <obs_21_1011__table421218296302>` | Yes                | **Explanation:**                                                                                                      |
   |                 |                                                              |                    |                                                                                                                       |
   |                 |                                                              |                    | Request parameters for deleting objects in batches. For details, see :ref:`Table 2 <obs_21_1011__table421218296302>`. |
   +-----------------+--------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1011__table421218296302:

.. table:: **Table 2** DeleteObjectsRequest

   +-----------------+--------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                         | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+==============================================================+====================+===================================================================================================================================================================================+
   | bucketName      | String                                                       | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | Bucket name.                                                                                                                                                                      |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                              |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                              |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                              |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                              |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                              |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | None                                                                                                                                                                              |
   +-----------------+--------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | keyAndVersions  | List<:ref:`KeyAndVersion <obs_21_1011__table1681555143414>`> | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | List of objects to be deleted. For details, see :ref:`Table 3 <obs_21_1011__table1681555143414>`.                                                                                 |
   +-----------------+--------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | quiet           | boolean                                                      | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | Response mode to the request for deleting objects in a batch.                                                                                                                     |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | -  **false**: The detailed mode. Results of both successful and failed deletions are returned.                                                                                    |
   |                 |                                                              |                    | -  **true**: The quiet mode. Only results of failed deletions are returned.                                                                                                       |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                              |                    |                                                                                                                                                                                   |
   |                 |                                                              |                    | **false**                                                                                                                                                                         |
   +-----------------+--------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1011__table1681555143414:

.. table:: **Table 3** KeyAndVersion

   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                           |
   +=================+=================+====================+=======================================================================================================================================================+
   | key             | String          | Yes                | **Explanation:**                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name. |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | **Value range**:                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                         |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | **Default value**:                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | None                                                                                                                                                  |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | versionId       | String          | No                 | **Explanation:**                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | Object version ID.                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | **Value range**:                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | The value must contain 32 characters.                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | **Default value**:                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | None. If this parameter is left blank, the latest version of the object is deleted.                                                                   |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 4** DeleteObjectsResult

   +-----------------------+--------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                               | Description                                                                                                                                                                 |
   +=======================+====================================================================+=============================================================================================================================================================================+
   | statusCode            | int                                                                | **Explanation:**                                                                                                                                                            |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | HTTP status code.                                                                                                                                                           |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | **Value range**:                                                                                                                                                            |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | **Default value**:                                                                                                                                                          |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | None                                                                                                                                                                        |
   +-----------------------+--------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | responseHeaders       | Map<String, Object>                                                | **Explanation:**                                                                                                                                                            |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | Response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header.      |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | **Default value**:                                                                                                                                                          |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | None                                                                                                                                                                        |
   +-----------------------+--------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | deletedObjectResults  | List<:ref:`DeleteObjectResult <obs_21_1011__table15127104401815>`> | **Explanation:**                                                                                                                                                            |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | Response results of the request for deleting objects in a batch. For details, see :ref:`Table 5 <obs_21_1011__table15127104401815>`.                                        |
   +-----------------------+--------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | errorResults          | List<:ref:`ErrorResult <obs_21_1011__table93551914173820>`>        | **Explanation:**                                                                                                                                                            |
   |                       |                                                                    |                                                                                                                                                                             |
   |                       |                                                                    | List of objects that fail to be deleted. For details, see :ref:`Table 6 <obs_21_1011__table93551914173820>`.                                                                |
   +-----------------------+--------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1011__table15127104401815:

.. table:: **Table 5** DeleteObjectResult

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================+
   | statusCode            | int                   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP status code.                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | responseHeaders       | Map<String, Object>   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header.      |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | versionId             | String                | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Object version ID.                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | The value must contain 32 characters.                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | deleteMarker          | boolean               | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Whether the deleted object is a delete marker.                                                                                                                              |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | -  **true**: The deleted object is a delete marker.                                                                                                                         |
   |                       |                       | -  **false**: The deleted object is not a delete marker.                                                                                                                    |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **false**                                                                                                                                                                   |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey             | String                | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | The value must contain 1 to 1,024 characters.                                                                                                                               |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1011__table93551914173820:

.. table:: **Table 6** ErrorResult

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                           |
   +=======================+=======================+=======================================================================================================================================================+
   | versionId             | String                | **Explanation:**                                                                                                                                      |
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
   | errorCode             | String                | **Explanation:**                                                                                                                                      |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | Error code for the failed deletion.                                                                                                                   |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey             | String                | **Explanation:**                                                                                                                                      |
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
   | message               | String                | **Explanation:**                                                                                                                                      |
   |                       |                       |                                                                                                                                                       |
   |                       |                       | Error message for the failed deletion.                                                                                                                |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example passes multiple version IDs (**versionId**) to batch delete object versions using **ObsClient.deleteObjects**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.DeleteObjectsRequest;
   import com.obs.services.model.DeleteObjectsResult;
   import com.obs.services.model.KeyAndVersion;
   import java.util.ArrayList;
   import java.util.List;
   public class DeleteObjects001 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
           // Enter the endpoint corresponding to the region where the bucket is to be created.
           String endPoint = "https://your-endpoint";
           // Obtain an endpoint using environment variables or import it in other ways.
           //String endPoint = System.getenv("ENDPOINT");

           // Create an ObsClient instance.
           // Use the permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use the temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               // Delete object versions in a batch.
               DeleteObjectsRequest request = new DeleteObjectsRequest("examplebucket");
               request.setQuiet(false);
               List<KeyAndVersion> toDelete = new ArrayList<KeyAndVersion>();
               toDelete.add(new KeyAndVersion("objectname1", "versionid1"));
               toDelete.add(new KeyAndVersion("objectname2", "versionid2"));
               toDelete.add(new KeyAndVersion("objectname3", "versionid3"));
               request.setKeyAndVersions(toDelete.toArray(new KeyAndVersion[toDelete.size()]));
               DeleteObjectsResult result = obsClient.deleteObjects(request);
               System.out.println("deleteObjects successfully");
               System.out.println("getDeletedObjectResults:" + result.getDeletedObjectResults());
               System.out.println("getErrorResults:" + result.getErrorResults());
           } catch (ObsException e) {
               System.out.println("deleteObjects failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code:" + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message:" + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
               e.printStackTrace();
           } catch (Exception e) {
               System.out.println("deleteObjects failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
