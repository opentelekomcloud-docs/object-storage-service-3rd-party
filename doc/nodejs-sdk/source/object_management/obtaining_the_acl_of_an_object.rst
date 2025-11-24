:original_name: obs_29_0603.html

.. _obs_29_0603:

Obtaining the ACL of an Object
==============================

Function
--------

Access control lists (ACLs) allow resource owners to grant other accounts the permissions to access resources. By default, only the resource owner has full control over resources when a bucket or object is created. That is, the bucket creator has full control over the bucket, and the object uploader has full control over the object. Other accounts do not have the permissions to access resources. If resource owners want to grant other accounts the read and write permissions on resources, they can use ACLs. ACLs grant permissions to accounts. After an account is granted permissions, both the account and its IAM users can access the resources.

This API returns the ACL of an object.

Restrictions
------------

-  To obtain an object ACL, you must be the bucket owner or have the required permission (**obs:object:GetObjectAcl** in IAM or **GetObjectAcl** in a bucket policy).

Method
------

.. code-block::

   ObsClient.getObjectAcl(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                          |
   +=================+=================+====================+======================================================================================================================================================================================+
   | Bucket          | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Bucket name                                                                                                                                                                          |
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
   | Key             | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name.                  |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | The value can contain 1 to 1,024 characters.                                                                                                                                         |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId       | string          | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Object version ID, for example, **G001117FCE89978B0000401205D5DC9A**                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | The value must contain 32 characters.                                                                                                                                                |
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
   | :ref:`Table 3 <obs_29_0603__table1722625714202>`                                          | **Explanation:**                                                                     |
   |                                                                                           |                                                                                      |
   | .. note::                                                                                 | Returned results. For details, see :ref:`Table 3 <obs_29_0603__table1722625714202>`. |
   |                                                                                           |                                                                                      |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. |                                                                                      |
   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_29_0603__table1722625714202:

.. table:: **Table 3** Response

   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                   |
   +=======================+=====================================================+===============================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_0603__table6176201212273>` | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 4 <obs_29_0603__table6176201212273>`. |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`Table 5 <obs_29_0603__table33959011>`         | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Results outputted for a successful call. For details, see :ref:`Table 5 <obs_29_0603__table33959011>`.                                                                        |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | **Restrictions:**                                                                                                                                                             |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | This parameter is not included if the value of **Status** is greater than 300.                                                                                                |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0603__table6176201212273:

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

.. _obs_29_0603__table33959011:

.. table:: **Table 5** GetObjectAclOutput

   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                               | Description                                                                                          |
   +=======================+====================================================+======================================================================================================+
   | RequestId             | string                                             | **Explanation:**                                                                                     |
   |                       |                                                    |                                                                                                      |
   |                       |                                                    | Request ID returned by the OBS server                                                                |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | VersionId             | string                                             | **Explanation:**                                                                                     |
   |                       |                                                    |                                                                                                      |
   |                       |                                                    | Object version ID, for example, **G001117FCE89978B0000401205D5DC9A**                                 |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | Owner                 | :ref:`Owner <obs_29_0603__table26550449512>`       | **Explanation:**                                                                                     |
   |                       |                                                    |                                                                                                      |
   |                       |                                                    | Object owner. For details, see :ref:`Owner <obs_29_0603__table26550449512>`.                         |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | Delivered             | string                                             | **Explanation:**                                                                                     |
   |                       |                                                    |                                                                                                      |
   |                       |                                                    | Whether the bucket ACL is applied to the objects in the bucket.                                      |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | Grants                | :ref:`Grant <obs_29_0603__table1764402511517>`\ [] | **Explanation:**                                                                                     |
   |                       |                                                    |                                                                                                      |
   |                       |                                                    | Grantees' permission information. For details, see :ref:`Table 7 <obs_29_0603__table1764402511517>`. |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------+

.. _obs_29_0603__table26550449512:

.. table:: **Table 6** Owner

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

.. _obs_29_0603__table1764402511517:

.. table:: **Table 7** Grant

   +-----------------+----------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+
   | Parameter       | Type                                               | Mandatory (Yes/No)                 | Description                                                                           |
   +=================+====================================================+====================================+=======================================================================================+
   | Grantee         | :ref:`Grantee <obs_29_0603__table94488481611>`     | Yes if used as a request parameter | **Explanation:**                                                                      |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | Grantee information. For details, see :ref:`Table 8 <obs_29_0603__table94488481611>`. |
   +-----------------+----------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+
   | Permission      | :ref:`PermissionType <obs_29_0603__table60165497>` | Yes if used as a request parameter | **Explanation:**                                                                      |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | Granted permission                                                                    |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | **Value range**:                                                                      |
   |                 |                                                    |                                    |                                                                                       |
   |                 |                                                    |                                    | See :ref:`Table 11 <obs_29_0603__table60165497>`.                                     |
   +-----------------+----------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+

.. _obs_29_0603__table94488481611:

.. table:: **Table 8** Grantee

   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                   | Mandatory (Yes/No)                                                                  | Description                                                                                 |
   +=================+========================================================+=====================================================================================+=============================================================================================+
   | Type            | string                                                 | Yes if used as a request parameter                                                  | **Explanation:**                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | Grantee type                                                                                |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Value range**:                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | See :ref:`Table 9 <obs_29_0603__table531313065315>`.                                        |
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
   |                 |                                                        |                                                                                     | Account name of the grantee.                                                                |
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
   | URI             | :ref:`GroupUriType <obs_29_0603__table84401320145418>` | Yes if this parameter is used as a request parameter and **Type** is set to a group | **Explanation:**                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | Authorized user group                                                                       |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Value range**:                                                                            |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | See :ref:`Table 10 <obs_29_0603__table84401320145418>`.                                     |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | **Default value**:                                                                          |
   |                 |                                                        |                                                                                     |                                                                                             |
   |                 |                                                        |                                                                                     | None                                                                                        |
   +-----------------+--------------------------------------------------------+-------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+

.. _obs_29_0603__table531313065315:

.. table:: **Table 9** GranteeType

   ============= =======================================
   Constant      Description
   ============= =======================================
   Group         Grants permissions to user groups.
   CanonicalUser Grants permissions to individual users.
   ============= =======================================

.. _obs_29_0603__table84401320145418:

.. table:: **Table 10** GroupUriType

   +-----------------------------------------+--------------------+--------------------------------------------------+
   | Constant                                | Default Value      | Description                                      |
   +=========================================+====================+==================================================+
   | ObsClient.enums.GroupAllUsers           | AllUsers           | All users.                                       |
   +-----------------------------------------+--------------------+--------------------------------------------------+
   | ObsClient.enums.GroupAuthenticatedUsers | AuthenticatedUsers | Authorized users. This constant is deprecated.   |
   +-----------------------------------------+--------------------+--------------------------------------------------+
   | ObsClient.enums.GroupLogDelivery        | LogDelivery        | Log delivery group. This constant is deprecated. |
   +-----------------------------------------+--------------------+--------------------------------------------------+

.. _obs_29_0603__table60165497:

.. table:: **Table 11** PermissionType

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

Code Examples
-------------

This example returns the ACL of object **example/objectname**.

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

   async function getObjectAcl() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify the object (example/objectname in this example).
         Key: 'example/objectname',
       };
       // Obtain the object ACL.
       const result = await obsClient.getObjectAcl(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Get object(%s)'s acl successful with bucket(%s)!", params.Key, params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         console.log('Owner[ID]: %s', result.InterfaceResult.Owner.ID);
         console.log('Owner[Name]: %s', result.InterfaceResult.Owner.Name);
         for (let i = 0; i < result.InterfaceResult.Grants.length; i++) {
           const grant = result.InterfaceResult.Grants[i];
           fmt.Printf("Grant[%d]-Type:%s, ID:%s, URI:%s, Permission:%s\n",
             index, grant.Grantee.Type, grant.Grantee.ID, grant.Grantee.URI, grant.Permission)
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

   getObjectAcl();
