:original_name: obs_21_1503.html

.. _obs_21_1503:

Obtaining the Logging Configuration of a Bucket
===============================================

Function
--------

This API returns the logging configuration of a bucket.

Restrictions
------------

-  To obtain the logging configuration of a bucket, you must be the bucket owner or have the required permission (**obs:bucket:GetBucketLogging** in IAM or **GetBucketLogging** in a bucket policy).

Method
------

obsClient.getBucketLogging(final :ref:`BaseBucketRequest <obs_21_1503__table43960571>` :ref:`request <obs_21_1503__table72121329103020>`)

Request Parameters
------------------

.. _obs_21_1503__table72121329103020:

.. table:: **Table 1** List of request parameters

   +-----------------+-------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                  | Mandatory (Yes/No) | Description                                                                                                                            |
   +=================+=======================================================+====================+========================================================================================================================================+
   | request         | :ref:`BaseBucketRequest <obs_21_1503__table43960571>` | Yes                | **Explanation:**                                                                                                                       |
   |                 |                                                       |                    |                                                                                                                                        |
   |                 |                                                       |                    | Request parameters for obtaining the logging configurations of a bucket. For details, see :ref:`Table 2 <obs_21_1503__table43960571>`. |
   +-----------------+-------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1503__table43960571:

.. table:: **Table 2** BaseBucketRequest

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

.. table:: **Table 3** BucketLoggingConfiguration

   +------------------+-------------------------------------------------------------------+-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Type                                                              | Mandatory (Yes/No)                  | Description                                                                                                                                                                                                                                                                        |
   +==================+===================================================================+=====================================+====================================================================================================================================================================================================================================================================================+
   | agency           | String                                                            | Yes if you configure bucket logging | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | Name of the IAM agency created by the owner of the target bucket for OBS.                                                                                                                                                                                                          |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | You can select an existing IAM agency or create one.                                                                                                                                                                                                                               |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | **Restrictions:**                                                                                                                                                                                                                                                                  |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | By default, the IAM agency only requires the **PutObject** permission to upload logs to the target bucket. If default encryption is enabled for the target bucket, the agency also requires the **KMS Administrator** permission in the region where the target bucket is located. |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | **Default value**:                                                                                                                                                                                                                                                                 |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | None                                                                                                                                                                                                                                                                               |
   +------------------+-------------------------------------------------------------------+-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | targetBucketName | String                                                            | No                                  | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | Name of the bucket for storing log files.                                                                                                                                                                                                                                          |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | **Restrictions:**                                                                                                                                                                                                                                                                  |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | -  This bucket must be in the same region as the bucket with logging enabled.                                                                                                                                                                                                      |
   |                  |                                                                   |                                     | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                                                                   |
   |                  |                                                                   |                                     | -  A bucket name:                                                                                                                                                                                                                                                                  |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                                                       |
   |                  |                                                                   |                                     |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                                                        |
   |                  |                                                                   |                                     |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                                                         |
   |                  |                                                                   |                                     |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                                                                    |
   |                  |                                                                   |                                     |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                                                            |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.                                                                                                  |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | **Default value**:                                                                                                                                                                                                                                                                 |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | None                                                                                                                                                                                                                                                                               |
   +------------------+-------------------------------------------------------------------+-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | logfilePrefix    | String                                                            | No                                  | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | Name prefix for log files stored in the target bucket.                                                                                                                                                                                                                             |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | **Value range**:                                                                                                                                                                                                                                                                   |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                                                      |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | **Default value**:                                                                                                                                                                                                                                                                 |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | None                                                                                                                                                                                                                                                                               |
   +------------------+-------------------------------------------------------------------+-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | targetGrantsList | List<:ref:`GrantAndPermission <obs_21_1503__table1966620295123>`> | No                                  | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                  |                                                                   |                                     |                                                                                                                                                                                                                                                                                    |
   |                  |                                                                   |                                     | Permission information list of grantees, which defines grantees and their permissions for log files. For details, see :ref:`Table 4 <obs_21_1503__table1966620295123>`.                                                                                                            |
   +------------------+-------------------------------------------------------------------+-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1503__table1966620295123:

.. table:: **Table 4** GrantAndPermission

   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                       | Mandatory (Yes/No) | Description                                                                                          |
   +=================+============================================================+====================+======================================================================================================+
   | grantee         | :ref:`GranteeInterface <obs_21_1503__table16903171143518>` | Yes                | **Explanation:**                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | Grantees (users or user groups). For details, see :ref:`Table 5 <obs_21_1503__table16903171143518>`. |
   +-----------------+------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------+
   | permission      | :ref:`Permission <obs_21_1503__table17475749161815>`       | Yes                | **Explanation:**                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | Permissions to grant.                                                                                |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | **Value range**:                                                                                     |
   |                 |                                                            |                    |                                                                                                      |
   |                 |                                                            |                    | See :ref:`Table 8 <obs_21_1503__table17475749161815>`.                                               |
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

.. _obs_21_1503__table16903171143518:

.. table:: **Table 5** GranteeInterface

   +---------------------------------------------------------+---------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | Parameter                                               | Type                                                    | Mandatory (Yes/No) | Description                                                                                  |
   +=========================================================+=========================================================+====================+==============================================================================================+
   | :ref:`CanonicalGrantee <obs_21_1503__table94488481611>` | :ref:`CanonicalGrantee <obs_21_1503__table94488481611>` | Yes                | **Explanation:**                                                                             |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | Grantee (user) information. For details, see :ref:`Table 6 <obs_21_1503__table94488481611>`. |
   +---------------------------------------------------------+---------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+
   | :ref:`GroupGrantee <obs_21_1503__table9881261176>`      | :ref:`GroupGrantee <obs_21_1503__table9881261176>`      | Yes                | **Explanation:**                                                                             |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | Grantee (user group) information.                                                            |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | **Value range**:                                                                             |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | See :ref:`Table 7 <obs_21_1503__table9881261176>`.                                           |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | **Default value**:                                                                           |
   |                                                         |                                                         |                    |                                                                                              |
   |                                                         |                                                         |                    | None                                                                                         |
   +---------------------------------------------------------+---------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------+

.. _obs_21_1503__table94488481611:

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

.. _obs_21_1503__table9881261176:

.. table:: **Table 7** GroupGrantee

   =================== ================================================
   Constant            Description
   =================== ================================================
   ALL_USERS           All users.
   AUTHENTICATED_USERS Authorized users. This constant is deprecated.
   LOG_DELIVERY        Log delivery group. This constant is deprecated.
   =================== ================================================

.. _obs_21_1503__table17475749161815:

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

This example returns the logging configuration of bucket **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.BucketLoggingConfiguration;
   public class GetBucketLogging001 {
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
               // View the bucket logging configuration.
               BucketLoggingConfiguration config = obsClient.getBucketLogging("examplebucket");
               System.out.println("TargetBucketName:" + config.getTargetBucketName());
               System.out.println("LogfilePrefix:" + config.getLogfilePrefix());
               System.out.println("getBucketLogging successfully");
           } catch (ObsException e) {
               System.out.println("getBucketLogging failed");
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
               System.out.println("getBucketLogging failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
