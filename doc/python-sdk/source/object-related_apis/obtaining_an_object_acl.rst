:original_name: obs_22_0923.html

.. _obs_22_0923:

Obtaining an Object ACL
=======================

Function
--------

Access control lists (ACLs) allow resource owners to grant other accounts the permissions to access resources. By default, only the resource owner has full control over resources when a bucket or object is created. That is, the bucket creator has full control over the bucket, and the object uploader has full control over the object. Other accounts do not have the permissions to access resources. If resource owners want to grant other accounts the read and write permissions on resources, they can use ACLs. ACLs grant permissions to accounts. After an account is granted permissions, both the account and its IAM users can access the resources.

This API obtains the ACL of an object in a specified bucket.

Restrictions
------------

-  To obtain an object ACL, you must be the bucket owner or have the required permission (**obs:object:GetObjectAcl** in IAM or **GetObjectAcl** in a bucket policy).
-  To call this API, you must have the read permission on the ACL of the object.

Method
------

.. code-block::

   ObsClient.getObjectAcl(bucketName, objectKey, versionId, extensionHeaders)

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
   | objectKey        | str             | Yes                | **Explanation:**                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                             |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | **Value range**:                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | **Default value**:                                                                                                                                                                |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | None                                                                                                                                                                              |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | versionId        | str             | No                 | **Explanation:**                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | Object version ID, for example, **G001117FCE89978B0000401205D5DC9A**                                                                                                              |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | **Value range**:                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | The value must contain 32 characters.                                                                                                                                             |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | **Default value**:                                                                                                                                                                |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | None                                                                                                                                                                              |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | extensionHeaders | dict            | No                 | **Explanation:**                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                   |
   |                  |                 |                    | Extension headers.                                                                                                                                                                |
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

   +---------------------------------------------------+-----------------------------------+
   | Type                                              | Description                       |
   +===================================================+===================================+
   | :ref:`GetResult <obs_22_0923__table133284282414>` | **Explanation:**                  |
   |                                                   |                                   |
   |                                                   | SDK common results                |
   +---------------------------------------------------+-----------------------------------+

.. _obs_22_0923__table133284282414:

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

   +----------------------------------------------------------------+----------------------------------------------------------------------------------------------+
   | GetResult.body Type                                            | Description                                                                                  |
   +================================================================+==============================================================================================+
   | :ref:`ACL <obs_22_0923__en-us_topic_0142814672_table14455523>` | **Explanation:**                                                                             |
   |                                                                |                                                                                              |
   |                                                                | Object ACL. For details, see :ref:`ACL <obs_22_0923__en-us_topic_0142814672_table14455523>`. |
   |                                                                |                                                                                              |
   |                                                                | **Default value**:                                                                           |
   |                                                                |                                                                                              |
   |                                                                | None                                                                                         |
   +----------------------------------------------------------------+----------------------------------------------------------------------------------------------+

.. _obs_22_0923__en-us_topic_0142814672_table14455523:

.. table:: **Table 5** ACL

   +-----------------+--------------------------------------------------------------------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                                     | Mandatory (Yes/No)                 | Description                                                                                                                    |
   +=================+==========================================================================+====================================+================================================================================================================================+
   | owner           | :ref:`Owner <obs_22_0923__table820982095914>`                            | Yes if used as a request parameter | **Explanation:**                                                                                                               |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | Bucket owner. For details, see :ref:`Table 6 <obs_22_0923__table820982095914>`.                                                |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | **Restrictions:**                                                                                                              |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | **owner** and **grants** must be used together and they cannot be used with **ACL**.                                           |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | **Default value**:                                                                                                             |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | None                                                                                                                           |
   +-----------------+--------------------------------------------------------------------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | grants          | list of :ref:`Grant <obs_22_0923__en-us_topic_0142814620_table14455523>` | Yes if used as a request parameter | **Explanation:**                                                                                                               |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | List of grantees' permission information. For details, see :ref:`Table 7 <obs_22_0923__en-us_topic_0142814620_table14455523>`. |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | **Default value**:                                                                                                             |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | None                                                                                                                           |
   +-----------------+--------------------------------------------------------------------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | delivered       | bool                                                                     | No if used as a request parameter  | **Explanation:**                                                                                                               |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | Whether the bucket ACL is applied to all objects in the bucket                                                                 |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | **Value range**:                                                                                                               |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | **True**: The bucket ACL is applied to all objects in the bucket.                                                              |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | **False**: The bucket ACL is not applied to all objects in the bucket.                                                         |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | **Default value**:                                                                                                             |
   |                 |                                                                          |                                    |                                                                                                                                |
   |                 |                                                                          |                                    | False                                                                                                                          |
   +-----------------+--------------------------------------------------------------------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+

