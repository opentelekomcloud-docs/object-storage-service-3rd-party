:original_name: obs_29_0806.html

.. _obs_29_0806:

Restoring a Cold Object Version
===============================

Function
--------

To download an object in the Cold storage class, you need to restore it first. After an object is restored, a copy of the object is saved in the Standard storage class. By doing so, the object in the Cold storage class and its copy in the Standard storage class co-exist in the bucket. The copy will be automatically deleted once its retention period ends.

This API restores a Cold object in a specified bucket.

Restrictions
------------

-  To restore a Cold object, you must be the bucket owner or have the required permission (**obs:object:RestoreObject** in IAM or **RestoreObject** in a bucket policy.)
-  To extend the validity period of the Cold data restored, you can repeatedly restore the data, but you will be billed for each restoration. After a restoration, the validity period of Standard object copies will be extended, and you need to pay for storing these copies during the extended period.

Method
------

.. code-block::

   ObsClient.restoreObject(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                | Mandatory (Yes/No) | Description                                                                                                                                                                                         |
   +=================+=====================================================+====================+=====================================================================================================================================================================================================+
   | Bucket          | string                                              | Yes                | **Explanation:**                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | Bucket name                                                                                                                                                                                         |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Restrictions**:                                                                                                                                                                                   |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                                    |
   |                 |                                                     |                    | -  A bucket name:                                                                                                                                                                                   |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                        |
   |                 |                                                     |                    |    -  Cannot be formatted as an IP address.                                                                                                                                                         |
   |                 |                                                     |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                          |
   |                 |                                                     |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                     |
   |                 |                                                     |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                           |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request.                |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Value range**:                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | The value can contain 3 to 63 characters.                                                                                                                                                           |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Default value**:                                                                                                                                                                                  |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | None                                                                                                                                                                                                |
   +-----------------+-----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key             | string                                              | Yes                | **Explanation:**                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name.                                 |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Restrictions**:                                                                                                                                                                                   |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | The object specified in **ObsClient.restoreObject** must be in the Cold storage class. Otherwise, an error is reported.                                                                             |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Value range**:                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | The value can contain 1 to 1,024 characters.                                                                                                                                                        |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Default value**:                                                                                                                                                                                  |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | None                                                                                                                                                                                                |
   +-----------------+-----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId       | string                                              | No                 | **Explanation:**                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | Version ID of the Cold object to restore.                                                                                                                                                           |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Restrictions**:                                                                                                                                                                                   |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | None                                                                                                                                                                                                |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Value range**:                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | The value must contain 32 characters.                                                                                                                                                               |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Default value**:                                                                                                                                                                                  |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | None. If this parameter is left blank, the latest version of the object is specified.                                                                                                               |
   +-----------------+-----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Days            | number                                              | Yes                | **Explanation:**                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | After an object is restored, a Standard copy is generated for the object. This parameter specifies how long the Standard copy can be retained, that is, the validity period of the restored object. |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Restrictions**:                                                                                                                                                                                   |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | None                                                                                                                                                                                                |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Value range**:                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | The value ranges from 1 to 30, in days.                                                                                                                                                             |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Default value**:                                                                                                                                                                                  |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | None                                                                                                                                                                                                |
   +-----------------+-----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Tier            | :ref:`RestoreTierType <obs_29_0806__table59775506>` | No                 | **Explanation:**                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | Tier of the restoration speed. You can select a suitable tier based on your needs.                                                                                                                  |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Restrictions**:                                                                                                                                                                                   |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | None                                                                                                                                                                                                |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Value range**:                                                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | See :ref:`Table 2 <obs_29_0806__table59775506>`.                                                                                                                                                    |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Default value**:                                                                                                                                                                                  |
   |                 |                                                     |                    |                                                                                                                                                                                                     |
   |                 |                                                     |                    | **Standard**                                                                                                                                                                                        |
   +-----------------+-----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0806__table59775506:

.. table:: **Table 2** RestoreTierType

   +--------------------------------------+---------------+--------------------------------------------------------------------------+
   | Constant                             | Default Value | Description                                                              |
   +======================================+===============+==========================================================================+
   | ObsClient.enums.RestoreTierExpedited | Expedited     | Objects can be quickly restored from Cold storage within 1 to 5 minutes. |
   +--------------------------------------+---------------+--------------------------------------------------------------------------+
   | ObsClient.enums.RestoreTierStandard  | Standard      | Objects can be restored from Cold storage within 3 to 5 hours.           |
   +--------------------------------------+---------------+--------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** Responses

   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Type                                                                                      | Description                                                                          |
   +===========================================================================================+======================================================================================+
   | :ref:`Table 4 <obs_29_0806__table1722625714202>`                                          | **Explanation:**                                                                     |
   |                                                                                           |                                                                                      |
   | .. note::                                                                                 | Returned results. For details, see :ref:`Table 4 <obs_29_0806__table1722625714202>`. |
   |                                                                                           |                                                                                      |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. |                                                                                      |
   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_29_0806__table1722625714202:

.. table:: **Table 4** Response

   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                   |
   +=======================+=====================================================+===============================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_0806__table6176201212273>` | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 5 <obs_29_0806__table6176201212273>`. |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`Table 6 <obs_29_0806__table33959011>`         | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Results outputted for a successful call. For details, see :ref:`Table 6 <obs_29_0806__table33959011>`.                                                                        |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | **Restrictions:**                                                                                                                                                             |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | This parameter is not included if the value of **Status** is greater than 300.                                                                                                |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0806__table6176201212273:

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

.. _obs_29_0806__table33959011:

.. table:: **Table 6** BaseResponseOutput

   +-----------------------+-----------------------+---------------------------------------+
   | Parameter             | Type                  | Description                           |
   +=======================+=======================+=======================================+
   | RequestId             | string                | **Explanation:**                      |
   |                       |                       |                                       |
   |                       |                       | Request ID returned by the OBS server |
   +-----------------------+-----------------------+---------------------------------------+

Code Examples
-------------

This example restores version **G001117FCE89978B0000401205D5DC9A** of Cold object **example/objectname** in bucket **examplebucket**.

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

   async function restoreObject() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify an object. example/objectname is used in this example.
         Key: "example/objectname",
         // Specify the version ID of the object.
         VersionId: 'G001117FCE89978B0000401205D5DC9A'
         // Specify how long the restored object will be retained, in days. The value ranges from 1 to 30 (1 is used in this example).
         Days: 1,
         // Specify the restore speed (obs.RestoreTierExpedited in this example). By default, the object is restored at an expedited speed.
         Tier: obs.enums.RestoreTierExpedited
       };
       // Restore the Cold object.
       const result = await obsClient.restoreObject(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Restore object(%s) under the bucket(%s) successful!", params.Key, params.Bucket);
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

   restoreObject();

.. caution::

   To prolong the validity period of the Cold data restored, you can repeatedly restore the data, but you will be billed for each restoration. After a second restore, the validity period of Standard object copies will be prolonged, and you need to pay for storing these copies during the prolonged period.
