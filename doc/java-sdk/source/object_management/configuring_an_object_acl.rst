:original_name: obs_21_0802.html

.. _obs_21_0802:

Configuring an Object ACL
=========================

Function
--------

Access control lists (ACLs) allow resource owners to grant other accounts the permissions to access resources. By default, only the resource owner has full control over resources when a bucket or object is created. That is, the bucket creator has full control over the bucket, and the object uploader has full control over the object. Other accounts do not have the permissions to access resources. If resource owners want to grant other accounts the read and write permissions on resources, they can use ACLs. ACLs grant permissions to accounts. After an account is granted permissions, both the account and its IAM users can access the resources. If an object is encrypted with SSE-KMS, the ACL configured for it is not in effect in the cross-tenant case.

An object ACL can be configured in any of the following ways:

#. :ref:`Code Example: Setting a Pre-defined ACL When Uploading the Object <obs_21_0802__section1243465074419>`
#. :ref:`Code Example: Setting a Pre-defined ACL for the Object <obs_21_0802__section34357507447>`
#. :ref:`Code Example: Setting an ACL for the Object Directly <obs_21_0802__section4436175014419>`

Restrictions
------------

-  To configure an object ACL, you must be the bucket owner or have the required permission (**obs:object:PutObjectAcl** in IAM or **PutObjectAcl** in a bucket policy).
-  An object can have a maximum of 100 rules in its ACL.

Method
------

obsClient.setObjectAcl(:ref:`SetObjectAclRequest <obs_21_0802__table14455523>` :ref:`request <obs_21_0802__table47528147>`)

Request Parameters
------------------

.. _obs_21_0802__table47528147:

.. table:: **Table 1** List of request parameters

   +-----------------+---------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                    | Mandatory (Yes/No) | Description                                                                                                 |
   +=================+=========================================================+====================+=============================================================================================================+
   | request         | :ref:`SetObjectAclRequest <obs_21_0802__table14455523>` | Yes                | **Explanation:**                                                                                            |
   |                 |                                                         |                    |                                                                                                             |
   |                 |                                                         |                    | Request parameters for setting an object ACL. For details, see :ref:`Table 2 <obs_21_0802__table14455523>`. |
   +-----------------+---------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------+

.. _obs_21_0802__table14455523:

