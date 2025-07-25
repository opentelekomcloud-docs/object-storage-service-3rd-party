:original_name: obs_33_0416.html

.. _obs_33_0416:

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

**func** (obsClient ObsClient) SetBucketAcl(input \*\ :ref:`SetBucketAclInput <obs_33_0416__table14455523>`) (output \*\ :ref:`BaseModel <obs_33_0416__table11884741191716>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                      | Mandatory (Yes/No) | Description                                                                                                  |
   +=================+===========================================================+====================+==============================================================================================================+
   | input           | \*\ :ref:`SetBucketAclInput <obs_33_0416__table14455523>` | Yes                | **Explanation:**                                                                                             |
   |                 |                                                           |                    |                                                                                                              |
   |                 |                                                           |                    | Input parameters for configuring a bucket ACL. For details, see :ref:`Table 2 <obs_33_0416__table14455523>`. |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------+

.. _obs_33_0416__table14455523:

.. table:: **Table 2** SetBucketAclInput

   +-----------------+-------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=================================================+====================+===================================================================================================================================================================================+
   | Bucket          | string                                          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | Bucket name                                                                                                                                                                       |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                 |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                 |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | None                                                                                                                                                                              |
   +-----------------+-------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ACL             | :ref:`AclType <obs_33_0416__table881141715520>` | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | Pre-defined ACL.                                                                                                                                                                  |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | See :ref:`Table 3 <obs_33_0416__table881141715520>`.                                                                                                                              |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | None                                                                                                                                                                              |
   +-----------------+-------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner           | :ref:`Owner <obs_33_0416__table1183415419527>`  | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | ID of the bucket owner. For details, see :ref:`Table 4 <obs_33_0416__table1183415419527>`.                                                                                        |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | **Owner** and **Grants** must be used together and they cannot be used with **ACL**.                                                                                              |
   +-----------------+-------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Grants          | :ref:`Grant <obs_33_0416__table1764402511517>`  | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                 |                    |                                                                                                                                                                                   |
   |                 |                                                 |                    | Grantees' permission information. For details, see :ref:`Table 5 <obs_33_0416__table1764402511517>`.                                                                              |
   +-----------------+-------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0416__table881141715520:

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

.. _obs_33_0416__table1183415419527:

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

.. _obs_33_0416__table1764402511517:

.. table:: **Table 5** Grant

   +-----------------+----------------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+
   | Parameter       | Type                                                     | Mandatory (Yes/No)                 | Description                                                                           |
   +=================+==========================================================+====================================+=======================================================================================+
   | Grantee         | :ref:`Grantee <obs_33_0416__table94488481611>`           | Yes if used as a request parameter | **Explanation:**                                                                      |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | Grantee information. For details, see :ref:`Table 6 <obs_33_0416__table94488481611>`. |
   +-----------------+----------------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+
   | Permission      | :ref:`PermissionType <obs_33_0416__table17475749161815>` | Yes if used as a request parameter | **Explanation:**                                                                      |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | Granted permission                                                                    |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | **Value range**:                                                                      |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | See :ref:`Table 8 <obs_33_0416__table17475749161815>`.                                |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | **Default value**:                                                                    |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | None                                                                                  |
   +-----------------+----------------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+

.. _obs_33_0416__table94488481611:

.. table:: **Table 6** Grantee

   +-----------------+------------------------------------------------------+---------------------------------------------------------------------------------------------+--------------------------------------------------------------------+
   | Parameter       | Type                                                 | Mandatory (Yes/No)                                                                          | Description                                                        |
   +=================+======================================================+=============================================================================================+====================================================================+
   | Type            | :ref:`GranteeType <obs_33_0416__table1360510402162>` | Yes if used as a request parameter                                                          | **Explanation:**                                                   |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | Grantee type                                                       |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | **Value range**:                                                   |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | See :ref:`Table 7 <obs_33_0416__table1360510402162>`.              |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | **Default value**:                                                 |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | None                                                               |
   +-----------------+------------------------------------------------------+---------------------------------------------------------------------------------------------+--------------------------------------------------------------------+
   | ID              | string                                               | Yes if this parameter is used as a request parameter and **Type** is set to **GranteeUser** | **Explanation:**                                                   |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | Account (domain) ID of the grantee                                 |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | **Default value**:                                                 |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | None                                                               |
   +-----------------+------------------------------------------------------+---------------------------------------------------------------------------------------------+--------------------------------------------------------------------+
   | DisplayName     | string                                               | No if used as a request parameter                                                           | **Explanation:**                                                   |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | Account name of the grantee                                        |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | **Restrictions:**                                                  |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | -  Starts with a letter.                                           |
   |                 |                                                      |                                                                                             | -  Contains 6 to 32 characters.                                    |
   |                 |                                                      |                                                                                             | -  Contains only letters, digits, hyphens (-), or underscores (_). |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | **Default value**:                                                 |
   |                 |                                                      |                                                                                             |                                                                    |
   |                 |                                                      |                                                                                             | None                                                               |
   +-----------------+------------------------------------------------------+---------------------------------------------------------------------------------------------+--------------------------------------------------------------------+

.. _obs_33_0416__table1360510402162:

.. table:: **Table 7** GranteeType

   ============ ============= ===============
   Constant     Default Value Description
   ============ ============= ===============
   GranteeGroup Group         User group
   GranteeUser  CanonicalUser Individual user
   ============ ============= ===============

.. _obs_33_0416__table17475749161815:

.. table:: **Table 8** PermissionType

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

Responses
---------

.. table:: **Table 9** List of returned results

   +-----------------------+---------------------------------------------------------+----------------------------------------------------------------------------------------+
   | Parameter             | Type                                                    | Description                                                                            |
   +=======================+=========================================================+========================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0416__table11884741191716>` | **Explanation:**                                                                       |
   |                       |                                                         |                                                                                        |
   |                       |                                                         | Returned results. For details, see :ref:`Table 10 <obs_33_0416__table11884741191716>`. |
   +-----------------------+---------------------------------------------------------+----------------------------------------------------------------------------------------+
   | err                   | error                                                   | **Explanation:**                                                                       |
   |                       |                                                         |                                                                                        |
   |                       |                                                         | Error messages returned by the API                                                     |
   +-----------------------+---------------------------------------------------------+----------------------------------------------------------------------------------------+

.. _obs_33_0416__table11884741191716:

.. table:: **Table 10** BaseModel

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

This example sets the ACL of bucket **examplebucket** to Private.

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
       //securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint, obs.WithSecurityToken(securityToken))
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.SetBucketAclInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Set the bucket ACL to be private.
       input.ACL = obs.AclPrivate
       // Configure the bucket ACL.
       output, err := obsClient.SetBucketAcl(input)
       if err == nil {
           fmt.Printf("Set bucket(%s)'s acl successful!\n", input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Set bucket(%s)'s acl fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
