:original_name: obs_25_0903.html

.. _obs_25_0903:

Viewing Lifecycle Rules
=======================

You can call **ObsClient.GetBucketLifecycle** to view lifecycle rules.

This example views the lifecycle configuration of bucket **bucketname**.

The example code is as follows:

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
   // View the bucket lifecycle.
   try
   {
       GetBucketLifecycleRequest request = new GetBucketLifecycleRequest();
       request.BucketName = "bucketname";
       GetBucketLifecycleResponse response = client.GetBucketLifecycle(request);
       foreach (LifecycleRule lifecycleRule in response.Configuration.Rules)
       {
           Console.WriteLine("Lifecycle rule id: {0}", lifecycleRule.Id);
           Console.WriteLine("Lifecycle rule prefix: {0}", lifecycleRule.Prefix);
           Console.WriteLine("Lifecycle rule status: {0}", lifecycleRule.Status);
           if (null != lifecycleRule.Expiration)
           {
               Console.WriteLine("expiration days: {0}", lifecycleRule.Expiration.Days);
           }
           if (null != lifecycleRule.NoncurrentVersionExpiration)
           {
               Console.WriteLine("NoncurrentVersionExpiration NoncurrentDays: {0}", lifecycleRule.NoncurrentVersionExpiration.NoncurrentDays);
           }
           foreach (Transition transition in lifecycleRule.Transitions)
           {
               Console.WriteLine("Transition Days : {0}", transition.Days);
               Console.WriteLine("Transition StorageClass : {0}", transition.StorageClass);
           }
           foreach (NoncurrentVersionTransition noncurrentVersionTransition in lifecycleRule.NoncurrentVersionTransitions)
           {
               Console.WriteLine("NoncurrentVersionTransition NoncurrentDays: {0}", noncurrentVersionTransition.NoncurrentDays);
               Console.WriteLine("NoncurrentVersionTransition StorageClass : {0}", noncurrentVersionTransition.StorageClass);
           }
           Console.WriteLine("Get bucket lifecycle response: {0}", response.StatusCode);
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  To handle the error codes possibly returned during the operation, see :ref:`OBS Server-Side Error Codes <obs_25_1601>`.
