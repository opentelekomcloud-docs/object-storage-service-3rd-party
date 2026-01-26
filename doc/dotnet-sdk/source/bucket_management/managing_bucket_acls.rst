:original_name: obs_25_0306.html

.. _obs_25_0306:

Managing Bucket ACLs
====================

Access control lists (ACLs) allow resource owners to grant other accounts the permissions to access resources. By default, only the resource owner has full control over resources when a bucket or object is created. That is, the bucket creator has full control over the bucket, and the object uploader has full control over the object. Other accounts do not have the permissions to access resources. If resource owners want to grant other accounts the read and write permissions on resources, they can use ACLs. ACLs grant permissions to accounts. After an account is granted permissions, both the account and its IAM users can access the resources.

A bucket ACL can be configured in any of the following ways:

#. Specify a pre-defined ACL when creating a bucket.
#. Call ObsClient.SetBucketAcl to specify a pre-defined ACL.
#. Call ObsClient.SetBucketAcl to specify a user-defined ACL.

The following table lists the five permission types supported by OBS.

+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+----------------------------+
| Permission            | Description                                                                                                                       | Value in OBS .NET SDK      |
+=======================+===================================================================================================================================+============================+
| READ                  | A grantee with this permission for a bucket can obtain the list of objects in the bucket and the metadata of the bucket.          | PermissionEnum.Read        |
|                       |                                                                                                                                   |                            |
|                       | A grantee with this permission for an object can obtain the object content and metadata.                                          |                            |
+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+----------------------------+
| WRITE                 | A grantee with this permission for a bucket can upload, overwrite, and delete any object in the bucket.                           | PermissionEnum.Write       |
|                       |                                                                                                                                   |                            |
|                       | Such permission for an object is not applicable.                                                                                  |                            |
+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+----------------------------+
| READ_ACP              | A grantee with this permission can obtain the ACL of a bucket or object.                                                          | PermissionEnum.ReadAcp     |
|                       |                                                                                                                                   |                            |
|                       | A bucket or object owner has this permission permanently.                                                                         |                            |
+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+----------------------------+
| WRITE_ACP             | A grantee with this permission can update the ACL of a bucket or object.                                                          | PermissionEnum.WriteAcp    |
|                       |                                                                                                                                   |                            |
|                       | A bucket or object owner has this permission permanently.                                                                         |                            |
|                       |                                                                                                                                   |                            |
|                       | A grantee with this permission can modify the access control policy and thus the grantee obtains full access permissions.         |                            |
+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+----------------------------+
| FULL_CONTROL          | A grantee with this permission for a bucket has **READ**, **WRITE**, **READ_ACP**, and **WRITE_ACP** permissions for the bucket.  | PermissionEnum.FullControl |
|                       |                                                                                                                                   |                            |
|                       | A grantee with this permission for an object has **READ**, **WRITE**, **READ_ACP**, and **WRITE_ACP** permissions for the object. |                            |
+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+----------------------------+

There are five access control policies pre-defined in OBS, as described in the following table:

+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
| Policy                      | Description                                                                                                                                                                                                                                                                                                                                   | Value in OBS .NET SDK                  |
+=============================+===============================================================================================================================================================================================================================================================================================================================================+========================================+
| private                     | The owner of a bucket or object has the **FULL_CONTROL** permission for the bucket or object. Other users have no permission to access the bucket or object.                                                                                                                                                                                  | CannedAclEnum.Private                  |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
| public-read                 | If this permission is set for a bucket, everyone can obtain the list of objects, multipart uploads, and object versions in the bucket, as well as metadata of the bucket.                                                                                                                                                                     | CannedAclEnum.PublicRead               |
|                             |                                                                                                                                                                                                                                                                                                                                               |                                        |
|                             | If this permission is set for an object, everyone can obtain the content and metadata of the object.                                                                                                                                                                                                                                          |                                        |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
| public-read-write           | If this permission is set for a bucket, everyone can obtain the object list in the bucket, multipart uploads in the bucket, metadata of the bucket; upload objects; delete objects; initialize multipart uploads; upload parts; combine parts; copy parts; and abort multipart uploads.                                                       | CannedAclEnum.PublicReadWrite          |
|                             |                                                                                                                                                                                                                                                                                                                                               |                                        |
|                             | If this permission is set for an object, everyone can obtain the content and metadata of the object.                                                                                                                                                                                                                                          |                                        |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
| public-read-delivered       | If this permission is set for a bucket, everyone can obtain the object list, multipart uploads, and bucket metadata in the bucket, and obtain the content and metadata of the objects in the bucket.                                                                                                                                          | CannedAclEnum.PublicReadDelivered      |
|                             |                                                                                                                                                                                                                                                                                                                                               |                                        |
|                             | This permission cannot be set for objects.                                                                                                                                                                                                                                                                                                    |                                        |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+
| public-read-write-delivered | If this permission is set for a bucket, everyone can obtain the object list in the bucket, multipart uploads in the bucket, metadata of the bucket; upload objects; delete objects; initialize multipart uploads; upload parts; combine parts; copy parts; abort multipart uploads; and obtain content and metadata of objects in the bucket. | CannedAclEnum.PublicReadWriteDelivered |
|                             |                                                                                                                                                                                                                                                                                                                                               |                                        |
|                             | This permission cannot be set for objects.                                                                                                                                                                                                                                                                                                    |                                        |
+-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------+

