:original_name: obs_25_0808.html

.. _obs_25_0808:

Setting or Obtaining a Versioning Object ACL
============================================

Setting an ACL for an Object Version
------------------------------------

You can call **ObsClient.SetObjectAcl** to pass the version ID (**VersionId**) to set an ACL for an object version. Sample code is as follows:

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
   // Set an ACL for an object version.
   try
   {
       SetObjectAclRequest request = new SetObjectAclRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       request.VersionId = "versionId";
       request.AccessControlList = new AccessControlList();
       Owner owner = new Owner();
       owner.Id = "ownerid";
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

Obtaining the ACL of an Object Version
--------------------------------------

You can call **ObsClient.GetObjectAcl** to pass the version ID (**VersionId**) to obtain the ACL of an object version. Sample code is as follows:

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
   // Obtain the ACL of a versioning object.
   try
   {
       GetObjectAclRequest request = new GetObjectAclRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       request.VersionId = "versionId";
       GetObjectAclResponse response = client.GetObjectAcl(request);
       Console.WriteLine("GetObjectAcl grant account: {0}", response.AccessControlList.Grants.Count);
       Console.WriteLine("GetObjectAcl owner id: {0}", response.AccessControlList.Owner.Id);
       foreach (Grant grant in response.AccessControlList.Grants)
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
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
