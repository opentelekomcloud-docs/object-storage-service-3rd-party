:original_name: obs_29_0606.html

.. _obs_29_0606:

Deleting an Object
==================

.. note::

   Exercise caution when performing this operation. If the versioning function is disabled for the bucket where the object is located, the object cannot be restored after being deleted.

Function
--------

This API deletes an object in the specified bucket to save space and costs.

Restrictions
------------

-  To delete an object, you must be the bucket owner or have the required permission (**obs:object:DeleteObject** in IAM or **DeleteObject** in a bucket policy).
-  If versioning is not enabled for a bucket, deleted objects cannot be restored.

Method
------

.. code-block::

   ObsClient.deleteObject(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                          |
   +=================+=================+====================+======================================================================================================================================================================================+
   | Bucket          | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Bucket name                                                                                                                                                                          |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                     |
   |                 |                 |                    | -  A bucket name:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                         |
   |                 |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                          |
   |                 |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                           |
   |                 |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                      |
   |                 |                 |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                            |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request. |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | The value can contain 3 to 63 characters.                                                                                                                                            |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key             | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name.                  |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | The value can contain 1 to 1,024 characters.                                                                                                                                         |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId       | string          | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Object version ID, for example, **G001117FCE89978B0000401205D5DC9A**                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | The value must contain 32 characters.                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 2** Responses

   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Type                                                                                      | Description                                                                          |
   +===========================================================================================+======================================================================================+
   | :ref:`Table 3 <obs_29_0606__table1722625714202>`                                          | **Explanation:**                                                                     |
   |                                                                                           |                                                                                      |
   | .. note::                                                                                 | Returned results. For details, see :ref:`Table 3 <obs_29_0606__table1722625714202>`. |
   |                                                                                           |                                                                                      |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. |                                                                                      |
   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_29_0606__table1722625714202:

.. table:: **Table 3** Response

   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                   |
   +=======================+=====================================================+===============================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_0606__table6176201212273>` | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 4 <obs_29_0606__table6176201212273>`. |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`Table 5 <obs_29_0606__table33959011>`         | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Results outputted for a successful call. For details, see :ref:`Table 5 <obs_29_0606__table33959011>`.                                                                        |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | **Restrictions:**                                                                                                                                                             |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | This parameter is not included if the value of **Status** is greater than 300.                                                                                                |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0606__table6176201212273:

.. table:: **Table 4** ICommonMsg

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

.. _obs_29_0606__table33959011:

.. table:: **Table 5** BaseResponseOutput

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                              |
   +=======================+=======================+==========================================================================================+
   | RequestId             | string                | **Explanation:**                                                                         |
   |                       |                       |                                                                                          |
   |                       |                       | Request ID returned by the OBS server                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | DeleteMarker          | boolean               | **Explanation:**                                                                         |
   |                       |                       |                                                                                          |
   |                       |                       | Whether the deleted object is a delete marker.                                           |
   |                       |                       |                                                                                          |
   |                       |                       | **Value range**:                                                                         |
   |                       |                       |                                                                                          |
   |                       |                       | -  **true**: The deleted object is a delete marker.                                      |
   |                       |                       | -  **false**: The deleted object is not a delete marker.                                 |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | VersionId             | string                | **Explanation:**                                                                         |
   |                       |                       |                                                                                          |
   |                       |                       | ID of the object version to be deleted, for example, **G001117FCE89978B0000401205D5DC9** |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+

Code Examples
-------------

This example deletes object **example/objectname** from bucket **examplebucket**.

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

   async function deleteObject() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify the object (example/objectname in this example) to delete.
         Key: 'example/objectname',
       };
       // Delete the object.
       const result = await obsClient.deleteObject(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Delete object(%s) under the bucket(%s) successful!", params.Key, params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         return;
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

   deleteObject();
