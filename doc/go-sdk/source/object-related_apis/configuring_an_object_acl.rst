:original_name: obs_33_0509.html

.. _obs_33_0509:

Configuring an Object ACL
=========================

Function
--------

Access control lists (ACLs) allow resource owners to grant other accounts the permissions to access resources. By default, only the resource owner has full control over resources when a bucket or object is created. That is, the bucket creator has full control over the bucket, and the object uploader has full control over the object. Other accounts do not have the permissions to access resources. If resource owners want to grant other accounts the read and write permissions on resources, they can use ACLs. ACLs grant permissions to accounts. After an account is granted permissions, both the account and its IAM users can access the resources. Even if an ACL is set for an object encrypted using SSE-KMS, the cross-tenant access is unavailable.

You can set an ACL when uploading an object or call an ACL API to modify or obtain the ACL of an existing object.

Restrictions
------------

-  To configure object ACL, you must be the bucket owner or have the required permission (**obs:object:PutObjectAcl** in IAM or **PutObjectAcl** in a bucket policy).
-  An object can have a maximum of 100 rules in its ACL.

Method
------

**func** (obsClient ObsClient) SetObjectAcl(input \*\ :ref:`SetObjectAclInput <obs_33_0509__table14455523>`) (output \*\ :ref:`BaseModel <obs_33_0509__table11821548123411>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                      | Mandatory (Yes/No) | Description                                                                                                           |
   +=================+===========================================================+====================+=======================================================================================================================+
   | input           | \*\ :ref:`SetObjectAclInput <obs_33_0509__table14455523>` | Yes                | **Explanation:**                                                                                                      |
   |                 |                                                           |                    |                                                                                                                       |
   |                 |                                                           |                    | Input parameters for configuring an ACL for the object. For details, see :ref:`Table 2 <obs_33_0509__table14455523>`. |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0509__table14455523:

.. table:: **Table 2** SetObjectAclInput

   +-----------------+----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                               | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+====================================================+====================+===================================================================================================================================================================================+
   | Bucket          | string                                             | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | Bucket name                                                                                                                                                                       |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                    |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                    |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                    |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                    |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                    |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | None                                                                                                                                                                              |
   +-----------------+----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key             | string                                             | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                             |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | None                                                                                                                                                                              |
   +-----------------+----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId       | string                                             | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | Object version ID, for example, **G001117FCE89978B0000401205D5DC9A**                                                                                                              |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | The value must contain 32 characters.                                                                                                                                             |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | None                                                                                                                                                                              |
   +-----------------+----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ACL             | :ref:`AclType <obs_33_0509__table3131153615508>`   | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | Pre-defined ACL.                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | See :ref:`Table 3 <obs_33_0509__table3131153615508>`.                                                                                                                             |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | None                                                                                                                                                                              |
   +-----------------+----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner           | :ref:`Owner <obs_33_0509__table390162815439>`      | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | Account ID of the object owner. For details, see :ref:`Table 4 <obs_33_0509__table390162815439>`.                                                                                 |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Owner** and **Grants** must be used together and they cannot be used with **ACL**.                                                                                              |
   +-----------------+----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Grants          | []\ :ref:`Grant <obs_33_0509__table1466035143020>` | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | Grantees' permission information. For details, see :ref:`Table 5 <obs_33_0509__table1466035143020>`.                                                                              |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                    |                    |                                                                                                                                                                                   |
   |                 |                                                    |                    | None                                                                                                                                                                              |
   +-----------------+----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0509__table3131153615508:

.. table:: **Table 3** AclType

   +-----------------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Constant                    | Default Value               | Description                                                                                                                                                                                                                                                                                                                                                 |
   +=============================+=============================+=============================================================================================================================================================================================================================================================================================================================================================+
   | AclPrivate                  | private                     | Private read/write                                                                                                                                                                                                                                                                                                                                          |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | A bucket or object can only be accessed by its owner.                                                                                                                                                                                                                                                                                                       |
   +-----------------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AclPublicRead               | public-read                 | Public read and private write                                                                                                                                                                                                                                                                                                                               |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | If this permission is granted on a bucket, anyone can read the object list, multipart tasks, metadata, and object versions in the bucket.                                                                                                                                                                                                                   |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | If it is granted on an object, anyone can read the content and metadata of the object.                                                                                                                                                                                                                                                                      |
   +-----------------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AclPublicReadWrite          | public-read-write           | Public read/write                                                                                                                                                                                                                                                                                                                                           |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | If this permission is granted on a bucket, anyone can read the object list, multipart tasks, metadata, and object versions in the bucket, and can upload or delete objects, initiate multipart upload tasks, upload parts, assemble parts, copy parts, and abort multipart upload tasks.                                                                    |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | If it is granted on an object, anyone can read the content and metadata of the object.                                                                                                                                                                                                                                                                      |
   +-----------------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AclPublicReadDelivered      | public-read-delivered       | Public read on a bucket as well as objects in the bucket                                                                                                                                                                                                                                                                                                    |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | If this permission is granted on a bucket, anyone can read the object list, multipart tasks, metadata, and object versions, and read the content and metadata of objects in the bucket.                                                                                                                                                                     |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | .. note::                                                                                                                                                                                                                                                                                                                                                   |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             |    **AclPublicReadDelivered** does not apply to objects.                                                                                                                                                                                                                                                                                                    |
   +-----------------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AclPublicReadWriteDelivered | public-read-write-delivered | Public read/write on a bucket as well as objects in the bucket                                                                                                                                                                                                                                                                                              |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | If this permission is granted on a bucket, anyone can read the object list, multipart uploads, metadata, and object versions in the bucket, and can upload or delete objects, initiate multipart upload tasks, upload parts, assemble parts, copy parts, and abort multipart uploads. They can also read the content and metadata of objects in the bucket. |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | .. note::                                                                                                                                                                                                                                                                                                                                                   |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             |    **AclPublicReadWriteDelivered** does not apply to objects.                                                                                                                                                                                                                                                                                               |
   +-----------------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AclBucketOwnerFullControl   | bucket-owner-full-control   | If this permission is granted on an object, only the bucket and object owners have the full control over the object.                                                                                                                                                                                                                                        |
   |                             |                             |                                                                                                                                                                                                                                                                                                                                                             |
   |                             |                             | By default, if you upload an object to a bucket of any other user, the bucket owner does not have the permissions on your object. After you grant this permission to the bucket owner, the bucket owner can have full control over your object.                                                                                                             |
   +-----------------------------+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0509__table390162815439:

.. table:: **Table 4** Owner

   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                 | Description                                                                                |
   +=================+=================+====================================+============================================================================================+
   | ID              | string          | Yes if used as a request parameter | **Explanation:**                                                                           |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | Account (domain) ID of the owner                                                           |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | **Value range**:                                                                           |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>` |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | **Default value**:                                                                         |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | None                                                                                       |
   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------+

.. _obs_33_0509__table1466035143020:

.. table:: **Table 5** Grant

   +-----------------+---------------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------+
   | Parameter       | Type                                                    | Mandatory (Yes/No)                 | Description                                                                            |
   +=================+=========================================================+====================================+========================================================================================+
   | Grantee         | :ref:`Grantee <obs_33_0509__table137688903120>`         | Yes if used as a request parameter | **Explanation:**                                                                       |
   |                 |                                                         |                                    |                                                                                        |
   |                 |                                                         |                                    | Grantee information. For details, see :ref:`Table 6 <obs_33_0509__table137688903120>`. |
   +-----------------+---------------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------+
   | Permission      | :ref:`PermissionType <obs_33_0509__table2033304653119>` | Yes if used as a request parameter | **Explanation:**                                                                       |
   |                 |                                                         |                                    |                                                                                        |
   |                 |                                                         |                                    | Granted permission                                                                     |
   |                 |                                                         |                                    |                                                                                        |
   |                 |                                                         |                                    | **Value range**:                                                                       |
   |                 |                                                         |                                    |                                                                                        |
   |                 |                                                         |                                    | See :ref:`Table 7 <obs_33_0509__table2033304653119>`.                                  |
   |                 |                                                         |                                    |                                                                                        |
   |                 |                                                         |                                    | **Default value**:                                                                     |
   |                 |                                                         |                                    |                                                                                        |
   |                 |                                                         |                                    | None                                                                                   |
   +-----------------+---------------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------+

.. _obs_33_0509__table137688903120:

.. table:: **Table 6** Grantee

   +-----------------+---------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                    | Mandatory (Yes/No)                                                                           | Description                                                                                |
   +=================+=========================================================+==============================================================================================+============================================================================================+
   | Type            | :ref:`GranteeType <obs_33_0509__table1272250183214>`    | Yes if used as a request parameter                                                           | **Explanation:**                                                                           |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | Grantee type                                                                               |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | **Value range**:                                                                           |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | See :ref:`Table 8 <obs_33_0509__table1272250183214>`.                                      |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | **Default value**:                                                                         |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | None                                                                                       |
   +-----------------+---------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | ID              | string                                                  | Yes if this parameter is used as a request parameter and **Type** is set to **GranteeUser**  | **Explanation:**                                                                           |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | Account (domain) ID of the grantee                                                         |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | **Value range**:                                                                           |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>` |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | **Default value**:                                                                         |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | None                                                                                       |
   +-----------------+---------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | DisplayName     | string                                                  | No if used as a request parameter                                                            | **Explanation:**                                                                           |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | Account name of the grantee                                                                |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | **Restrictions:**                                                                          |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | -  Starts with a letter.                                                                   |
   |                 |                                                         |                                                                                              | -  Contains 6 to 32 characters.                                                            |
   |                 |                                                         |                                                                                              | -  Contains only letters, digits, hyphens (-), or underscores (_).                         |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | **Default value**:                                                                         |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | None                                                                                       |
   +-----------------+---------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | URI             | :ref:`GroupUriType <obs_33_0509__table163361648163313>` | Yes if this parameter is used as a request parameter and **Type** is set to **GranteeGroup** | **Explanation:**                                                                           |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | Authorized user group                                                                      |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | **Value range**:                                                                           |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | See :ref:`Table 9 <obs_33_0509__table163361648163313>`.                                    |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | **Default value**:                                                                         |
   |                 |                                                         |                                                                                              |                                                                                            |
   |                 |                                                         |                                                                                              | None                                                                                       |
   +-----------------+---------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+

.. _obs_33_0509__table2033304653119:

.. table:: **Table 7** PermissionType

   +-----------------------+---------------+-------------------------------------------------------------------------------------------------------------------+
   | Constant              | Default Value | Description                                                                                                       |
   +=======================+===============+===================================================================================================================+
   | PermissionRead        | READ          | Read permission                                                                                                   |
   +-----------------------+---------------+-------------------------------------------------------------------------------------------------------------------+
   | PermissionWrite       | WRITE         | Write permission                                                                                                  |
   +-----------------------+---------------+-------------------------------------------------------------------------------------------------------------------+
   | PermissionReadAcp     | READ_ACP      | Permission to read ACL configurations                                                                             |
   +-----------------------+---------------+-------------------------------------------------------------------------------------------------------------------+
   | PermissionWriteAcp    | WRITE_ACP     | Permission to modify ACL configurations                                                                           |
   +-----------------------+---------------+-------------------------------------------------------------------------------------------------------------------+
   | PermissionFullControl | FULL_CONTROL  | Full control access, including read and write permissions for a bucket and its ACL, or for an object and its ACL. |
   +-----------------------+---------------+-------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0509__table1272250183214:

.. table:: **Table 8** GranteeType

   ============ ============= ===============
   Constant     Default Value Description
   ============ ============= ===============
   GranteeGroup Group         User group
   GranteeUser  CanonicalUser Individual user
   ============ ============= ===============

.. _obs_33_0509__table163361648163313:

.. table:: **Table 9** GroupUriType

   ============= ============= ===========
   Constant      Default Value Description
   ============= ============= ===========
   GroupAllUsers AllUsers      All users
   ============= ============= ===========

Responses
---------

.. table:: **Table 10** List of returned results

   +-----------------------+---------------------------------------------------------+----------------------------------------------------------------------------------------+
   | Parameter             | Type                                                    | Description                                                                            |
   +=======================+=========================================================+========================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0509__table11821548123411>` | **Explanation:**                                                                       |
   |                       |                                                         |                                                                                        |
   |                       |                                                         | Returned results. For details, see :ref:`Table 11 <obs_33_0509__table11821548123411>`. |
   +-----------------------+---------------------------------------------------------+----------------------------------------------------------------------------------------+
   | err                   | error                                                   | **Explanation:**                                                                       |
   |                       |                                                         |                                                                                        |
   |                       |                                                         | Error messages returned by the API                                                     |
   +-----------------------+---------------------------------------------------------+----------------------------------------------------------------------------------------+

.. _obs_33_0509__table11821548123411:

.. table:: **Table 11** BaseModel

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================+
   | StatusCode            | int                   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP status code                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Request ID returned by the OBS server                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ResponseHeaders       | map[string][]string   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP response headers                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example sets the ACL of object **example/objectname** to Private.

::

   package main
   import (
       "fmt"
       "os"
       "obs-sdk-go/obs"
   )
   func main() {
       //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
       //Obtain an AK/SK pair on the management console.
       ak := os.Getenv("AccessKeyID")
       sk := os.Getenv("SecretAccessKey")
       // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
       securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint, obs.WithSecurityToken(securityToken))
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.SetObjectAclInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify an object (example/objectname as an example).
       input.Key = "example/objectname"
       // Set the object ACL to Private.
       input.ACL = obs.AclPrivate
       // Configure the object ACL.
       output, err := obsClient.SetObjectAcl(input)
       if err == nil {
           fmt.Printf("Set Object(%s)'s acl successful with Bucket(%s)!\n", input.Key, input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Set Object(%s)'s acl fail with Bucket(%s)!\n", input.Key, input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
