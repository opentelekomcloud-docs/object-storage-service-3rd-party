:original_name: obs_25_1203.html

.. _obs_25_1203:

Setting Website Hosting
=======================

You can call **ObsClient.SetBucketWebsite** to set website hosting on a bucket.

Configuring the Default Homepage and Error Pages
------------------------------------------------

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
   //Configure the homepage and error pages.
   try
   {
       SetBucketWebsiteRequest request = new SetBucketWebsiteRequest();
       request.BucketName = "bucketname";
       request.Configuration = new WebsiteConfiguration();
       //Configure the default homepage.
       request.Configuration.IndexDocument = "index.html";
       //Configure the error pages.
       request.Configuration.ErrorDocument = "error.html";
       SetBucketWebsiteResponse response = client.SetBucketWebsiteConfiguration(request);
       Console.WriteLine("Set bucket website response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Configuring the Redirection Rules
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
   // Set the redirection rule.
   try
   {
       SetBucketWebsiteRequest request = new SetBucketWebsiteRequest();
       request.BucketName = "bucketname";
       request.Configuration = new WebsiteConfiguration(); //Configure the default homepage.
       request.Configuration.IndexDocument= "index.html";
       //Configure the error pages.
       request.Configuration.ErrorDocument = "error.html";
       RoutingRule routingRule = new RoutingRule();
       routingRule.Redirect = new Redirect();
       routingRule.Redirect.HostName = "www.example.com";
       routingRule.Redirect.HttpRedirectCode = "305";
       routingRule.Redirect.Protocol = ProtocolEnum.Http;
       routingRule.Redirect.ReplaceKeyPrefixWith = "replacekeyprefix";
       routingRule.Condition = new Condition();
       routingRule.Condition.HttpErrorCodeReturnedEquals = "404";
       routingRule.Condition.KeyPrefixEquals = "keyprefix";
       request.Configuration.RoutingRules.Add(routingRule);
       SetBucketWebsiteResponse response = client.SetBucketWebsiteConfiguration(request);
       Console.WriteLine("Set bucket website response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Configuring Redirection for All Requests
----------------------------------------

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
   // Configure redirection for all requests.
   try
   {
       SetBucketWebsiteRequest request = new SetBucketWebsiteRequest();
       request.BucketName = "bucketname";
       request.Configuration = new WebsiteConfiguration();
       request.Configuration.RedirectAllRequestsTo = new RedirectBasic();
       request.Configuration.RedirectAllRequestsTo.HostName = "www.example.com";
       request.Configuration.RedirectAllRequestsTo.Protocol = ProtocolEnum.Https;
       SetBucketWebsiteResponse response = client.SetBucketWebsiteConfiguration(request);
       Console.WriteLine("Set bucket website response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
