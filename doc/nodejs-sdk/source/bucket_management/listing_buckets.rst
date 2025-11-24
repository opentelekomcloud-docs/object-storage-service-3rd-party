:original_name: obs_29_0302.html

.. _obs_29_0302:

Listing Buckets
===============

Function
--------

OBS buckets are containers for storing objects you upload to OBS. This API returns a list of all buckets that meet the specified conditions in all regions of the current account. Returned buckets are listed in alphabetical order by bucket name.

Restrictions
------------

-  To list buckets, you must have the **obs:bucket:ListAllMyBuckets** permission.

Method
------

.. code-block::

   ObsClient.listBuckets(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------+--------------------+---------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                       |
   +=================+=================+====================+===================================================+
   | QueryLocation   | boolean         | No                 | **Explanation:**                                  |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | Whether to query the bucket location              |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | **Restrictions**:                                 |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | None                                              |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | **Value range**:                                  |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | -  **true**: The bucket location is queried.      |
   |                 |                 |                    | -  **false**: The bucket location is not queried. |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | **Default value**:                                |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | false                                             |
   +-----------------+-----------------+--------------------+---------------------------------------------------+

.. table:: **Table 2** BucketType

   ======== ==============================
   Constant Description
   ======== ==============================
   OBJECT   An object bucket
   POSIX    A parallel file system (POSIX)
   ======== ==============================

Responses
---------

.. table:: **Table 3** Responses

   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Type                                                                                      | Description                                                                          |
   +===========================================================================================+======================================================================================+
   | :ref:`Table 4 <obs_29_0302__table1722625714202>`                                          | **Explanation:**                                                                     |
   |                                                                                           |                                                                                      |
   | .. note::                                                                                 | Returned results. For details, see :ref:`Table 4 <obs_29_0302__table1722625714202>`. |
   |                                                                                           |                                                                                      |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. |                                                                                      |
   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_29_0302__table1722625714202:

.. table:: **Table 4** Response

   +-----------------------+------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                       | Description                                                                                                                                                                   |
   +=======================+============================================================+===============================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_0302__table6176201212273>`        | **Explanation:**                                                                                                                                                              |
   |                       |                                                            |                                                                                                                                                                               |
   |                       |                                                            | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 5 <obs_29_0302__table6176201212273>`. |
   +-----------------------+------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`ListBucketsOutput <obs_29_0302__table2078171205919>` | **Explanation:**                                                                                                                                                              |
   |                       |                                                            |                                                                                                                                                                               |
   |                       |                                                            | Results outputted for a successful call. For details, see :ref:`Table 6 <obs_29_0302__table2078171205919>`.                                                                   |
   |                       |                                                            |                                                                                                                                                                               |
   |                       |                                                            | **Restrictions:**                                                                                                                                                             |
   |                       |                                                            |                                                                                                                                                                               |
   |                       |                                                            | This parameter is not included if the value of **Status** is greater than 300.                                                                                                |
   +-----------------------+------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0302__table6176201212273:

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

.. _obs_29_0302__table2078171205919:

.. table:: **Table 6** ListBucketsOutput

   +-----------------------+------------------------------------------------------+--------------------------------------------------------+
   | Parameter             | Type                                                 | Description                                            |
   +=======================+======================================================+========================================================+
   | RequestId             | string                                               | **Explanation:**                                       |
   |                       |                                                      |                                                        |
   |                       |                                                      | Request ID returned by the OBS server                  |
   |                       |                                                      |                                                        |
   |                       |                                                      | **Default value**:                                     |
   |                       |                                                      |                                                        |
   |                       |                                                      | None                                                   |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------+
   | Owner                 | :ref:`Owner <obs_29_0302__table57526325189>`         | **Explanation:**                                       |
   |                       |                                                      |                                                        |
   |                       |                                                      | Bucket owner                                           |
   |                       |                                                      |                                                        |
   |                       |                                                      | **Value range**:                                       |
   |                       |                                                      |                                                        |
   |                       |                                                      | See :ref:`Table 7 <obs_29_0302__table57526325189>`.    |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------+
   | Buckets               | :ref:`Bucket <obs_29_0302__table13702957151812>`\ [] | **Explanation:**                                       |
   |                       |                                                      |                                                        |
   |                       |                                                      | Bucket information list                                |
   |                       |                                                      |                                                        |
   |                       |                                                      | **Value range**:                                       |
   |                       |                                                      |                                                        |
   |                       |                                                      | See :ref:`Table 8 <obs_29_0302__table13702957151812>`. |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------+

.. _obs_29_0302__table57526325189:

.. table:: **Table 7** Owner

   +-----------------+-----------------+------------------------------------+---------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                 | Description                                                                                 |
   +=================+=================+====================================+=============================================================================================+
   | ID              | string          | Yes if used as a request parameter | **Explanation:**                                                                            |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | Account (domain) ID of the owner                                                            |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | **Value range**:                                                                            |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_29_1715>`. |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | **Default value**:                                                                          |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | None                                                                                        |
   +-----------------+-----------------+------------------------------------+---------------------------------------------------------------------------------------------+
   | DisplayName     | string          | No                                 | **Explanation:**                                                                            |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | Account name of the owner                                                                   |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | **Default value**:                                                                          |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | None                                                                                        |
   +-----------------+-----------------+------------------------------------+---------------------------------------------------------------------------------------------+

.. _obs_29_0302__table13702957151812:

.. table:: **Table 8** Bucket

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                                               |
   +=======================+=======================+===========================================================================================================================================================================================================================================================================================================================+
   | BucketName            | string                | **Explanation:**                                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | Bucket name.                                                                                                                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | **Restrictions**:                                                                                                                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                                                                                                          |
   |                       |                       | -  A bucket name:                                                                                                                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                                                                                              |
   |                       |                       |    -  Cannot be an IP address.                                                                                                                                                                                                                                                                                            |
   |                       |                       |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                                                                                                |
   |                       |                       |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                                                                                                           |
   |                       |                       |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CreationDate          | string                | **Explanation:**                                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | When the bucket was created.                                                                                                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Location              | string                | **Explanation:**                                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | Where a bucket is located.                                                                                                                                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | **Value range**:                                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | To learn about valid regions and endpoints, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__. An endpoint is the request address for calling an API. Endpoints vary depending on services and regions. To obtain the regions and endpoints, contact the enterprise administrator. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

You can call **ObsClient.listBuckets** to list buckets. This example lists all buckets.

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

   async function listBuckets() {
     try {
       const params = {
         // Specify whether to query the bucket location in the listing. The default value is false. true is used in this example.
         QueryLocation: true,
         // Specify a bucket type (object buckets in this example). If this parameter is not specified, object buckets and parallel file systems are listed by default.
         BucketType: "OBJECT",
       };
       // List buckets.
       const result = await obsClient.listBuckets(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("List buckets successful!", params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         console.log('Owner:');
         console.log('ID: %s', result.InterfaceResult.Owner.ID);
         console.log('Name: %s', result.InterfaceResult.Owner.Name);
         console.log('Buckets:');
         for (let i = 0; i < result.InterfaceResult.Buckets.length; i++) {
             const val = result.InterfaceResult.Buckets[i];
             console.log("Bucket[%d]-Name:%s,CreationDate:%s,Location: %s",
               i, val.BucketName, val.CreationDate, val.Location);
         };
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

   listBuckets();