.. _obs_22_0923__table820982095914:

.. table:: **Table 6** Owner

   +-----------------+-----------------+------------------------------------+------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                 | Description                                                                                    |
   +=================+=================+====================================+================================================================================================+
   | owner_id        | str             | Yes if used as a request parameter | **Explanation:**                                                                               |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | Account (domain) ID of the owner                                                               |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | **Value range**:                                                                               |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | To obtain the account ID, see :ref:`How Do I Get My Account ID and IAM User ID? <obs_22_1703>` |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | **Default value**:                                                                             |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | None                                                                                           |
   +-----------------+-----------------+------------------------------------+------------------------------------------------------------------------------------------------+
   | owner_name      | str             | No if used as a request parameter  | **Explanation:**                                                                               |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | Account name of the owner                                                                      |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | **Value range**:                                                                               |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | To obtain the account ID, see :ref:`How Do I Get My Account ID and IAM User ID? <obs_22_1703>` |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | **Default value**:                                                                             |
   |                 |                 |                                    |                                                                                                |
   |                 |                 |                                    | None                                                                                           |
   +-----------------+-----------------+------------------------------------+------------------------------------------------------------------------------------------------+

.. _obs_22_0923__en-us_topic_0142814620_table14455523:

.. table:: **Table 7** Grant

   +-----------------+-------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------+
   | Parameter       | Type                                            | Mandatory (Yes/No)                 | Description                                                                            |
   +=================+=================================================+====================================+========================================================================================+
   | grantee         | :ref:`Grantee <obs_22_0923__table111151512507>` | Yes if used as a request parameter | **Explanation:**                                                                       |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | Grantee information. For details, see :ref:`Table 9 <obs_22_0923__table111151512507>`. |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | **Default value**:                                                                     |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | None                                                                                   |
   +-----------------+-------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------+
   | permission      | str                                             | Yes if used as a request parameter | **Explanation:**                                                                       |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | Granted permission                                                                     |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | **Value range**:                                                                       |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | See :ref:`Table 8 <obs_22_0923__table1867520815467>`.                                  |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | **Default value**:                                                                     |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | None                                                                                   |
   +-----------------+-------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------+
   | delivered       | bool                                            | No if used as a request parameter  | **Explanation:**                                                                       |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | Whether the bucket ACL is applied to all objects in the bucket                         |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | **Value range**:                                                                       |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | **True**: The bucket ACL is applied to all objects in the bucket.                      |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | **False**: The bucket ACL is not applied to all objects in the bucket.                 |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | **Default value**:                                                                     |
   |                 |                                                 |                                    |                                                                                        |
   |                 |                                                 |                                    | False                                                                                  |
   +-----------------+-------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------+

.. _obs_22_0923__table1867520815467:

