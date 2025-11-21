:original_name: obs_29_0314.html

.. _obs_29_0314:

Obtaining the Storage Quota of a Bucket
=======================================

Function
--------

This API returns the storage quota (upper limit of the storage capacity) of a bucket. If the quota is 0, there is no upper limit on the bucket capacity.

Restrictions
------------

-  A bucket storage quota must be a non-negative integer expressed in bytes. The maximum value is 2\ :sup:`63` - 1.
-  A bucket owner with a frozen account in arrears is not allowed to query the bucket storage quota.
-  To obtain the storage quota of a bucket, you must be the bucket owner or have the required permission (**obs:bucket:GetBucketQuota** in IAM or **GetBucketQuota** in a bucket policy).

Method
------

.. code-block::

   ObsClient.getBucketQuota(params)

Request Parameters
------------------

.. table:: **Table 1** BucketRequestInput

   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                          |
   +=================+=================+====================+======================================================================================================================================================================================+
   | Bucket          | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Bucket name.                                                                                                                                                                         |
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

Responses
---------

.. table:: **Table 2** Responses

   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Type                                                                                      | Description                                                                          |
   +===========================================================================================+======================================================================================+
   | :ref:`Table 3 <obs_29_0314__table1722625714202>`                                          | **Explanation:**                                                                     |
   |                                                                                           |                                                                                      |
   | .. note::                                                                                 | Returned results. For details, see :ref:`Table 3 <obs_29_0314__table1722625714202>`. |
   |                                                                                           |                                                                                      |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. |                                                                                      |
   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_29_0314__table1722625714202:

.. table:: **Table 3** Response

   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                   |
   +=======================+=====================================================+===============================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_0314__table6176201212273>` | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 4 <obs_29_0314__table6176201212273>`. |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`Table 5 <obs_29_0314__table33959011>`         | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Results outputted for a successful call. For details, see :ref:`Table 5 <obs_29_0314__table33959011>`.                                                                        |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | **Restrictions**:                                                                                                                                                             |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | This parameter is not included if the value of **Status** is greater than 300.                                                                                                |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0314__table6176201212273:

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

.. _obs_29_0314__table33959011:

.. table:: **Table 5** GetBucketQuotaOutput

   +-----------------------+-----------------------+---------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                   |
   +=======================+=======================+===============================================================+
   | RequestId             | string                | **Explanation:**                                              |
   |                       |                       |                                                               |
   |                       |                       | Request ID returned by the OBS server                         |
   +-----------------------+-----------------------+---------------------------------------------------------------+
   | StorageQuota          | number                | **Explanation:**                                              |
   |                       |                       |                                                               |
   |                       |                       | Bucket quota.                                                 |
   |                       |                       |                                                               |
   |                       |                       | **Default value**:                                            |
   |                       |                       |                                                               |
   |                       |                       | **0**, indicating that there is no limit on the bucket quota. |
   +-----------------------+-----------------------+---------------------------------------------------------------+

Code Examples
-------------

You can call **ObsClient.getBucketQuota** to obtain the storage quota of a bucket. This example uses bucket **examplebucket**.

::

   // Import the OBS library.
   // Use npm to install the client.
   const ObsClient = require("esdk-obs-nodejs");
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');

   // Create an instance of ObsClient.
   const obsClient = new ObsClient({
     //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
     //Obtain an AK/SK pair on the management console.
     access_key_id: process.env.ACCESS_KEY_ID,
     secret_access_key: process.env.SECRET_ACCESS_KEY,
     // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
     // security_token: process.env.SECURITY_TOKEN,
     // Enter the endpoint of the region where the bucket is located.
     server: "https://your-endpoint"
   });

   async function getBucketQuota() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket"
       };
       // Obtain the bucket quota.
       const result = await obsClient.getBucketQuota(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Get bucket(%s)'s quota successful!", params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         console.log('StorageQuota: %s', result.InterfaceResult.StorageQuota);
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

   getBucketQuota();
