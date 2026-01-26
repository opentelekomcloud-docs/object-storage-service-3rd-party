:original_name: obs_25_1003.html

.. _obs_25_1003:

Viewing CORS Rules
==================

You can call **ObsClient.GetBucketCors** to view CORS rules of a bucket.

This example views the CORS rule of bucket **bucketname**.

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
   // View CORS rules.
   try
   {

       GetBucketCorsRequest request = new GetBucketCorsRequest();
       request.BucketName = "bucketname";
       GetBucketCorsResponse response = client.GetBucketCors(request);
       foreach (CorsRule rule in response.Configuration.Rules)
       {
           Console.WriteLine("rule id is: {0}\n", rule.Id);
           foreach (string allowOrigin in rule.AllowedOrigins)
           {
               Console.WriteLine("allowOrigin is: {0}\n", allowOrigin);
           }
           foreach (string allowHeader in rule.AllowedHeaders)
           {
               Console.WriteLine("allowHeader is: {0}\n", allowHeader);
           }
           foreach (HttpVerb allowMethod in rule.AllowedMethods)
           {
               Console.WriteLine("allowMethod is: {0}\n", allowMethod);
           }
           foreach (string exposeHeader in rule.ExposeHeaders)
           {
               Console.WriteLine("exposeHeader is: {0}\n", exposeHeader);
           }
           Console.WriteLine("rule maxAgeSeconds is: {0}\n", rule.MaxAgeSeconds);

       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  To handle the error codes possibly returned during the operation, see :ref:`OBS Server-Side Error Codes <obs_25_1601>`.