.. table:: **Table 8** Permission

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Constant                          | Description                                                                                                                                        |
   +===================================+====================================================================================================================================================+
   | READ                              | Read permission                                                                                                                                    |
   |                                   |                                                                                                                                                    |
   |                                   | A grantee with this permission for a bucket can obtain the list of objects, multipart uploads, bucket metadata, and object versions in the bucket. |
   |                                   |                                                                                                                                                    |
   |                                   | A grantee with this permission for an object can obtain the object content and metadata.                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | WRITE                             | Write permission                                                                                                                                   |
   |                                   |                                                                                                                                                    |
   |                                   | A grantee with this permission for a bucket can upload, overwrite, and delete any object or part in the bucket.                                    |
   |                                   |                                                                                                                                                    |
   |                                   | Such permission for an object is not applicable.                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | READ_ACP                          | Permission to read ACL configurations                                                                                                              |
   |                                   |                                                                                                                                                    |
   |                                   | A grantee with this permission can obtain the ACL of a bucket or object.                                                                           |
   |                                   |                                                                                                                                                    |
   |                                   | A bucket or object owner has this permission for the bucket or object permanently.                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | WRITE_ACP                         | Permission to modify ACL configurations                                                                                                            |
   |                                   |                                                                                                                                                    |
   |                                   | A grantee with this permission can update the ACL of a bucket or object.                                                                           |
   |                                   |                                                                                                                                                    |
   |                                   | A bucket or object owner has this permission for the bucket or object permanently.                                                                 |
   |                                   |                                                                                                                                                    |
   |                                   | A grantee with this permission can modify the ACL, thus obtaining full access permissions.                                                         |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | FULL_CONTROL                      | Full control access, including read and write permissions for a bucket and its ACL, or for an object and its ACL.                                  |
   |                                   |                                                                                                                                                    |
   |                                   | A grantee with this permission for a bucket has **READ**, **WRITE**, **READ_ACP**, and **WRITE_ACP** permissions for the bucket.                   |
   |                                   |                                                                                                                                                    |
   |                                   | A grantee with this permission for an object has **READ**, **READ_ACP**, and **WRITE_ACP** permissions for the object.                             |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_22_0923__table111151512507:

.. table:: **Table 9** Grantee

   +-----------------+-----------------+--------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                                                                   | Description                                                         |
   +=================+=================+======================================================================================+=====================================================================+
   | grantee_id      | str             | Yes if the parameter is used as a request parameter and **group** is left blank      | **Explanation:**                                                    |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | Account (domain) ID of the grantee                                  |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | **Value range**:                                                    |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | **Default value**:                                                  |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | None                                                                |
   +-----------------+-----------------+--------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | grantee_name    | str             | No if used as a request parameter                                                    | **Explanation:**                                                    |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | Account name of the grantee                                         |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | **Restrictions:**                                                   |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | -  Cannot contain full-width characters.                            |
   |                 |                 |                                                                                      | -  Starts with a letter.                                            |
   |                 |                 |                                                                                      | -  Contains 6 to 32 characters.                                     |
   |                 |                 |                                                                                      | -  Contains only letters, digits, hyphens (-), and underscores (_). |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | **Default value**:                                                  |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | None                                                                |
   +-----------------+-----------------+--------------------------------------------------------------------------------------+---------------------------------------------------------------------+
   | group           | str             | Yes if the parameter is used as a request parameter and **grantee_id** is left blank | **Explanation:**                                                    |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | Authorized user group                                               |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | **Value range**:                                                    |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | See :ref:`Table 10 <obs_22_0923__table4995949171>`.                 |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | **Default value**:                                                  |
   |                 |                 |                                                                                      |                                                                     |
   |                 |                 |                                                                                      | None                                                                |
   +-----------------+-----------------+--------------------------------------------------------------------------------------+---------------------------------------------------------------------+

.. _obs_22_0923__table4995949171:

.. table:: **Table 10** Group

   =================== ================================================
   Constant            Description
   =================== ================================================
   ALL_USERS           All users
   AUTHENTICATED_USERS Authorized users. This constant is deprecated.
   LOG_DELIVERY        Log delivery group. This constant is deprecated.
   =================== ================================================

Code Examples
-------------

This example returns the object ACL information of object **objectname**.

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
       # Obtain the ACL of an object in a specified bucket.
       resp = obsClient.getObjectAcl(bucketName, objectKey)

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Get Object Acl Succeeded')
           print('requestId:', resp.requestId)
           print('owner_id:', resp.body.owner.owner_id)
           print('owner_name:', resp.body.owner.owner_name)

           index = 1
           for grant in resp.body.grants:
               print('grant [' + str(index) + ']')
               print('grantee_id:', grant.grantee.grantee_id)
               print('grantee_name:', grant.grantee.grantee_name)
               print('group:', grant.grantee.group)
               print('permission:', grant.permission)
               index += 1
       else:
           print('Get Object Acl Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Get Object Acl Failed')
       print(traceback.format_exc())
