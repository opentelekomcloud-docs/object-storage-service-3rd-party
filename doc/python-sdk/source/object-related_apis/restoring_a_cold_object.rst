:original_name: obs_22_0924.html

.. _obs_22_0924:

Restoring a Cold Object
=======================

Function
--------

To obtain the contents of an object in the Cold storage class, you need to restore the object first and then you can download it. After an object is restored, a copy of the object is saved in the Standard storage class. By doing so, the object in the Cold storage class and its copy in the Standard storage class co-exist in the bucket. The copy will be automatically deleted once its retention period expires.

This API is used to restore Cold objects in a specified bucket.

Restrictions
------------

-  To restore a Cold object, you must be the bucket owner or have the required permission (**obs:object:RestoreObject** in IAM or **RestoreObject** in a bucket policy.)
-  To prolong the validity period of the Cold data restored, you can repeatedly restore the data, but you will be billed for each restore. After a second restore, the validity period of Standard object copies will be prolonged, and you need to pay for storing these copies during the prolonged period.

Method
------

.. code-block::

   ObsClient.restoreObject(bucketName, objectKey, days, tier, versionId, extensionHeaders)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                                |
   +==================+=================+====================+============================================================================================================================================================================================+
   | bucketName       | str             | Yes                | **Explanation:**                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | Bucket name                                                                                                                                                                                |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Restrictions:**                                                                                                                                                                          |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                           |
   |                  |                 |                    | -  A bucket name:                                                                                                                                                                          |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                               |
   |                  |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                                |
   |                  |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                 |
   |                  |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                            |
   |                  |                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                    |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket properties comply with those set in the first creation request.          |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Default value**:                                                                                                                                                                         |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | None                                                                                                                                                                                       |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey        | str             | Yes                | **Explanation:**                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                                      |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Value range**:                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                                                              |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Default value**:                                                                                                                                                                         |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | None                                                                                                                                                                                       |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | days             | int             | Yes                | **Explanation:**                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | After an object is restored, a Standard copy of it is generated. This parameter specifies how long the Standard copy can be retained, that is, the validity period of the restored object. |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Value range**:                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | The value ranges from 1 to 30, in days.                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Default value**:                                                                                                                                                                         |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | None                                                                                                                                                                                       |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | tier             | str             | No                 | **Explanation:**                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | Retrieval speed tiers. You can select a suitable tier based on your requirements for retrieval speed.                                                                                      |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Value range**:                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | See :ref:`Table 2 <obs_22_0924__table1427811514514>`.                                                                                                                                      |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Default value**:                                                                                                                                                                         |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | Standard                                                                                                                                                                                   |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | versionId        | str             | No                 | **Explanation:**                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | Version ID of the Cold object to be restored                                                                                                                                               |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Default value**:                                                                                                                                                                         |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | None. If this parameter is left blank, the latest version of the object is specified.                                                                                                      |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | extensionHeaders | dict            | No                 | **Explanation:**                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | Extension headers.                                                                                                                                                                         |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Value range**:                                                                                                                                                                           |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | See :ref:`User-defined Headers <obs_22_1305>`.                                                                                                                                             |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | **Default value**:                                                                                                                                                                         |
   |                  |                 |                    |                                                                                                                                                                                            |
   |                  |                 |                    | None                                                                                                                                                                                       |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_22_0924__table1427811514514:

.. table:: **Table 2** RestoreTier

   +-----------+----------------------------------------------------------------------+
   | Constant  | Description                                                          |
   +===========+======================================================================+
   | Expedited | Objects can be restored at an expedited speed within 1 to 5 minutes. |
   +-----------+----------------------------------------------------------------------+
   | Standard  | Objects can be restored at a standard speed within 3 to 5 hours.     |
   +-----------+----------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** List of returned results

   +---------------------------------------------------+-----------------------------------+
   | Type                                              | Description                       |
   +===================================================+===================================+
   | :ref:`GetResult <obs_22_0924__table133284282414>` | **Explanation:**                  |
   |                                                   |                                   |
   |                                                   | SDK common results                |
   +---------------------------------------------------+-----------------------------------+

.. note::

   If **GetResult.status** is **202**, the object is being restored. If **GetResult.status** is **200**, the object has been restored.

.. _obs_22_0924__table133284282414:

.. table:: **Table 4** GetResult

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

Code Examples
-------------

This example restores the Cold object **objectname**.

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
       bucketName = "examplebucket"
       objectKey = "objectname"
       # Specify how long the restored object will be retained, in days. The value ranges from 1 to 30.
       days = 1
       # Specify the restoration speed. Options: Expedited or Standard
       tier = "Expedited"
       # Restore the Cold object.
       resp = obsClient.restoreObject(bucketName, objectKey, days, tier)

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Restore Object Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Restore Object Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Restore Object Failed')
       print(traceback.format_exc())
