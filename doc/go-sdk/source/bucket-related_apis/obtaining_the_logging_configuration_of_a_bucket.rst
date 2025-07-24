:original_name: obs_33_0419.html

.. _obs_33_0419:

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

**func** (obsClient ObsClient) GetBucketLoggingConfiguration(:ref:`bucketName <obs_33_0419>` string) (output \*\ :ref:`GetBucketLoggingConfigurationOutput <obs_33_0419__table14455523>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=================+====================+===================================================================================================================================================================================+
   | bucketName      | string          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Bucket name                                                                                                                                                                       |
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
   |                 |                 |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 2** List of returned results

   +-----------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------------------+
   | Parameter             | Type                                                                        | Description                                                                     |
   +=======================+=============================================================================+=================================================================================+
   | output                | \*\ :ref:`GetBucketLoggingConfigurationOutput <obs_33_0419__table14455523>` | **Explanation:**                                                                |
   |                       |                                                                             |                                                                                 |
   |                       |                                                                             | Returned results. For details, see :ref:`Table 3 <obs_33_0419__table14455523>`. |
   +-----------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------------------+
   | err                   | error                                                                       | **Explanation:**                                                                |
   |                       |                                                                             |                                                                                 |
   |                       |                                                                             | Error messages returned by the API                                              |
   +-----------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------------------+

.. _obs_33_0419__table14455523:

.. table:: **Table 3** GetBucketLoggingConfigurationOutput

   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                               | Description                                                                                                                                                                                                                                                                        |
   +=======================+====================================================+====================================================================================================================================================================================================================================================================================+
   | StatusCode            | int                                                | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | HTTP status code                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Value range**:                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response.                                                                                                        |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                                             | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | Request ID returned by the OBS server                                                                                                                                                                                                                                              |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ResponseHeaders       | map[string][]string                                | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | HTTP response headers                                                                                                                                                                                                                                                              |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Agency                | string                                             | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | Name of the IAM agency created by the owner of the target bucket for OBS.                                                                                                                                                                                                          |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | You can select an existing IAM agency or create one.                                                                                                                                                                                                                               |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Restrictions:**                                                                                                                                                                                                                                                                  |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | By default, the IAM agency only requires the **PutObject** permission to upload logs to the target bucket. If default encryption is enabled for the target bucket, the agency also requires the **KMS Administrator** permission in the region where the target bucket is located. |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetBucket          | string                                             | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | Name of the bucket for storing log files                                                                                                                                                                                                                                           |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Restrictions:**                                                                                                                                                                                                                                                                  |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | -  This bucket must be in the same region as the bucket with logging enabled.                                                                                                                                                                                                      |
   |                       |                                                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                                                                   |
   |                       |                                                    | -  A bucket name:                                                                                                                                                                                                                                                                  |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                                                       |
   |                       |                                                    |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                                                        |
   |                       |                                                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                                                         |
   |                       |                                                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                                                                    |
   |                       |                                                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                                                          |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.                                                                                                  |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetPrefix          | string                                             | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | Name prefix for log files stored in the log storage bucket                                                                                                                                                                                                                         |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Value range**:                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                                                      |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetGrants          | []\ :ref:`Grant <obs_33_0419__table1764402511517>` | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                       |                                                    |                                                                                                                                                                                                                                                                                    |
   |                       |                                                    | Permission information list of grantees, which defines grantees and their permissions for log files. For details, see :ref:`Table 4 <obs_33_0419__table1764402511517>`.                                                                                                            |
   +-----------------------+----------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0419__table1764402511517:

.. table:: **Table 4** Grant

   +-----------------------+----------------------------------------------------------+---------------------------------------------------------------------------------------+
   | Parameter             | Type                                                     | Description                                                                           |
   +=======================+==========================================================+=======================================================================================+
   | Grantee               | :ref:`Grantee <obs_33_0419__table94488481611>`           | **Explanation:**                                                                      |
   |                       |                                                          |                                                                                       |
   |                       |                                                          | Grantee information. For details, see :ref:`Table 5 <obs_33_0419__table94488481611>`. |
   +-----------------------+----------------------------------------------------------+---------------------------------------------------------------------------------------+
   | Permission            | :ref:`PermissionType <obs_33_0419__table18443232202617>` | **Explanation:**                                                                      |
   |                       |                                                          |                                                                                       |
   |                       |                                                          | Granted permission                                                                    |
   |                       |                                                          |                                                                                       |
   |                       |                                                          | **Value range**:                                                                      |
   |                       |                                                          |                                                                                       |
   |                       |                                                          | See :ref:`Table 8 <obs_33_0419__table18443232202617>`.                                |
   |                       |                                                          |                                                                                       |
   |                       |                                                          | **Default value**:                                                                    |
   |                       |                                                          |                                                                                       |
   |                       |                                                          | None                                                                                  |
   +-----------------------+----------------------------------------------------------+---------------------------------------------------------------------------------------+

.. _obs_33_0419__table94488481611:

.. table:: **Table 5** Grantee

   +-----------------------+------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                 | Description                                                                                |
   +=======================+======================================================+============================================================================================+
   | Type                  | :ref:`GranteeType <obs_33_0419__table68358509233>`   | **Explanation:**                                                                           |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | Grantee type                                                                               |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | **Value range**:                                                                           |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | See :ref:`Table 6 <obs_33_0419__table68358509233>`.                                        |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | **Default value**:                                                                         |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | None                                                                                       |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | ID                    | string                                               | **Explanation:**                                                                           |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | Account (domain) ID of the grantee                                                         |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | **Value range**:                                                                           |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>` |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | **Default value**:                                                                         |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | None                                                                                       |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | DisplayName           | string                                               | **Explanation:**                                                                           |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | Account name of the grantee                                                                |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | **Restrictions:**                                                                          |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | -  Starts with a letter. Contains 6 to 32 characters.                                      |
   |                       |                                                      | -  Contains only letters, digits, hyphens (-), or underscores (_).                         |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | **Default value**:                                                                         |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | None                                                                                       |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------------------------------------------+
   | URI                   | :ref:`GroupUriType <obs_33_0419__table715045462318>` | **Explanation:**                                                                           |
   |                       |                                                      |                                                                                            |
   |                       |                                                      | Authorized user group. For details, see :ref:`Table 7 <obs_33_0419__table715045462318>`.   |
   +-----------------------+------------------------------------------------------+--------------------------------------------------------------------------------------------+

.. _obs_33_0419__table68358509233:

.. table:: **Table 6** GranteeType

   ============ ============= ===============
   Constant     Default Value Description
   ============ ============= ===============
   GranteeGroup Group         User group
   GranteeUser  CanonicalUser Individual user
   ============ ============= ===============

.. _obs_33_0419__table715045462318:

.. table:: **Table 7** GroupUriType

   ============= ============= ===========
   Constant      Default Value Description
   ============= ============= ===========
   GroupAllUsers AllUsers      All users
   ============= ============= ===========

.. _obs_33_0419__table18443232202617:

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

Code Examples
-------------

This example returns the logging configuration of bucket **examplebucket**.

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
       // securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint, obs.WithSignature(obs.SignatureObs)/*, obs.WithSecurityToken(securityToken)*/)
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       // Specify a bucket name.
       bucketname := "examplebucket"
       // Obtain the logging configuration of the bucket.
       output, err := obsClient.GetBucketLoggingConfiguration(bucketname)
       if err == nil {
           fmt.Printf("Get bucket(%s)'s BucketLoggingConfiguration successful!\n", bucketname)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           fmt.Printf("TargetBucket:%s, TargetPrefix:%s\n", output.TargetBucket, output.TargetPrefix)
           for index, grant := range output.TargetGrants {
               fmt.Printf("Grant[%d]-Type:%s, ID:%s, URI:%s, Permission:%s\n",
                   index, grant.Grantee.Type, grant.Grantee.ID, grant.Grantee.URI, grant.Permission)
           }
           return
       }
       fmt.Printf("Get bucket(%s)'s BucketLoggingConfiguration fail!\n", bucketname)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
