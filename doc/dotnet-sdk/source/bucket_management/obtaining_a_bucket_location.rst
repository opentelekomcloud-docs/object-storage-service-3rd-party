:original_name: obs_25_0308.html

.. _obs_25_0308:

Obtaining a Bucket Location
===========================

You can call **ObsClient.GetBucketLocation** to obtain the location of a bucket.

This example returns the region of bucket **bucketname**.

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
   // Obtain the bucket location.
   try
   {
       GetBucketLocationRequest request = new GetBucketLocationRequest
       {
           BucketName = "bucketname",
       };
       GetBucketLocationResponse response = client.GetBucketLocation(request);
       Console.WriteLine("Get bucket location response: {0}", response.StatusCode);
       Console.WriteLine("Location: {0}", response.Location);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   When creating a bucket, you can specify its location. For details, see :ref:`Creating a Bucket <obs_25_0301>`.