Specifying a Pre-defined ACL During Bucket Creation
---------------------------------------------------

Sample code:

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an instance of ObsClient.
   ObsClient client = new ObsClient(accessKey, secretKey, config);
   // Create a bucket.
   try
   {
       CreateBucketRequest request = new CreateBucketRequest
       {
           BucketName = "bucketname",
           // Set the bucket ACL to public read and write.
           CannedAcl = CannedAclEnum.PublicReadWrite,
       };
       CreateBucketResponse response = client.CreateBucket(request);
       Console.WriteLine("StatusCode: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Setting a Pre-defined ACL for a Bucket
--------------------------------------

Sample code:

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an instance of ObsClient.
   ObsClient client = new ObsClient(accessKey, secretKey, config);
   //Set the bucket ACL.
   try
   {
       SetBucketAclRequest request = new SetBucketAclRequest
       {
           BucketName = "bucketname",
           // Set the bucket ACL to be private.
           CannedAcl = CannedAclEnum.Private
       };
       SetBucketAclResponse response = client.SetBucketAcl(request);
       Console.WriteLine("Set bucket acl response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Setting a User-defined Bucket ACL
---------------------------------

The following code shows how to set a user-defined ACL for a bucket:

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an instance of ObsClient.
   ObsClient client = new ObsClient(accessKey, secretKey, config);
   //Set the bucket ACL.
   try
   {
       //Set the bucket owner.
       Owner owner = new Owner
       {
           Id = "ownerid",//ID of the domain to which the owner belongs
       };
       AccessControlList acl = new AccessControlList();
       acl.Owner = owner ;

       Grant item = new Grant()
       {
           Grantee = new GroupGrantee()
           {
               GroupGranteeType = GroupGranteeEnum.AllUsers
           },
           Permission = PermissionEnum.FullControl
       };

       IList<Grant> grants = new List<Grant>();
       grants.Add(item);
       acl.Grants = grants;

       SetBucketAclRequest request = new SetBucketAclRequest()
       {
           BucketName = "bucketname",
           AccessControlList = acl
       };

       SetBucketAclResponse response = client.SetBucketAcl(request);
       Console.WriteLine("Set bucket acl response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   The owner or grantee ID needed in the ACL indicates the account ID, which can be viewed on the **My Credentials** page of OBS Console.

Obtaining a Bucket ACL
----------------------

You can call ObsClient.GetBucketAcl to obtain the bucket ACL. Sample code is as follows:

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an instance of ObsClient.
   ObsClient client = new ObsClient(accessKey, secretKey, config);
   //Obtain the bucket ACL.
   try
   {
       GetBucketAclRequest request = new GetBucketAclRequest
       {
           BucketName = "bucketname",
       };
       GetBucketAclResponse response = client.GetBucketAcl(request);
       Console.WriteLine("Get bucket acl response: {0}", response.StatusCode);
       foreach(Grant grant in response.AccessControlList.Grants)
       {
           if(grant.Grantee is CanonicalGrantee)
           {
                 Console.WriteLine("Grantee id: {0}", (grant.Grantee as CanonicalGrantee).Id);
           }else if(grant.Grantee is GroupGrantee)
           {
                 Console.WriteLine("Grantee type: {0}", (grant.Grantee as GroupGrantee).GroupGranteeType);
           }
                 Console.WriteLine("Grant permission: {0}", grant.Permission);
           }
       }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
