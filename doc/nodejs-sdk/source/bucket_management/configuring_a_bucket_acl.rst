:original_name: obs_29_0306.html

.. _obs_29_0306:

Configuring a Bucket ACL
========================

Function
--------

Access control lists (ACLs) allow resource owners to grant other accounts the permissions to access resources. By default, only the resource owner has full control over resources when a bucket or object is created. That is, the bucket creator has full control over the bucket, and the object uploader has full control over the object. Other accounts do not have the permissions to access resources. If resource owners want to grant other accounts the read and write permissions on resources, they can use ACLs. ACLs grant permissions to accounts. After an account is granted permissions, both the account and its IAM users can access the resources.

This API modifies a bucket ACL.

Restrictions
------------

-  A bucket can have up to 100 ACL rules.
-  To configure an ACL for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketAcl** in IAM or **PutBucketAcl** in a bucket policy).

Method
------

.. code-block::

   ObsClient.setBucketAcl(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+----------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                               | Mandatory (Yes/No) | Description                                                                                                                                                                          |
   +=================+====================================================+====================+======================================================================================================================================================================================+
   | Bucket          | string                                             | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | Bucket name.                                                                                                                                                                         |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Restrictions:**                                                                                                                                                                    |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                     |
   |                 |                                                    |                    | -  A bucket name:                                                                                                                                                                    |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                         |
   |                 |                                                    |                    |    -  Cannot be formatted as an IP address.                                                                                                                                          |
   |                 |                                                    |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                           |
   |                 |                                                    |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                      |
   |                 |                                                    |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                            |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | The value can contain 3 to 63 characters.                                                                                                                                            |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | None                                                                                                                                                                                 |
   +-----------------+----------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ACL             | :ref:`AclType <obs_29_0306__table1678382365116>`   | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | Pre-defined ACL.                                                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | You must specify either **ACL** or the combination of **Owner** and **Grants**.                                                                                                      |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | See :ref:`Table 2 <obs_29_0306__table1678382365116>`.                                                                                                                                |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | None                                                                                                                                                                                 |
   +-----------------+----------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner           | :ref:`Owner <obs_29_0306__table26550449512>`       | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | Bucket owner                                                                                                                                                                         |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | -  **Owner** and **Grants** must be used together, and they cannot be used with **ACL**.                                                                                             |
   |                 |                                                    |                    | -  You must specify either **ACL** or the combination of **Owner** and **Grants**.                                                                                                   |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | See :ref:`Table 3 <obs_29_0306__table26550449512>`.                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | None                                                                                                                                                                                 |
   +-----------------+----------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Grants          | :ref:`Grant <obs_29_0306__table1764402511517>`\ [] | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | Grantees and permissions                                                                                                                                                             |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | -  **Owner** and **Grants** must be used together, and they cannot be used with **ACL**.                                                                                             |
   |                 |                                                    |                    | -  You must specify either **ACL** or the combination of **Owner** and **Grants**.                                                                                                   |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | See :ref:`Table 4 <obs_29_0306__table1764402511517>`.                                                                                                                                |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                    |                    |                                                                                                                                                                                      |
   |                 |                                                    |                    | None                                                                                                                                                                                 |
   +-----------------+----------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0306__table1678382365116:

.. table:: **Table 2** AclType

   +---------------------------------------------+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Constant                                    | Default Value               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   +=============================================+=============================+==========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | ObsClient.enums.AclPrivate                  | private                     | Private read and write                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | A bucket or object can only be accessed by its owner.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   +---------------------------------------------+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.AclPublicRead               | public-read                 | Public read and private write                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | If this permission is granted on a bucket, anyone can read the object list, multipart uploads, metadata, and object versions in the bucket.                                                                                                                                                                                                                                                                                                                                              |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | If this permission is granted on an object, everyone can obtain the content and metadata of the object.                                                                                                                                                                                                                                                                                                                                                                                  |
   +---------------------------------------------+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.AclPublicReadWrite          | public-read-write           | Public read and write                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | If this permission is granted on a bucket, anyone can read the object list, multipart tasks, metadata, and object versions in the bucket and can upload or delete objects, initiate multipart upload tasks, upload parts, assemble parts, copy parts, and abort multipart upload tasks.                                                                                                                                                                                                  |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | If this permission is granted on an object, everyone can obtain the content and metadata of the object.                                                                                                                                                                                                                                                                                                                                                                                  |
   +---------------------------------------------+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.AclPublicReadDelivered      | public-read-delivered       | Public read on a bucket as well as the objects in the bucket.                                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | If this permission is granted on a bucket, anyone can read the object list, multipart tasks, metadata, and object versions and read the content and metadata of objects in the bucket.                                                                                                                                                                                                                                                                                                   |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             |    **AclPublicReadDelivered** does not apply to objects.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   +---------------------------------------------+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.AclPublicReadWriteDelivered | public-read-write-delivered | Public read and write on a bucket as well as the objects in the bucket.                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | If this permission is granted on a bucket, anyone can read the object list, multipart uploads, metadata, and object versions in the bucket and can upload or delete objects, initiate multipart upload tasks, upload parts, assemble parts, copy parts, and abort multipart uploads. They can also read the content and metadata of objects in the bucket.                                                                                                                               |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             |    **AclPublicReadWriteDelivered** does not apply to objects.                                                                                                                                                                                                                                                                                                                                                                                                                            |
   +---------------------------------------------+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.AclBucketOwnerFullControl   | bucket-owner-full-control   | If this permission is granted on an object, only the bucket and object owners have the full control over the object.                                                                                                                                                                                                                                                                                                                                                                     |
   |                                             |                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                                             |                             | By default, if you upload an object to a bucket of any other user, the bucket owner does not have the permissions on your object. After you grant this policy to the bucket owner, the bucket owner can have full control over your object. For example, if user A uploads object **x** to user B's bucket, user B does not have the control over object **x**. If user A sets the **bucket-owner-full-control** policy for object **x**, user B then has the control over object **x**. |
   +---------------------------------------------+-----------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0306__table26550449512:

.. table:: **Table 3** Owner

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

.. _obs_29_0306__table1764402511517:

.. table:: **Table 4** Grant

   +-----------------+----------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+
   | Parameter       | Type                                               | Mandatory (Yes/No)                 | Description                                                                           |
   +=================+====================================================+====================================+=======================================================================================+
   | Grantee         | :ref:`Grantee <obs_29_0306__table94488481611>`     | Yes if used as a request parameter | **Explanation:**                                                                      |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | Grantee information. For details, see :ref:`Table 5 <obs_29_0306__table94488481611>`. |
   +-----------------+----------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+
   | Permission      | :ref:`PermissionType <obs_29_0306__table60165497>` | Yes if used as a request parameter | **Explanation:**                                                                      |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | Granted permission                                                                    |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | **Value range**:                                                                      |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | See :ref:`Table 8 <obs_29_0306__table60165497>`.                                      |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | **Default value**:                                                                    |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | None                                                                                  |
   +-----------------+----------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+
   | Delivered       | boolean                                            | No                                 | **Explanation:**                                                                      |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | Whether the ACL of the bucket applies to its objects                                  |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | **Value range**:                                                                      |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | -  **true**: The ACL of the bucket applies to its objects.                            |
   |                 |                                                    |                                    | -  **false**: The ACL of the bucket does not apply to its objects.                    |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | **Default value**:                                                                    |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | None                                                                                  |
   +-----------------+----------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+

.. _obs_29_0306__table94488481611:

.. table:: **Table 5** Grantee

   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                   | Mandatory (Yes/No)                                                                  | Description                                                                                 |
   +=================+========================================================+=====================================================================================+=============================================================================================+
   | Type            | string                                                 | Yes if used as a request parameter                                                  | **Explanation:**                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | Grantee type                                                                                |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Value range**:                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | See :ref:`Table 6 <obs_29_0306__table531313065315>`.                                        |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Default value**:                                                                          |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | None                                                                                        |
   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | ID              | string                                                 | Yes if this parameter is used as a request parameter and **Type** is set to a user  | **Explanation:**                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | Account (domain) ID of the grantee.                                                         |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Value range**:                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_29_1715>`. |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Default value**:                                                                          |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | None                                                                                        |
   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Name            | string                                                 | No if used as a request parameter                                                   | **Explanation:**                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | Account name of the grantee                                                                 |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Restrictions**:                                                                           |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | -  The account name starts with a letter.                                                   |
   |                 |                                                        |                                                                                     | -  The account name contains 6 to 32 characters.                                            |
   |                 |                                                        |                                                                                     | -  The account name contains only letters, digits, hyphens (-), or underscores (_).         |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Default value**:                                                                          |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | None                                                                                        |
   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | URI             | :ref:`GroupUriType <obs_29_0306__table84401320145418>` | Yes if this parameter is used as a request parameter and **Type** is set to a group | **Explanation:**                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | Authorized user group                                                                       |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Value range**:                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | See :ref:`Table 7 <obs_29_0306__table84401320145418>`.                                      |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Default value**:                                                                          |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | None                                                                                        |
   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+

.. _obs_29_0306__table531313065315:

.. table:: **Table 6** GranteeType

   ============= =======================================
   Constant      Description
   ============= =======================================
   Group         Grants permissions to user groups.
   CanonicalUser Grants permissions to individual users.
   ============= =======================================

.. _obs_29_0306__table84401320145418:

.. table:: **Table 7** GroupUriType

   +-----------------------------------------+--------------------+--------------------------------------------------+
   | Constant                                | Default Value      | Description                                      |
   +=========================================+====================+==================================================+
   | ObsClient.enums.GroupAllUsers           | AllUsers           | All users.                                       |
   +-----------------------------------------+--------------------+--------------------------------------------------+
   | ObsClient.enums.GroupAuthenticatedUsers | AuthenticatedUsers | Authorized users. This constant is deprecated.   |
   +-----------------------------------------+--------------------+--------------------------------------------------+
   | ObsClient.enums.GroupLogDelivery        | LogDelivery        | Log delivery group. This constant is deprecated. |
   +-----------------------------------------+--------------------+--------------------------------------------------+

.. _obs_29_0306__table60165497:

.. table:: **Table 8** PermissionType

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

.. table:: **Table 9** Responses

   +-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+
   | Type                                                                                      | Description                                                                           |
   +===========================================================================================+=======================================================================================+
   | :ref:`Table 10 <obs_29_0306__table1722625714202>`                                         | **Explanation:**                                                                      |
   |                                                                                           |                                                                                       |
   | .. note::                                                                                 | Returned results. For details, see :ref:`Table 10 <obs_29_0306__table1722625714202>`. |
   |                                                                                           |                                                                                       |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. |                                                                                       |
   +-------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------+

.. _obs_29_0306__table1722625714202:

.. table:: **Table 10** Response

   +-----------------------+-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                    |
   +=======================+=====================================================+================================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_0306__table6176201212273>` | **Explanation:**                                                                                                                                                               |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 11 <obs_29_0306__table6176201212273>`. |
   +-----------------------+-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`Table 12 <obs_29_0306__table33959011>`        | **Explanation:**                                                                                                                                                               |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | Results outputted for a successful call. For details, see :ref:`Table 12 <obs_29_0306__table33959011>`.                                                                        |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | **Restrictions:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | This parameter is not included if the value of **Status** is greater than 300.                                                                                                 |
   +-----------------------+-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0306__table6176201212273:

.. table:: **Table 11** ICommonMsg

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

.. _obs_29_0306__table33959011:

.. table:: **Table 12** BaseResponseOutput

   +-----------------------+-----------------------+---------------------------------------+
   | Parameter             | Type                  | Description                           |
   +=======================+=======================+=======================================+
   | RequestId             | string                | **Explanation:**                      |
   |                       |                       |                                       |
   |                       |                       | Request ID returned by the OBS server |
   +-----------------------+-----------------------+---------------------------------------+

Code Examples: Setting a Pre-defined ACL When Creating a Bucket
---------------------------------------------------------------

This example sets a pre-defined ACL (private read and write) when creating a bucket.

::

   // Import the OBS library.
   // Use npm to install the client.
   const ObsClient = require("esdk-obs-nodejs");
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');

   // Create an ObsClient instance.
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

   async function createBucket() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify the region where the bucket is to be created. The region must be the same as that in the passed endpoint.
         // Location: "region",
         // Specify the ACL. obs.AclPrivate is used as an example.
         ACL: obsClient.enums.AclPrivate,
       };
       // Create a bucket.
       const result = await obsClient.createBucket(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Create bucket(%s) successful!", params.Bucket);
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

   createBucket();

Code Examples: Setting a Pre-defined ACL for a Bucket
-----------------------------------------------------

This example sets an ACL (private) for bucket **examplebucket**.

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

   async function setBucketAcl() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Set the bucket ACL to be private.
         ACL: obsClient.enums.AclPrivate
       };
       // Set the bucket ACL.
       const result = await obsClient.setBucketAcl(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Set bucket(%s)'s acl successful!", params.Bucket);
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

   setBucketAcl();

Code Examples: Setting an ACL for a Bucket Directly
---------------------------------------------------

This example sets an ACL to allow all users to read from bucket **examplebucket** but only allow user **0a03f5833900d3730f13c00f49d5exxx** to write to the bucket.

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

   async function setBucketAcl() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify the bucket owner ID. ownerid is used in this example.
         Owner: { ID: 'ownerid' },
         Grants: [
           // Grant the public-read permission to all users.
           { Grantee: { Type: 'Group', URI: obsClient.enums.GroupAllUsers  }, Permission: obsClient.enums.PermissionRead },
             // Grant the write permission to a specific user. In this example, the user ID is 0a03f5833900d3730f13c00f49d5exxx.
           { Grantee: { Type: 'CanonicalUser', ID: '0a03f5833900d3730f13c00f49d5exxx' }, Permission: obsClient.enums.PermissionWrite },
         ]
       };
       // Set the bucket ACL.
       const result = await obsClient.setBucketAcl(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Set bucket(%s)'s acl successful!", params.Bucket);
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

   setBucketAcl();
