:original_name: obs_25_0902.html

.. _obs_25_0902:

Setting Lifecycle Rules
=======================

You can call **ObsClient.SetBucketLifecycle** to set lifecycle rules.

Setting an Object Transition Policy
-----------------------------------

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
   //Set an object transition policy.
   try
   {
       SetBucketLifecycleRequest request = new SetBucketLifecycleRequest();
       request.BucketName = "bucketname";
       request.Configuration = new LifecycleConfiguration();
       LifecycleRule rule1 = new LifecycleRule();
       rule1.Id = "rule1";
       rule1.Prefix = "prefix";
       rule1.Status = RuleStatusEnum.Enabled;
       Transition transition = new Transition();
       rule1.Transitions.Add(transition);
       // Specify that objects whose names contain the specified prefix will be transitioned 30 days after creation.
       transition.Days = 30;
       // Specify the storage class that the object will be transitioned to.
       transition.StorageClass = StorageClassEnum.Warm;
       NoncurrentVersionTransition noncurrentVersionTransition  = new NoncurrentVersionTransition();
       rule1.NoncurrentVersionTransitions.Add(noncurrentVersionTransition);
       // Specify that objects whose names contain the specified prefix will be transitioned 60 days after becoming noncurrent versions.
       noncurrentVersionTransition.NoncurrentDays = 60;
       // Specify the storage class that a noncurrent version will be transitioned to.
       noncurrentVersionTransition.StorageClass = StorageClassEnum.Warm;
       request.Configuration.Rules.Add(rule1);
       SetBucketLifecycleResponse response = client.SetBucketLifecycle(request);
       Console.WriteLine("Set bucket lifecycle response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Setting an Object Expiration Time
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
   // Set the object expiration time.
   try
   {
       SetBucketLifecycleRequest request = new SetBucketLifecycleRequest();
       request.BucketName = "bucketname";
       request.Configuration = new LifecycleConfiguration();
       LifecycleRule rule1 = new LifecycleRule();
       rule1.Id = "rule1";
       rule1.Prefix = "prefix";
       rule1.Status = RuleStatusEnum.Enabled;
       rule1.Expiration = new Expiration();
       //Specify that objects whose names contain the prefix will expire 60 days after creation.
       rule1.Expiration.Days = 60;
       // Specify that objects whose names contain the prefix will expire 60 days after becoming noncurrent versions.
       rule1.NoncurrentVersionExpiration = new NoncurrentVersionExpiration();
       rule1.NoncurrentVersionExpiration.NoncurrentDays = 60;
       request.Configuration.Rules.Add(rule1);
       SetBucketLifecycleResponse response = client.SetBucketLifecycle(request);
       Console.WriteLine("Set bucket lifecycle response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  Each time you call this API to configure a lifecycle rule, the lifecycle rules you previously configured will be overwritten.
