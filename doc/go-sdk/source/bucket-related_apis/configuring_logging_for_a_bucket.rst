:original_name: obs_33_0418.html

.. _obs_33_0418:

Configuring Logging for a Bucket
================================

Function
--------

This API enables logging for a bucket (source) and configures another bucket (target) to store the log files. When a bucket is created, logging is not enabled by default. You can call this API to enable logging for the bucket. With logging enabled, a log message is generated for each operation on the bucket. Multiple log messages are packed into a file. The bucket for storing log files must be specified when logging is enabled. It can be the bucket logging is enabled for, or any other bucket you have access to. If you specify another bucket for storing logs, the bucket must be in the same region as the logged bucket. You can also configure access to log files and the name prefix of log files.

Restrictions
------------

-  OBS creates log files and uploads them to the bucket. Before enabling logging for a bucket, you need to create an IAM agency to delegate OBS to upload log files to the specified bucket.
-  To configure logging for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketLogging** in IAM or **PutBucketLogging** in a bucket policy).

Method
------

**func** (obsClient ObsClient) SetBucketLoggingConfiguration(input \*\ :ref:`SetBucketLoggingConfigurationInput <obs_33_0418__table14455523>`) (output \*\ :ref:`BaseModel <obs_33_0418__table176861118134319>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+----------------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                                       | Mandatory (Yes/No) | Description                                                                                                    |
   +=================+============================================================================+====================+================================================================================================================+
   | input           | \*\ :ref:`SetBucketLoggingConfigurationInput <obs_33_0418__table14455523>` | Yes                | **Explanation:**                                                                                               |
   |                 |                                                                            |                    |                                                                                                                |
   |                 |                                                                            |                    | Input parameters for configuring bucket logging. For details, see :ref:`Table 2 <obs_33_0418__table14455523>`. |
   +-----------------+----------------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------+

.. _obs_33_0418__table14455523:

.. table:: **Table 2** SetBucketLoggingConfigurationInput

   +-----------------+----------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                               | Mandatory (Yes/No)                                                 | Description                                                                                                                                                                                                                                                                        |
   +=================+====================================================+====================================================================+====================================================================================================================================================================================================================================================================================+
   | Bucket          | string                                             | Yes                                                                | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | Bucket name                                                                                                                                                                                                                                                                        |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | **Restrictions:**                                                                                                                                                                                                                                                                  |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                                                                   |
   |                 |                                                    |                                                                    | -  A bucket name:                                                                                                                                                                                                                                                                  |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                                                       |
   |                 |                                                    |                                                                    |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                                                        |
   |                 |                                                    |                                                                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                                                         |
   |                 |                                                    |                                                                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                                                          |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.                                                                                                  |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------+----------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Agency          | string                                             | Yes if the parameter is in a request to enable bucket logging      | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | Name of the IAM agency created by the owner of the target bucket for OBS.                                                                                                                                                                                                          |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | You can select an existing IAM agency or create one.                                                                                                                                                                                                                               |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | **Restrictions:**                                                                                                                                                                                                                                                                  |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | By default, the IAM agency only requires the **PutObject** permission to upload logs to the target bucket. If default encryption is enabled for the target bucket, the agency also requires the **KMS Administrator** permission in the region where the target bucket is located. |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------+----------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetBucket    | string                                             | Yes if you enable logging for the bucket                           | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    | Do not set this parameter when you disable logging for the bucket. | Name of the bucket for storing log files                                                                                                                                                                                                                                           |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | **Restrictions:**                                                                                                                                                                                                                                                                  |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | -  This bucket must be in the same region as the bucket with logging enabled.                                                                                                                                                                                                      |
   |                 |                                                    |                                                                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                                                                   |
   |                 |                                                    |                                                                    | -  A bucket name:                                                                                                                                                                                                                                                                  |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                                                       |
   |                 |                                                    |                                                                    |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                                                        |
   |                 |                                                    |                                                                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                                                         |
   |                 |                                                    |                                                                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                                                          |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.                                                                                                  |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------+----------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetPrefix    | string                                             | Yes if you enable logging for the bucket                           | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    | Do not set this parameter when you disable logging for the bucket. | Name prefix for log files stored in the log storage bucket                                                                                                                                                                                                                         |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | **Value range**:                                                                                                                                                                                                                                                                   |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                                                      |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | **Default value**:                                                                                                                                                                                                                                                                 |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | None                                                                                                                                                                                                                                                                               |
   +-----------------+----------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TargetGrants    | []\ :ref:`Grant <obs_33_0418__table1764402511517>` | No                                                                 | **Explanation:**                                                                                                                                                                                                                                                                   |
   |                 |                                                    |                                                                    |                                                                                                                                                                                                                                                                                    |
   |                 |                                                    |                                                                    | Permission information list of grantees, which defines grantees and their permissions for log files. For details, see :ref:`Table 3 <obs_33_0418__table1764402511517>`.                                                                                                            |
   +-----------------+----------------------------------------------------+--------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0418__table1764402511517:

.. table:: **Table 3** Grant

   +-----------------+----------------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+
   | Parameter       | Type                                                     | Mandatory (Yes/No)                 | Description                                                                           |
   +=================+==========================================================+====================================+=======================================================================================+
   | Grantee         | :ref:`Grantee <obs_33_0418__table94488481611>`           | Yes if used as a request parameter | **Explanation:**                                                                      |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | Grantee information. For details, see :ref:`Table 4 <obs_33_0418__table94488481611>`. |
   +-----------------+----------------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+
   | Permission      | :ref:`PermissionType <obs_33_0418__table18443232202617>` | Yes if used as a request parameter | **Explanation:**                                                                      |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | Granted permission                                                                    |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | **Value range**:                                                                      |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | See :ref:`Table 7 <obs_33_0418__table18443232202617>`.                                |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | **Default value**:                                                                    |
   |                 |                                                          |                                    |                                                                                       |
   |                 |                                                          |                                    | None                                                                                  |
   +-----------------+----------------------------------------------------------+------------------------------------+---------------------------------------------------------------------------------------+

.. _obs_33_0418__table94488481611:

.. table:: **Table 4** Grantee

   +-----------------+------------------------------------------------------+--------------------------------------------+--------------------------------------------------------------------+
   | Parameter       | Type                                                 | Mandatory (Yes/No)                         | Description                                                        |
   +=================+======================================================+============================================+====================================================================+
   | Type            | :ref:`GranteeType <obs_33_0418__table68358509233>`   | Yes                                        | **Explanation:**                                                   |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | Grantee type                                                       |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | **Value range**:                                                   |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | See :ref:`Table 5 <obs_33_0418__table68358509233>`.                |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | **Default value**:                                                 |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | None                                                               |
   +-----------------+------------------------------------------------------+--------------------------------------------+--------------------------------------------------------------------+
   | ID              | string                                               | Yes if **Type** is set to **GranteeUser**  | **Explanation:**                                                   |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | Account (domain) ID of the grantee                                 |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | **Default value**:                                                 |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | None                                                               |
   +-----------------+------------------------------------------------------+--------------------------------------------+--------------------------------------------------------------------+
   | DisplayName     | string                                               | No                                         | **Explanation:**                                                   |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | Account name of the grantee                                        |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | **Restrictions:**                                                  |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | -  Starts with a letter. Contains 6 to 32 characters.              |
   |                 |                                                      |                                            | -  Contains only letters, digits, hyphens (-), or underscores (_). |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | **Default value**:                                                 |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | None                                                               |
   +-----------------+------------------------------------------------------+--------------------------------------------+--------------------------------------------------------------------+
   | URI             | :ref:`GroupUriType <obs_33_0418__table715045462318>` | Yes if **Type** is set to **GranteeGroup** | **Explanation:**                                                   |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | Authorized user group                                              |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | **Value range**:                                                   |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | See :ref:`Table 6 <obs_33_0418__table715045462318>`.               |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | **Default value**:                                                 |
   |                 |                                                      |                                            |                                                                    |
   |                 |                                                      |                                            | None                                                               |
   +-----------------+------------------------------------------------------+--------------------------------------------+--------------------------------------------------------------------+

.. _obs_33_0418__table68358509233:

.. table:: **Table 5** GranteeType

   ============ ============= ===============
   Constant     Default Value Description
   ============ ============= ===============
   GranteeGroup Group         User group
   GranteeUser  CanonicalUser Individual user
   ============ ============= ===============

.. _obs_33_0418__table715045462318:

.. table:: **Table 6** GroupUriType

   ============= ============= ===========
   Constant      Default Value Description
   ============= ============= ===========
   GroupAllUsers AllUsers      All users
   ============= ============= ===========

.. _obs_33_0418__table18443232202617:

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

Responses
---------

.. table:: **Table 8** List of returned results

   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------+
   | Parameter             | Type                                                     | Description                                                                            |
   +=======================+==========================================================+========================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0418__table176861118134319>` | **Explanation:**                                                                       |
   |                       |                                                          |                                                                                        |
   |                       |                                                          | Returned results. For details, see :ref:`Table 9 <obs_33_0418__table176861118134319>`. |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------+
   | err                   | error                                                    | **Explanation:**                                                                       |
   |                       |                                                          |                                                                                        |
   |                       |                                                          | Error messages returned by the API                                                     |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------+

.. _obs_33_0418__table176861118134319:

.. table:: **Table 9** BaseModel

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

This example configures logging for bucket **examplebucket**, with **obs_test_agency** as the agency, **TargetPrefixtest/** as the prefix for generated log files, and **TargetBucketname** as the bucket for storing log files.

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
       input := &obs.SetBucketLoggingConfigurationInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify an agency name (obs_test_agency as an example).
       input.Agency = "obs_test_agency"
       // Specify a bucket (TargetBucketname as an example) for storing generated log files.
       input.TargetBucket = "TargetBucketname"
       // Specify a prefix (TargetPrefixtest/ as an example) for log files to be generated.
       input.TargetPrefix = "TargetPrefixtest/"
       // Configure logging for the bucket.
       output, err := obsClient.SetBucketLoggingConfiguration(input)
       if err == nil {
           fmt.Printf("Set bucket(%s)'s logging configuration successful!\n", input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Set bucket(%s)'s logging configuration fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
