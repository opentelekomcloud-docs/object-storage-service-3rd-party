:original_name: obs_22_0811.html

.. _obs_22_0811:

Obtaining a Bucket Storage Quota
================================

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

ObsClient.getBucketQuota(bucketName, extensionHeaders)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +==================+=================+====================+===================================================================================================================================================================================+
   | bucketName       | str             | Yes                | **Explanation:**                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | Bucket name                                                                                                                                                                       |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | **Restrictions:**                                                                                                                                                                 |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                  |                 |                    | -  A bucket name:                                                                                                                                                                 |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                  |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                  |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                  |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                  |                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket properties comply with those set in the first creation request. |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | **Default value**:                                                                                                                                                                |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | None                                                                                                                                                                              |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | extensionHeaders | dict            | No                 | **Explanation:**                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | Extension headers                                                                                                                                                                 |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | **Value range**:                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | See :ref:`User-defined Headers <obs_22_1305>`.                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | **Default value**:                                                                                                                                                                |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | None                                                                                                                                                                              |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 2** List of returned results

   +-----------------------------------------------------+-----------------------------------+
   | Type                                                | Description                       |
   +=====================================================+===================================+
   | :ref:`GetResult <obs_22_0811__table20121844173311>` | **Explanation:**                  |
   |                                                     |                                   |
   |                                                     | SDK common results                |
   +-----------------------------------------------------+-----------------------------------+

.. _obs_22_0811__table20121844173311:

.. table:: **Table 3** GetResult

   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                      |
   +=======================+=======================+==================================================================================================================================================================================================================================================================================================+
   | status                | int                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | HTTP status code                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Value range**:                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | A status code is a group of digits ranging from 2\ *xx* (indicating successes) to 4\ *xx* or 5\ *xx* (indicating errors). It indicates the status of a response.                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | reason                | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Reason description.                                                                                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | errorCode             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Error code returned by the OBS server. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | errorMessage          | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Error message returned by the OBS server. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | requestId             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Request ID returned by the OBS server                                                                                                                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | indicator             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Error indicator returned by the OBS server.                                                                                                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hostId                | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Requested server ID. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource              | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Error source (a bucket or an object). If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                             |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | header                | list                  | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Response header list, composed of tuples. Each tuple consists of two elements, respectively corresponding to the key and value of a response header.                                                                                                                                             |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | body                  | object                | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Result content returned after the operation is successful. If the value of **status** is larger than **300**, the value of **body** is null. The value varies with the API being called. For details, see :ref:`Bucket-Related APIs <obs_22_0800>` and :ref:`Object-Related APIs <obs_22_0900>`. |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 4** GetResult.body

   +---------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | GetResult.body Type                                           | Description                                                                         |
   +===============================================================+=====================================================================================+
   | :ref:`GetBucketQuotaResponse <obs_22_0811__table61312171198>` | **Explanation:**                                                                    |
   |                                                               |                                                                                     |
   |                                                               | Response result of the request for obtaining the storage capacity quota of a bucket |
   +---------------------------------------------------------------+-------------------------------------------------------------------------------------+

.. _obs_22_0811__table61312171198:

.. table:: **Table 5** GetBucketQuotaResponse

   +-----------------------+-----------------------+---------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                   |
   +=======================+=======================+===============================================================+
   | quota                 | int                   | **Explanation:**                                              |
   |                       |                       |                                                               |
   |                       |                       | Bucket quota                                                  |
   |                       |                       |                                                               |
   |                       |                       | **Value range**:                                              |
   |                       |                       |                                                               |
   |                       |                       | An integer greater than or equal to 0, in bytes               |
   |                       |                       |                                                               |
   |                       |                       | **Default value**:                                            |
   |                       |                       |                                                               |
   |                       |                       | **0**, indicating that there is no limit on the bucket quota. |
   +-----------------------+-----------------------+---------------------------------------------------------------+

Code Examples
-------------

This example returns the quota of bucket **examplebucket**.

::

   from obs import ObsClient
   import os
   import traceback

   # Obtain an AK and SK pair using environment variables or import the AK and SK pair in other ways. Using hard coding may result in leakage.
   # Obtain an AK and SK pair on the management console.
   ak = os.getenv("AccessKeyID")
   sk = os.getenv("SecretAccessKey")
   # (Optional) If you use a temporary AK and SK pair and a security token to access OBS, obtain them from environment variables.
   # security_token = os.getenv("SecurityToken")
   # Set server to the endpoint of the region where the bucket is located.
   server = "https://your-endpoint"

   # Create an obsClient instance.
   # If you use a temporary AK and SK pair and a security token to access OBS, you must specify security_token when creating an instance.
   obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)
   try:
       bucketName="examplebucket"
       # Obtain the bucket quota.
       resp = obsClient.getBucketQuota(bucketName)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Get Bucket Quota Succeeded')
           print('requestId:', resp.requestId)
           print('quota:', resp.body.quota)
       else:
           print('Get Bucket Quota Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Get Bucket Quota Failed')
       print(traceback.format_exc())
