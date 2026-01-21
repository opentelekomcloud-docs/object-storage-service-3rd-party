:original_name: obs_25_0602.html

.. _obs_25_0602:

Managing Object ACLs
====================

Access control lists (ACLs) allow resource owners to grant other accounts the permissions to access resources. By default, only the resource owner has full control over resources when a bucket or object is created. That is, the bucket creator has full control over the bucket, and the object uploader has full control over the object. Other accounts do not have the permissions to access resources. If resource owners want to grant other accounts the read and write permissions on resources, they can use ACLs. ACLs grant permissions to accounts. After an account is granted permissions, both the account and its IAM users can access the resources.

An object ACL can be configured in any of the following ways:

#. Specify a pre-defined ACL during object upload.
#. Call ObsClient.SetObjectAcl to specify a pre-defined ACL.
#. Call ObsClient.SetObjectAcl to specify a user-defined ACL.

Specifying a Pre-defined ACL During Object Upload
-------------------------------------------------

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
   // Set a pre-defined ACL for an object during the upload.
   try
   {
       PutObjectRequest request = new PutObjectRequest
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           // Set the object ACL to public read and write.
           CannedAcl = CannedAclEnum.PublicReadWrite,
       };
       PutObjectResponse response = client.PutObject(request);
       Console.WriteLine("Set object ac response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
      Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
      Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Setting a Pre-defined ACL for an Object
---------------------------------------

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
   // Set a pre-defined ACL for the object.
   try
   {
       SetObjectAclRequest request = new SetObjectAclRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       request.CannedAcl = CannedAclEnum.PublicRead;
       SetObjectAclResponse response = client.SetObjectAcl(request);
       Console.WriteLine("Set object acl response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
      Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
      Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Setting a User-defined Object ACL
---------------------------------

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
   // Set a user-defined object ACL.
   try
   {
       SetObjectAclRequest request = new SetObjectAclRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       request.AccessControlList = new AccessControlList();
       Owner owner = new Owner();
       owner.Id = "owerid";
       request.AccessControlList.Owner = owner;
       Grant item = new Grant();
       item.Permission = PermissionEnum.FullControl;
       item.Grantee = new GroupGrantee(GroupGranteeEnum.AllUsers);
       request.AccessControlList.Grants.Add(item);
       SetObjectAclResponse response = client.SetObjectAcl(request);
       Console.WriteLine("Set object acl response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
      Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
      Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   The owner or grantee ID needed in the ACL indicates the account ID, which can be viewed on the **My Credentials** page of OBS Console.

Obtaining an Object ACL
-----------------------

You can call ObsClient.GetObjectAcl to obtain the ACL of an object. Sample code is as follows:

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
   // Obtain the ACL of an object.
   try
   {
       GetObjectAclRequest request = new GetObjectAclRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       GetObjectAclResponse response = client.GetObjectAcl(request);
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
