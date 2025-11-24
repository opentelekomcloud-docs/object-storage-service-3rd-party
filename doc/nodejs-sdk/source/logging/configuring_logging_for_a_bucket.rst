:original_name: obs_29_1102.html

.. _obs_29_1102:

Configuring Logging for a Bucket
================================

.. note::

   A bucket in the Warm or Cold storage class cannot be used as a log target bucket.

Function
--------

This API enables logging for a bucket (source) and configures another bucket (target) to store the log files. When a bucket is created, logging is not enabled by default. You can call this API to enable logging for the bucket. With logging enabled, a log message is generated for each operation on the bucket. Multiple log messages are packed into a file. The target bucket for storing log files must be specified when logging is enabled. It can be the bucket logging is enabled for, or any other bucket you have access to. If you specify another bucket for storing logs, the bucket must be in the same region as the logged bucket. You can also specify access permissions and name prefixes for log files.

Restrictions
------------

-  OBS creates log files and uploads them to the bucket. Before enabling logging for a bucket, you need to create an IAM agency to delegate OBS to upload log files to the specified bucket. For details about how to create an agency, see .
-  To configure logging for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketLogging** in IAM or **PutBucketLogging** in a bucket policy).
-  The source bucket and target bucket must be in the same region.

Method
------

.. code-block::

   ObsClient.setBucketLogging(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-------------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                  | Mandatory (Yes/No)                                                 | Description                                                                                                                                                                                                                                                                        |
   +=================+=======================================================+====================================================================+====================================================================================================================================================================================================================================================================================+
   | Bucket          | string                                                | Yes                                                                | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | Bucket name                                                                                                                                                                                                                                                                        |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | **Restrictions**:                                                                                                                                                                                                                                                                  |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                                                                   |
   |                 |                                                       |                                                                    | -  A bucket name:                                                                                                                                                                                                                                                                  |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                                                       |
   |                 |                                                       |                                                                    |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                                                        |
   |                 |                                                       |                                                                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                                                         |
   |                 |                                                       |                                                                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                                                          |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request.                                                                                               |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | **Value range**:                                                                                                                                                                                                                                                                   |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | The value can contain 3 to 63 characters.                                                                                                                                                                                                                                          |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------+-------------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Agency          | string                                                | Yes if used in a request for enabling bucket logging               | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | Name of the IAM agency created by the owner of the target bucket for OBS.                                                                                                                                                                                                          |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | **Restrictions**:                                                                                                                                                                                                                                                                  |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | By default, the IAM agency only requires the **PutObject** permission to upload logs to the target bucket. If default encryption is enabled for the target bucket, the agency also requires the **KMS Administrator** permission in the region where the target bucket is located. |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | **Value range**:                                                                                                                                                                                                                                                                   |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | You can select an existing IAM agency or create one.                                                                                                                                                                                                                               |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------+-------------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | LoggingEnabled  | :ref:`LoggingEnabled <obs_29_1102__table74814341711>` | Yes if you enable logging for the bucket                           | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       | Do not set this parameter when you disable logging for the bucket. | Logging configuration information. If this parameter is not set, bucket logging is disabled by default.                                                                                                                                                                            |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | **Restrictions**:                                                                                                                                                                                                                                                                  |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | None                                                                                                                                                                                                                                                                               |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | **Value range**:                                                                                                                                                                                                                                                                   |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | See :ref:`LoggingEnabled <obs_29_1102__table74814341711>`.                                                                                                                                                                                                                         |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                 |                                                       |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                       |                                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------+-------------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1102__table74814341711:

.. table:: **Table 2** LoggingEnabled

   +-----------------+------------------------------------------------+--------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                           | Mandatory (Yes/No)                                                 | Description                                                                                                                                                                          |
   +=================+================================================+====================================================================+======================================================================================================================================================================================+
   | TargetBucket    | string                                         | Yes if you enable logging for the bucket                           | **Explanation:**                                                                                                                                                                     |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                | Do not set this parameter when you disable logging for the bucket. | Name of the bucket for storing log files.                                                                                                                                            |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | -  This bucket must be in the same region as the bucket with logging enabled.                                                                                                        |
   |                 |                                                |                                                                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                     |
   |                 |                                                |                                                                    | -  A bucket name:                                                                                                                                                                    |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                         |
   |                 |                                                |                                                                    |    -  Cannot be formatted as an IP address.                                                                                                                                          |
   |                 |                                                |                                                                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                           |
   |                 |                                                |                                                                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                      |
   |                 |                                                |                                                                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                            |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | The value can contain 3 to 63 characters.                                                                                                                                            |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | None                                                                                                                                                                                 |
   +-----------------+------------------------------------------------+--------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetPrefix    | string                                         | Yes if you enable logging for the bucket                           | **Explanation:**                                                                                                                                                                     |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                | Do not set this parameter when you disable logging for the bucket. | Name prefix for log files stored in the target bucket.                                                                                                                               |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | None                                                                                                                                                                                 |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | The value can contain 1 to 1,024 characters.                                                                                                                                         |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | None                                                                                                                                                                                 |
   +-----------------+------------------------------------------------+--------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetGrants    | :ref:`Grant <obs_29_1102__table1764402511517>` | No                                                                 | **Explanation:**                                                                                                                                                                     |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | Permission information list of grantees, which defines grantees and their permissions for log files.                                                                                 |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | None                                                                                                                                                                                 |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | See :ref:`Grant <obs_29_1102__table1764402511517>`.                                                                                                                                  |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                |                                                                    |                                                                                                                                                                                      |
   |                 |                                                |                                                                    | None                                                                                                                                                                                 |
   +-----------------+------------------------------------------------+--------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1102__table1764402511517:

.. table:: **Table 3** Grant

   +-----------------+----------------------------------------------------+--------------------+---------------------------------------------------------+
   | Parameter       | Type                                               | Mandatory (Yes/No) | Description                                             |
   +=================+====================================================+====================+=========================================================+
   | Grantee         | :ref:`Grantee <obs_29_1102__table94488481611>`     | Yes                | **Explanation:**                                        |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | Grantees and permissions                                |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | **Restrictions**:                                       |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | None                                                    |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | **Value range**:                                        |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | See :ref:`Grantee <obs_29_1102__table94488481611>`.     |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | **Default value**:                                      |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | None                                                    |
   +-----------------+----------------------------------------------------+--------------------+---------------------------------------------------------+
   | Permission      | :ref:`PermissionType <obs_29_1102__table60165497>` | Yes                | **Explanation:**                                        |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | Granted permission                                      |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | **Restrictions**:                                       |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | None                                                    |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | **Value range**:                                        |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | See :ref:`PermissionType <obs_29_1102__table60165497>`. |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | **Default value**:                                      |
   |                 |                                                    |                    |                                                         |
   |                 |                                                    |                    | None                                                    |
   +-----------------+----------------------------------------------------+--------------------+---------------------------------------------------------+

.. _obs_29_1102__table94488481611:

.. table:: **Table 4** Grantee

   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | Parameter       | Type                                                   | Mandatory (Yes/No)                                                                  | Description                                                                        |
   +=================+========================================================+=====================================================================================+====================================================================================+
   | Type            | :ref:`GranteeType <obs_29_1102__table531313065315>`    | Yes if used as a request parameter                                                  | **Explanation:**                                                                   |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | Grantee type                                                                       |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Restrictions**:                                                                  |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | None                                                                               |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Value range**:                                                                   |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | See :ref:`Table 5 <obs_29_1102__table531313065315>`.                               |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Default value**:                                                                 |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | None                                                                               |
   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | ID              | string                                                 | Yes if this parameter is used as a request parameter and **Type** is set to a user  | **Explanation:**                                                                   |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | Account (domain) ID of the grantee.                                                |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Restrictions**:                                                                  |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | None                                                                               |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Default value**:                                                                 |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | None                                                                               |
   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | Name            | string                                                 | No if used as a request parameter                                                   | **Explanation:**                                                                   |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | Account name of the grantee.                                                       |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Restrictions**:                                                                  |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | -  The account name starts with a letter.                                          |
   |                 |                                                        |                                                                                     | -  The account name contains 6 to 32 characters.                                   |
   |                 |                                                        |                                                                                     | -  The account name only allows letters, digits, hyphens (-), and underscores (_). |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Value range**:                                                                   |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | None                                                                               |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Default value**:                                                                 |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | None                                                                               |
   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+------------------------------------------------------------------------------------+
   | URI             | :ref:`GroupUriType <obs_29_1102__table84401320145418>` | Yes if this parameter is used as a request parameter and **Type** is set to a group | **Explanation:**                                                                   |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | Authorized user group                                                              |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Restrictions**:                                                                  |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | None                                                                               |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Value range**:                                                                   |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | See :ref:`Table 6 <obs_29_1102__table84401320145418>`.                             |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | **Default value**:                                                                 |
   |                 |                                                        |                                                                                     |                                                                                    |
   |                 |                                                        |                                                                                     | None                                                                               |
   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+------------------------------------------------------------------------------------+

.. _obs_29_1102__table531313065315:

.. table:: **Table 5** GranteeType

   ============ ============= =======================================
   Constant     Default Value Description
   ============ ============= =======================================
   GranteeGroup Group         Grants permissions to user groups.
   GranteeUser  CanonicalUser Grants permissions to individual users.
   ============ ============= =======================================

.. _obs_29_1102__table84401320145418:

.. table:: **Table 6** GroupUriType

   +-------------------------+--------------------+--------------------------------------------------+
   | Constant                | Default Value      | Description                                      |
   +=========================+====================+==================================================+
   | GroupAllUsers           | AllUsers           | All users                                        |
   +-------------------------+--------------------+--------------------------------------------------+
   | GroupAuthenticatedUsers | AuthenticatedUsers | Authorized users. This constant is deprecated.   |
   +-------------------------+--------------------+--------------------------------------------------+
   | GroupLogDelivery        | LogDelivery        | Log delivery group. This constant is deprecated. |
   +-------------------------+--------------------+--------------------------------------------------+

.. _obs_29_1102__table60165497:

.. table:: **Table 7** PermissionType

   +---------------------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Constant                              | Default Value         | Description                                                                                                                                                            |
   +=======================================+=======================+========================================================================================================================================================================+
   | ObsClient.enums.PermissionRead        | READ                  | A grantee with this permission for a bucket can obtain the list of objects, multipart uploads, bucket metadata, and object versions in the bucket.                     |
   |                                       |                       |                                                                                                                                                                        |
   |                                       |                       | A grantee with this permission for an object can obtain the object content and metadata.                                                                               |
   +---------------------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.PermissionWrite       | WRITE                 | A grantee with this permission for a bucket can upload, overwrite, and delete any object or part in the bucket.                                                        |
   |                                       |                       |                                                                                                                                                                        |
   |                                       |                       | This permission is not applicable to objects.                                                                                                                          |
   +---------------------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.PermissionReadAcp     | READ_ACP              | A grantee with this permission can obtain the ACL of a bucket or object.                                                                                               |
   |                                       |                       |                                                                                                                                                                        |
   |                                       |                       | A bucket or object owner has this permission for their bucket or object by default.                                                                                    |
   +---------------------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.PermissionWriteAcp    | WRITE_ACP             | A grantee with this permission can update the ACL of a bucket or object.                                                                                               |
   |                                       |                       |                                                                                                                                                                        |
   |                                       |                       | A bucket or object owner has this permission for their bucket or object by default.                                                                                    |
   |                                       |                       |                                                                                                                                                                        |
   |                                       |                       | This permission allows the grantee to change the access control policies, meaning the grantee has full control over a bucket or object.                                |
   +---------------------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.PermissionFullControl | FULL_CONTROL          | A grantee with this permission for a bucket has **PermissionRead**, **PermissionWrite**, **PermissionReadAcp**, and **PermissionWriteAcp** permissions for the bucket. |
   |                                       |                       |                                                                                                                                                                        |
   |                                       |                       | A grantee with this permission for an object has **PermissionRead**, **PermissionReadAcp**, and **PermissionWriteAcp** permissions for the object.                     |
   +---------------------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 8** Responses

   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Type                                                                                      | Description                                                                          |
   +===========================================================================================+======================================================================================+
   | :ref:`Table 9 <obs_29_1102__table1722625714202>`                                          | **Explanation:**                                                                     |
   |                                                                                           |                                                                                      |
   | .. note::                                                                                 | Returned results. For details, see :ref:`Table 9 <obs_29_1102__table1722625714202>`. |
   |                                                                                           |                                                                                      |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. |                                                                                      |
   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_29_1102__table1722625714202:

.. table:: **Table 9** Response

   +-----------------------+-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                    |
   +=======================+=====================================================+================================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_1102__table6176201212273>` | **Explanation:**                                                                                                                                                               |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 10 <obs_29_1102__table6176201212273>`. |
   +-----------------------+-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`Table 11 <obs_29_1102__table33959011>`        | **Explanation:**                                                                                                                                                               |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | Results outputted for a successful call. For details, see :ref:`Table 11 <obs_29_1102__table33959011>`.                                                                        |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | **Restrictions:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | This parameter is not included if the value of **Status** is greater than 300.                                                                                                 |
   +-----------------------+-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1102__table6176201212273:

.. table:: **Table 10** ICommonMsg

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

.. _obs_29_1102__table33959011:

.. table:: **Table 11** BaseResponseOutput

   +-----------------------+-----------------------+---------------------------------------+
   | Parameter             | Type                  | Description                           |
   +=======================+=======================+=======================================+
   | RequestId             | string                | **Explanation:**                      |
   |                       |                       |                                       |
   |                       |                       | Request ID returned by the OBS server |
   +-----------------------+-----------------------+---------------------------------------+

Code Examples: Enabling Bucket Logging
--------------------------------------

This example configures logging for bucket **examplebucket**.

::

   // Import the OBS library.
   // Use npm to install the client.
   const ObsClient = require("esdk-obs-nodejs");
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');

   // Create an instance of ObsClient.
   const obsClient = new ObsClient({
     //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
     // Obtain an AK/SK pair on the management console.
     access_key_id: process.env.ACCESS_KEY_ID,
     secret_access_key: process.env.SECRET_ACCESS_KEY,
     // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
     // security_token: process.env.SECURITY_TOKEN,
     // Enter the endpoint of the region where the bucket is located.
     server: "https://your-endpoint"
   });

   async function setBucketLogging() {
       try {
           const params = {
               // Specify the bucket name.
               Bucket: "examplebucket",
               // Specify an agency name (obs_test_agency in this example).
               Agency: 'obs_test_agency',
               LoggingEnabled: {
                   // Specify a bucket (TargetBucketname in this example) for storing generated log files.
                   TargetBucket: 'TargetBucketname',
                   // Specify a prefix (TargetPrefixtest/ in this example) for log files to be generated.
                   TargetPrefix: 'TargetPrefixtest/',
                   // Specify the grantee permissions.
                   TargetGrants: [
                       // Grant the read permission to a specific user. In this example, the user ID is 0a03f5833900d3730f13c00f49d5exxx.
                       { Grantee: { Type: 'CanonicalUser', ID: '0a03f5833900d3730f13c00f49d5exxx' }, Permission: obsClient.enums.PermissionRead }
                   ]
               }
           };
           // Configure logging for a bucket.
           const result = await obsClient.setBucketLogging(params);
           if (result.CommonMsg.Status <= 300) {
               console.log("Set bucket(%s)'s logging configuration successful!", params.Bucket);
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

   setBucketLogging();

Code Examples: Disabling Bucket Logging
---------------------------------------

This example disables logging for bucket **examplebucket**.

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

   async function setBucketLogging() {
       try {
           const params = {
               // Specify the bucket name.
               Bucket: "examplebucket",
               // Clear the logging configuration.
               LoggingEnabled : {}
           };
           // Delete the access logging configuration of the bucket.
           const result = await obsClient.setBucketLogging(params);
           if (result.CommonMsg.Status <= 300) {
               console.log("Delete bucket(%s)'s logging configuration successful!", params.Bucket);
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

   setBucketLogging();
