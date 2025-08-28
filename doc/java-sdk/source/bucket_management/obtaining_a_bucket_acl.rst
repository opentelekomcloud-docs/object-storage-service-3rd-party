:original_name: obs_21_0412.html

.. _obs_21_0412:

Obtaining a Bucket ACL
======================

Function
--------

Access control lists (ACLs) allow resource owners to grant other accounts the permissions to access resources. By default, only the resource owner has full control over resources when a bucket or object is created. That is, the bucket creator has full control over the bucket, and the object uploader has full control over the object. Other accounts do not have the permissions to access resources. If resource owners want to grant other accounts the read and write permissions on resources, they can use ACLs. ACLs grant permissions to accounts. After an account is granted permissions, both the account and its IAM users can access the resources.

This API returns the ACL of a bucket.

Restrictions
------------

-  To obtain the ACL of a bucket, you must be the bucket owner or have the required permission (**obs:bucket:GetBucketAcl** in IAM or **GetBucketAcl** in a bucket policy).

Method
------

obsClient.getBucketAcl(String :ref:`bucketName <obs_21_0412__table47625841>`)

Request Parameters
------------------

.. _obs_21_0412__table47625841:

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=================+====================+===================================================================================================================================================================================+
   | bucketName      | String          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Bucket name.                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                 |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 2** AccessControlList

   +-----------------+------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                             | Mandatory (Yes/No) | Type                                                                                         |
   +=================+==================================================================+====================+==============================================================================================+
   | owner           | :ref:`Owner <obs_21_0412__table1183415419527>`                   | Yes                | **Explanation:**                                                                             |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | Bucket owner information. For details, see :ref:`Table 3 <obs_21_0412__table1183415419527>`. |
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
   | grants          | Set<:ref:`GrantAndPermission <obs_21_0412__table1966620295123>`> | No                 | **Explanation:**                                                                             |
   |                 |                                                                  |                    |                                                                                              |
   |                 |                                                                  |                    | Grantee information. For details, see :ref:`Table 4 <obs_21_0412__table1966620295123>`.      |
   +-----------------+------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+

.. _obs_21_0412__table1183415419527:

.. table:: **Table 3** Owner

   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                  |
   +=================+=================+====================+==============================================================================================+
   | id              | String          | Yes                | **Explanation:**                                                                             |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | Account (domain) ID of the owner.                                                            |
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

.. _obs_21_0412__table1966620295123:

.. table:: **Table 4** GrantAndPermission

   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                       | Mandatory (Yes/No) | Description                                                                                          |
   +=================+============================================================+====================+======================================================================================================+
   | grantee         | :ref:`GranteeInterface <obs_21_0412__table16903171143518>` | Yes                | **Explanation:**                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | Grantees (users or user groups). For details, see :ref:`Table 5 <obs_21_0412__table16903171143518>`. |
   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------+
   | permission      | :ref:`Permission <obs_21_0412__table17475749161815>`       | Yes                | **Explanation:**                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | Permissions to grant.                                                                                |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | **Value range**:                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | See :ref:`Table 8 <obs_21_0412__table17475749161815>`.                                               |
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

.. _obs_21_0412__table16903171143518:

.. table:: **Table 5** GranteeInterface

   +---------------------------------------------------------+---------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | Parameter                                               | Type                                                    | Mandatory (Yes/No) | Description                                                                                  |
   +=========================================================+=========================================================+====================+==============================================================================================+
   | :ref:`CanonicalGrantee <obs_21_0412__table94488481611>` | :ref:`CanonicalGrantee <obs_21_0412__table94488481611>` | Yes                | **Explanation:**                                                                             |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | Grantee (user) information. For details, see :ref:`Table 6 <obs_21_0412__table94488481611>`. |
   +---------------------------------------------------------+---------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | :ref:`GroupGrantee <obs_21_0412__table9881261176>`      | :ref:`GroupGrantee <obs_21_0412__table9881261176>`      | Yes                | **Explanation:**                                                                             |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | Grantee (user group) information.                                                            |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | **Value range**:                                                                             |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | See :ref:`Table 7 <obs_21_0412__table9881261176>`.                                           |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | **Default value**:                                                                           |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | None                                                                                         |
   +---------------------------------------------------------+---------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+

.. _obs_21_0412__table94488481611:

.. table:: **Table 6** CanonicalGrantee

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

.. _obs_21_0412__table9881261176:

.. table:: **Table 7** GroupGrantee

   =================== ================================================
   Constant            Description
   =================== ================================================
   ALL_USERS           All users.
   AUTHENTICATED_USERS Authorized users. This constant is deprecated.
   LOG_DELIVERY        Log delivery group. This constant is deprecated.
   =================== ================================================

.. _obs_21_0412__table17475749161815:

.. table:: **Table 8** Permission

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

Code Examples
-------------

This example obtains the ACL of the **examplebucket** bucket.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.AccessControlList;
   public class GetBucketAcl001 {
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
               // Example bucket name
               String exampleBucket = "examplebucket";
               //Obtain the bucket ACL.
               AccessControlList acl = obsClient.getBucketAcl(exampleBucket);
               System.out.println("GetBucketAcl successfully");
               System.out.println(acl);
           } catch (ObsException e) {
               System.out.println("GetBucketAcl failed");
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
               System.out.println("GetBucketAcl failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