.. table:: **Table 2** SetObjectAclRequest

   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                       | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+============================================================+====================+===================================================================================================================================================================================+
   | bucketName      | String                                                     | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | Bucket name.                                                                                                                                                                      |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                            |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                            |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                            |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                            |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                            |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | None                                                                                                                                                                              |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey       | String                                                     | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                             |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | None                                                                                                                                                                              |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | versionId       | String                                                     | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | Object version ID.                                                                                                                                                                |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | The value must contain 32 characters.                                                                                                                                             |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | None                                                                                                                                                                              |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | acl             | :ref:`AccessControlList <obs_21_0802__table1028194816109>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | An ACL specified for the object. You can use either a pre-defined or a user-defined ACL.                                                                                          |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | -  To use a pre-defined ACL, see :ref:`Table 3 <obs_21_0802__table15301633184920>` for the available options.                                                                     |
   |                 |                                                            |                    | -  To use a user-defined ACL, see :ref:`Table 4 <obs_21_0802__table1028194816109>` to configure the required parameters.                                                          |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                            |                    |                                                                                                                                                                                   |
   |                 |                                                            |                    | AccessControlList.REST_CANNED_PRIVATE                                                                                                                                             |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0802__table15301633184920:

.. table:: **Table 3** Pre-defined ACL

   +-----------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Constant                                                  | Description                                                                                                                                                                                                                                                                                                                             |
   +===========================================================+=========================================================================================================================================================================================================================================================================================================================================+
   | AccessControlList.REST_CANNED_PRIVATE                     | Private read/write.                                                                                                                                                                                                                                                                                                                     |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | A bucket or object can only be accessed by its owner.                                                                                                                                                                                                                                                                                   |
   +-----------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AccessControlList.REST_CANNED_PUBLIC_READ                 | Public read.                                                                                                                                                                                                                                                                                                                            |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | If this permission is granted on a bucket, anyone can read the object list, multipart uploads, bucket metadata, and object versions in the bucket.                                                                                                                                                                                      |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | If this permission is granted on an object, anyone can read the content and metadata of the object.                                                                                                                                                                                                                                     |
   +-----------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AccessControlList.REST_CANNED_PUBLIC_READ_WRITE           | Public read/write.                                                                                                                                                                                                                                                                                                                      |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | If this permission is granted on a bucket, anyone can read the object list, multipart uploads, and bucket metadata, and can upload or delete objects, initiate multipart uploads, upload parts, assemble parts, copy parts, and abort multipart upload tasks.                                                                           |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | If this permission is granted on an object, anyone can read the content and metadata of the object.                                                                                                                                                                                                                                     |
   +-----------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AccessControlList.REST_CANNED_PUBLIC_READ_DELIVERED       | Public read on a bucket as well as objects in the bucket.                                                                                                                                                                                                                                                                               |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | If this permission is granted on a bucket, anyone can read the object list, multipart tasks, and bucket metadata, and can also read the content and metadata of the objects in the bucket.                                                                                                                                              |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | This permission cannot be granted on objects.                                                                                                                                                                                                                                                                                           |
   +-----------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AccessControlList.REST_CANNED_PUBLIC_READ_WRITE_DELIVERED | Public read/write on a bucket as well as objects in the bucket.                                                                                                                                                                                                                                                                         |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | If this permission is granted on a bucket, anyone can read the object list, multipart uploads, and bucket metadata, and can upload or delete objects, initiate multipart upload tasks, upload parts, assemble parts, copy parts, and abort multipart uploads. They can also read the content and metadata of the objects in the bucket. |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | This permission cannot be granted on objects.                                                                                                                                                                                                                                                                                           |
   +-----------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AccessControlList.REST_CANNED_BUCKET_OWNER_FULL_CONTROL   | If this permission is granted on an object, only the bucket and object owners have the full control over the object.                                                                                                                                                                                                                    |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | By default, if you upload an object to a bucket owned by another user, the bucket owner does not have the permissions on your object. After you grant this permission to the bucket owner, the bucket owner can have full control over your object.                                                                                     |
   |                                                           |                                                                                                                                                                                                                                                                                                                                         |
   |                                                           | For example, if user A uploads object **x** to user B's bucket, user B does not have the control over object **x**. If user A sets **bucket-owner-full-control** for object **x**, user B then has the control over object **x**.                                                                                                       |
   +-----------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0802__table1028194816109:

.. table:: **Table 4** AccessControlList

   +-----------------+------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                             | Mandatory (Yes/No) | Description                                                                                  |
   +=================+==================================================================+====================+==============================================================================================+
   | owner           | :ref:`Owner <obs_21_0802__table1183415419527>`                   | Yes                | **Explanation:**                                                                             |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | Bucket owner information. For details, see :ref:`Table 5 <obs_21_0802__table1183415419527>`. |
   +-----------------+------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | delivered       | boolean                                                          | No                 | **Explanation:**                                                                             |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | Whether the bucket ACL is applied to all objects in the bucket.                              |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | **Value range**:                                                                             |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | **true**: The bucket ACL is applied to all objects in the bucket.                            |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | **false**: The bucket ACL is not applied to any objects in the bucket.                       |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | **Default value**:                                                                           |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | **false**                                                                                    |
   +-----------------+------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | grants          | Set<:ref:`GrantAndPermission <obs_21_0802__table1966620295123>`> | No                 | **Explanation:**                                                                             |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | Grantee information. For details, see :ref:`Table 6 <obs_21_0802__table1966620295123>`.      |
   +-----------------+------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+

.. _obs_21_0802__table1183415419527:

.. table:: **Table 5** Owner

   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                  |
   +=================+=================+====================+==============================================================================================+
   | id              | String          | Yes                | **Explanation:**                                                                             |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | Account (domain) ID of the bucket owner.                                                     |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | **Value range**:                                                                             |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>`   |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | **Default value**:                                                                           |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | None                                                                                         |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------+
   | displayName     | String          | No                 | **Explanation:**                                                                             |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | Account name of the owner.                                                                   |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | **Value range**:                                                                             |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | To obtain the account name, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>` |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | **Default value**:                                                                           |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | None                                                                                         |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------+

.. _obs_21_0802__table1966620295123:

.. table:: **Table 6** GrantAndPermission

   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                       | Mandatory (Yes/No) | Description                                                                                          |
   +=================+============================================================+====================+======================================================================================================+
   | grantee         | :ref:`GranteeInterface <obs_21_0802__table16903171143518>` | Yes                | **Explanation:**                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | Grantees (users or user groups). For details, see :ref:`Table 7 <obs_21_0802__table16903171143518>`. |
   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------+
   | permission      | :ref:`Permission <obs_21_0802__table17475749161815>`       | Yes                | **Explanation:**                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | Permissions to grant.                                                                                |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | **Value range**:                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | See :ref:`Table 10 <obs_21_0802__table17475749161815>`.                                              |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | **Default value**:                                                                                   |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | None                                                                                                 |
   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------+
   | delivered       | boolean                                                    | No                 | **Explanation:**                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | Whether the bucket ACL is applied to all objects in the bucket.                                      |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | **Value range**:                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | **true**: The bucket ACL is applied to all objects in the bucket.                                    |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | **false**: The bucket ACL is not applied to any objects in the bucket.                               |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | **Default value**:                                                                                   |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | **false**                                                                                            |
   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------+

.. _obs_21_0802__table16903171143518:

.. table:: **Table 7** GranteeInterface

   +---------------------------------------------------------+---------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | Parameter                                               | Type                                                    | Mandatory (Yes/No) | Description                                                                                  |
   +=========================================================+=========================================================+====================+==============================================================================================+
   | :ref:`CanonicalGrantee <obs_21_0802__table94488481611>` | :ref:`CanonicalGrantee <obs_21_0802__table94488481611>` | Yes                | **Explanation:**                                                                             |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | Grantee (user) information. For details, see :ref:`Table 8 <obs_21_0802__table94488481611>`. |
   +---------------------------------------------------------+---------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | :ref:`GroupGrantee <obs_21_0802__table9881261176>`      | :ref:`GroupGrantee <obs_21_0802__table9881261176>`      | Yes                | **Explanation:**                                                                             |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | Grantee (user group) information.                                                            |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | **Value range**:                                                                             |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | See :ref:`Table 9 <obs_21_0802__table9881261176>`.                                           |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | **Default value**:                                                                           |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | None                                                                                         |
   +---------------------------------------------------------+---------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+

.. _obs_21_0802__table94488481611:

.. table:: **Table 8** CanonicalGrantee

   +-----------------+-----------------+-------------------------------------------+----------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                        | Description                                                                                  |
   +=================+=================+===========================================+==============================================================================================+
   | grantId         | String          | Yes if **Type** is set to **GranteeUser** | **Explanation:**                                                                             |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | Account (domain) ID of the grantee.                                                          |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | **Value range**:                                                                             |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>`   |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | **Default value**:                                                                           |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | None                                                                                         |
   +-----------------+-----------------+-------------------------------------------+----------------------------------------------------------------------------------------------+
   | displayName     | String          | No                                        | **Explanation**:                                                                             |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | Account name of the grantee.                                                                 |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | **Value range**:                                                                             |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | To obtain the account name, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>` |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | **Default value**:                                                                           |
   |                 |                 |                                           |                                                                                              |
   |                 |                 |                                           | None                                                                                         |
   +-----------------+-----------------+-------------------------------------------+----------------------------------------------------------------------------------------------+

.. _obs_21_0802__table9881261176:

.. table:: **Table 9** GroupGrantee

   =================== ================================================
   Constant            Description
   =================== ================================================
   ALL_USERS           All users.
   AUTHENTICATED_USERS Authorized users. This constant is deprecated.
   LOG_DELIVERY        Log delivery group. This constant is deprecated.
   =================== ================================================

.. _obs_21_0802__table17475749161815:

.. table:: **Table 10** Permission

   +-------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Constant                | Default Value         | Description                                                                                                                                        |
   +=========================+=======================+====================================================================================================================================================+
   | PERMISSION_READ         | READ                  | Read permission.                                                                                                                                   |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | A grantee with this permission for a bucket can obtain the list of objects, multipart uploads, bucket metadata, and object versions in the bucket. |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | A grantee with this permission for an object can obtain the object content and metadata.                                                           |
   +-------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | PERMISSION_WRITE        | WRITE                 | Write permission.                                                                                                                                  |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | A grantee with this permission for a bucket can upload, overwrite, and delete any object or part in the bucket.                                    |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | This permission is not available for objects.                                                                                                      |
   +-------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | PERMISSION_READ_ACP     | READ_ACP              | Permission to read an ACL.                                                                                                                         |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | A grantee with this permission can obtain the ACL of a bucket or object.                                                                           |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | A bucket or object owner has this permission for their bucket or object by default.                                                                |
   +-------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | PERMISSION_WRITE_ACP    | WRITE_ACP             | Permission to modify an ACL.                                                                                                                       |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | A grantee with this permission can update the ACL of a bucket or object.                                                                           |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | A bucket or object owner has this permission for their bucket or object by default.                                                                |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | This permission allows the grantee to change the access control policies, meaning the grantee has full control over a bucket or object.            |
   +-------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | PERMISSION_FULL_CONTROL | FULL_CONTROL          | Full control access, including read and write permissions for a bucket and its ACL, or for an object and its ACL.                                  |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | A grantee with this permission for a bucket has **READ**, **WRITE**, **READ_ACP**, and **WRITE_ACP** permissions for the bucket.                   |
   |                         |                       |                                                                                                                                                    |
   |                         |                       | A grantee with this permission for an object has **READ**, **READ_ACP**, and **WRITE_ACP** permissions for the object.                             |
   +-------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 11** Common response headers

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================+
   | statusCode            | int                   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP status code.                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | responseHeaders       | Map<String, Object>   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0802__section1243465074419:

Code Example: Setting a Pre-defined ACL When Uploading the Object
-----------------------------------------------------------------

This example uploads **localfile** to bucket **examplebucket** as object **objectname**, and specifies a pre-defined ACl during the upload.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.AccessControlList;
   import com.obs.services.model.PutObjectRequest;
   import java.io.File;
   public class PutObject012 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
           // Enter the endpoint corresponding to the region where the bucket is to be created.
           String endPoint = "https://your-endpoint";
           // Obtain an endpoint using environment variables or import it in other ways.
           //String endPoint = System.getenv("ENDPOINT");

           // Create an ObsClient instance.
           // Use the permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use the temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               // Specify a pre-defined ACL during object upload.
               PutObjectRequest request = new PutObjectRequest();
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               request.setFile(new File("localfile"));
               // Set the object ACL to private read and write.
               request.setAcl(AccessControlList.REST_CANNED_PRIVATE);
               obsClient.putObject(request);
               System.out.println("putObject successfully");
           } catch (ObsException e) {
               System.out.println("putObject failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code:" + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message:" + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
               e.printStackTrace();
           } catch (Exception e) {
               System.out.println("putObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

.. _obs_21_0802__section34357507447:

Code Example: Setting a Pre-defined ACL for the Object
------------------------------------------------------

This example specifies a pre-defined ACL of private read and write for object **objectname** in **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.AccessControlList;
   public class SetObjectAcl001 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
           // Enter the endpoint corresponding to the region where the bucket is to be created.
           String endPoint = "https://your-endpoint";
           // Obtain an endpoint using environment variables or import it in other ways.
           //String endPoint = System.getenv("ENDPOINT");

           // Create an ObsClient instance.
           // Use the permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use the temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               // Set a predefined ACL for the object.
               // Set the object ACL to private read and write.
               obsClient.setObjectAcl("examplebucket", "objectname", AccessControlList.REST_CANNED_PRIVATE);
               System.out.println("setObjectAcl successfully");
           } catch (ObsException e) {
               System.out.println("setObjectAcl failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code:" + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message:" + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
               e.printStackTrace();
           } catch (Exception e) {
               System.out.println("setObjectAcl failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

.. _obs_21_0802__section4436175014419:

Code Example: Setting an ACL for the Object Directly
----------------------------------------------------

This example configures an ACL for object **objectname** in bucket **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.AccessControlList;
   import com.obs.services.model.CanonicalGrantee;
   import com.obs.services.model.GroupGrantee;
   import com.obs.services.model.Owner;
   import com.obs.services.model.Permission;
   public class SetObjectAcl002 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
           // Enter the endpoint corresponding to the region where the bucket is to be created.
           String endPoint = "https://your-endpoint";
           // Obtain an endpoint using environment variables or import it in other ways.
           //String endPoint = System.getenv("ENDPOINT");

           // Create an ObsClient instance.
           // Use the permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use the temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               AccessControlList acl = new AccessControlList();
               Owner owner = new Owner();
               owner.setId("ownerid");
               // (Mandatory) Owner ID
               acl.setOwner(owner);
               //Retain the owner's full control permissions. (Note that if this permission is not set, the owner does not have the access permission.)
               acl.grantPermission(new CanonicalGrantee("ownerid"), Permission.PERMISSION_FULL_CONTROL);
               // Grant the full control permission to a specified user.
               acl.grantPermission(new CanonicalGrantee("userid"), Permission.PERMISSION_FULL_CONTROL);
               // Grant the read permission to all users.
               acl.grantPermission(GroupGrantee.ALL_USERS, Permission.PERMISSION_READ);
               obsClient.setObjectAcl("examplebucket", "objectname", acl);
               System.out.println("setObjectAcl successfully");
               System.out.println(acl);
           } catch (ObsException e) {
               System.out.println("setObjectAcl failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code:" + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message:" + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
               e.printStackTrace();
           } catch (Exception e) {
               System.out.println("setObjectAcl failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
