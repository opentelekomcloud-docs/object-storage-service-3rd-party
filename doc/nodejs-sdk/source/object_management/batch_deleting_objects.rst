:original_name: obs_29_0607.html

.. _obs_29_0607:

Batch Deleting Objects
======================

.. note::

   Exercise caution when performing this operation. If versioning is disabled for the bucket where objects are located, objects cannot be restored after being deleted.

Function
--------

This API deletes objects in a batch from a specific bucket. Deleted objects cannot be restored.

In a batch deletion, OBS concurrently deletes the specified objects and returns the deletion result of each object.

Restrictions
------------

-  To delete objects in a batch, you must be the bucket owner or have the required permission (**obs:object:DeleteObject** in IAM or **DeleteObject** in a bucket policy).
-  If versioning is not enabled for a bucket, deleted objects cannot be restored.
-  A maximum of 1,000 objects can be deleted at a time. If you send a request for deleting more than 1,000 objects, OBS returns an error message.
-  After concurrent tasks are assigned, if an internal error occurs during cyclic deletion of multiple objects, an object may be deleted in the index data but still exist in the metadata.

Method
------

.. code-block::

   ObsClient.deleteObjects(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                          | Mandatory (Yes/No) | Description                                                                                                                                                                          |
   +=================+===============================================================+====================+======================================================================================================================================================================================+
   | Bucket          | string                                                        | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | Bucket name                                                                                                                                                                          |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | **Restrictions:**                                                                                                                                                                    |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                     |
   |                 |                                                               |                    | -  A bucket name:                                                                                                                                                                    |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                         |
   |                 |                                                               |                    |    -  Cannot be formatted as an IP address.                                                                                                                                          |
   |                 |                                                               |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                           |
   |                 |                                                               |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                      |
   |                 |                                                               |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                            |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | The value can contain 3 to 63 characters.                                                                                                                                            |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | None                                                                                                                                                                                 |
   +-----------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Quiet           | boolean                                                       | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | Mode of the response to the request for deleting objects in a batch                                                                                                                  |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | None                                                                                                                                                                                 |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | -  **false**: The detailed mode. Results of both successful and failed deletions are returned.                                                                                       |
   |                 |                                                               |                    | -  **true**: The quiet mode. Only results of failed deletions are returned.                                                                                                          |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | false                                                                                                                                                                                |
   +-----------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Objects         | :ref:`ObjectToDelete <obs_29_0607__table137571218103915>`\ [] | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | List of objects to be deleted. For details, see :ref:`Table 2 <obs_29_0607__table137571218103915>`.                                                                                  |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | A maximum of 1000 objects can be deleted at a time.                                                                                                                                  |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | None                                                                                                                                                                                 |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                               |                    |                                                                                                                                                                                      |
   |                 |                                                               |                    | None                                                                                                                                                                                 |
   +-----------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0607__table137571218103915:

.. table:: **Table 2** ObjectToDelete

   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                         |
   +=================+=================+====================+=====================================================================================================================================================================+
   | Key             | string          | Yes                | **Explanation:**                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name. |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | None                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | **Value range**:                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | The value can contain 1 to 1,024 characters.                                                                                                                        |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | **Default value**:                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | None                                                                                                                                                                |
   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId       | string          | No                 | **Explanation:**                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | ID of the object version to be deleted, for example, **G001117FCE89978B0000401205D5DC9**.                                                                           |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | None                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | **Value range**:                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | The value must contain 32 characters.                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | **Default value**:                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                     |
   |                 |                 |                    | None. If this parameter is left blank, the latest version of the object is deleted.                                                                                 |
   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** Responses

   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Type                                                                                      | Description                                                                          |
   +===========================================================================================+======================================================================================+
   | :ref:`Table 4 <obs_29_0607__table1722625714202>`                                          | **Explanation:**                                                                     |
   |                                                                                           |                                                                                      |
   | .. note::                                                                                 | Returned results. For details, see :ref:`Table 4 <obs_29_0607__table1722625714202>`. |
   |                                                                                           |                                                                                      |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. |                                                                                      |
   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_29_0607__table1722625714202:

.. table:: **Table 4** Response

   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                   |
   +=======================+=====================================================+===============================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_0607__table6176201212273>` | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 5 <obs_29_0607__table6176201212273>`. |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`Table 6 <obs_29_0607__table33959011>`         | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Results outputted for a successful call. For details, see :ref:`Table 6 <obs_29_0607__table33959011>`.                                                                        |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | **Restrictions:**                                                                                                                                                             |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | This parameter is not included if the value of **Status** is greater than 300.                                                                                                |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0607__table6176201212273:

.. table:: **Table 5** ICommonMsg

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Parameter**         | **Type**              | **Description**                                                                                                                                                  |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                | number                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | HTTP status code returned by the OBS server.                                                                                                                     |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | **Value range**:                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | A status code is a group of digits indicating the status of a response. It ranges from 2\ *xx* (indicating successes) to 4\ *xx* or 5\ *xx* (indicating errors). |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Code                  | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Error code returned by the OBS server.                                                                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Message               | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Error description returned by the OBS server.                                                                                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HostId                | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Request server ID returned by the OBS server.                                                                                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Request ID returned by the OBS server.                                                                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Id2                   | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Request ID2 returned by the OBS server.                                                                                                                          |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Indicator             | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Error code details returned by the OBS server.                                                                                                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0607__table33959011:

.. table:: **Table 6** DeleteObjectsOutput

   +-----------------------+------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                 | Description                                                                                                        |
   +=======================+======================================================+====================================================================================================================+
   | RequestId             | string                                               | **Explanation:**                                                                                                   |
   |                       |                                                      |                                                                                                                    |
   |                       |                                                      | Request ID returned by the OBS server                                                                              |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Deleteds              | :ref:`Deleted <obs_29_0607__table1486510774515>`\ [] | **Explanation:**                                                                                                   |
   |                       |                                                      |                                                                                                                    |
   |                       |                                                      | List of objects that were successfully deleted. For details, see :ref:`Table 7 <obs_29_0607__table1486510774515>`. |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Errors                | :ref:`Error <obs_29_0607__table17613583454>`\ []     | **Explanation:**                                                                                                   |
   |                       |                                                      |                                                                                                                    |
   |                       |                                                      | List of objects that failed to be deleted. For details, see :ref:`Table 8 <obs_29_0607__table17613583454>`.        |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0607__table1486510774515:

.. table:: **Table 7** Deleted

   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                              |
   +=======================+=======================+==========================================================================================================================================================================================================================+
   | Key                   | string                | **Explanation:**                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                          |
   |                       |                       | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name.                                                      |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId             | string                | **Explanation:**                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                          |
   |                       |                       | Object version ID, for example, **G001117FCE89978B0000401205D5DC9**.                                                                                                                                                     |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DeleteMarker          | bool                  | **Explanation:**                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                          |
   |                       |                       | Whether the deleted object is a delete marker.                                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                                                                          |
   |                       |                       | **Value range**:                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                          |
   |                       |                       | -  **true**: The deleted object is a delete marker.                                                                                                                                                                      |
   |                       |                       | -  **false**: The deleted object is not a delete marker.                                                                                                                                                                 |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DeleteMarkerVersionId | string                | **Explanation:**                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                          |
   |                       |                       | Version ID of a delete marker to create or delete.                                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                                                                          |
   |                       |                       | OBS returns this element in the response when a delete marker is created or deleted for a versioning-enabled bucket. This element will be returned in either of the following cases:                                     |
   |                       |                       |                                                                                                                                                                                                                          |
   |                       |                       | -  You send a delete request specifying an object's name without providing a version ID. In this case, OBS creates a delete marker and returns its version ID in the response.                                           |
   |                       |                       | -  You send a delete request specifying both an object's name and its version ID, but this version ID points to a delete marker. In this case, OBS deletes the delete marker and returns its version ID in the response. |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0607__table17613583454:

.. table:: **Table 8** Error

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                         |
   +=======================+=======================+=====================================================================================================================================================================+
   | Key                   | string                | **Explanation:**                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                     |
   |                       |                       | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId             | string                | **Explanation:**                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                     |
   |                       |                       | Object version ID, for example, **G001117FCE89978B0000401205D5DC9**.                                                                                                |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Code                  | string                | **Explanation:**                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                     |
   |                       |                       | Error code for the failed deletion.                                                                                                                                 |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Message               | string                | **Explanation:**                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                     |
   |                       |                       | Error message for the failed deletion.                                                                                                                              |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

Sample code:

::

   // Import the OBS library.
   // Use npm to install the client.
   const ObsClient = require("esdk-obs-nodejs");
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');

   // Create an instance of ObsClient.
   const obsClient = new ObsClient({
     // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
     // Obtain an AK/SK pair on the management console.
     access_key_id: process.env.ACCESS_KEY_ID,
     secret_access_key: process.env.SECRET_ACCESS_KEY,
     // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
     // security_token: process.env.SECURITY_TOKEN,
     // Enter the endpoint of the region where the bucket is located.
     server: "https://your-endpoint"
   });

   async function deleteObjects() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify the object list to delete.
         Objects: [
           { Key: 'objectname1', VersionId: "version1" },
           { Key: 'objectname2', VersionId: "version2" },
           { Key: 'objectname3', VersionId: "version3" }
         ]
       };
       // Delete the objects in a batch.
       const result = await obsClient.deleteObjects(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Delete objects under the bucket(%s) successful!", params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         // Return details about which objects were deleted.
         console.log('Deleteds:');
         for (let i = 0; i < result.InterfaceResult.Deleteds.length; i++) {
           const deleted = result.InterfaceResult.Deleteds[i];
           console.log("Deleted[%d]-Key:%s, VersionId:%s", i, deleted.Key, deleted.VersionId);
         };
         // Return details about which objects were not deleted.
         console.log('Errors:');
         for (let i = 0; i < result.InterfaceResult.Errors.length; i++) {
           const err = result.InterfaceResult.Errors[i];
           console.log("Errors[%d]-Key:%s, Code:%s", i, err.Key, err.Code);
         };
       };
       console.log("An ObsError was found, which means your request sent to OBS was rejected with an error response.");
       console.log("Status: %d", result.CommonMsg.Status);
       console.log("Code: %s", result.CommonMsg.Code);
       console.log("Message: %s", result.CommonMsg.Message);
       console.log("RequestId: %s", result.CommonMsg.RequestId);
     } catch (error) {
       console.log("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.");
       console.log(error);
     };
   };

   deleteObjects();
