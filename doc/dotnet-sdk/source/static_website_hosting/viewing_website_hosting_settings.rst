:original_name: obs_25_1204.html

.. _obs_25_1204:

Viewing Website Hosting Settings
================================

You can call **ObsClient.GetBucketWebsite** to view the hosting settings of a bucket.

This example views the hosting configuration of bucket **bucketname**.

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
   // View hosting settings.
   try
   {
       GetBucketWebsiteRequest request = new GetBucketWebsiteRequest();
       request.BucketName = "bucketname";
       GetBucketWebsiteResponse response = client.GetBucketWebsite(request);
       Console.WriteLine("GetBucketWebsite website configuration error document: {0}", response.Configuration.ErrorDocument);
       Console.WriteLine("GetBucketWebsite website configuration index document: {0}", response.Configuration.IndexDocument);
       Console.WriteLine("Get bucket website response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  To handle the error codes possibly returned during the operation, see :ref:`OBS Server-Side Error Codes <obs_25_1601>`.
