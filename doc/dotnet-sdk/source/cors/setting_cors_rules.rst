:original_name: obs_25_1002.html

.. _obs_25_1002:

Setting CORS Rules
==================

You can call **ObsClient.SetBucketCors** to set CORS rules for a bucket. If the bucket is configured with CORS rules, the newly set ones will overwrite the existing ones.

This example sets a CORS rule for bucket **bucketname**.

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
   // Set the CORS rules for a bucket.
   try
   {
       SetBucketCorsRequest request = new SetBucketCorsRequest();
       request.BucketName = "bucketname";
       request.Configuration = new CorsConfiguration();
       CorsRule rule = new CorsRule();
       rule.Id = "20170820";
       // Specify the origin of the cross-domain request.
       rule.AllowedOrigins.Add("http://www.a.com");
       rule.AllowedOrigins.Add("http://www.b.com");
       // Specify whether headers specified in Access-Control-Request-Headers in the OPTIONS request can be used.
       rule.AllowedHeaders.Add("x-obs-header");
       // Specify the request method, which can be GET, PUT, DELETE, POST, or HEAD.
       rule.AllowedMethods.Add(HttpVerb.HEAD);
       rule.AllowedMethods.Add(HttpVerb.PUT);
       rule.AllowedMethods.Add(HttpVerb.GET);
       rule.AllowedMethods.Add(HttpVerb.POST);
       rule.AllowedMethods.Add(HttpVerb.DELETE);
       // Specify response headers that users can access using application programs.
       rule.ExposeHeaders.Add("x-obs-test1");
       rule.ExposeHeaders.Add("x-obs-test2");
       rule.MaxAgeSeconds = 100;
       request.Configuration.Rules.Add(rule);
       SetBucketCorsResponse response = client.SetBucketCors(request);
       Console.WriteLine("Set bucket cors response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  **AllowedOrigins**, **AllowedMethods**, and **AllowedHeaders**, respectively, can contain up to one wildcard character (*). Wildcard characters (*) indicate that all origins, operations, or headers are allowed.
