:original_name: obs_25_0803.html

.. _obs_25_0803:

Viewing Versioning Status of a Bucket
=====================================

You can call **ObsClient.GetBucketVersioning** to view the versioning status of a bucket.

This example obtains the versioning status of bucket **bucketname**.

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
   // View the versioning status.
   try
   {
       GetBucketVersioningRequest request = new GetBucketVersioningRequest();
       request.BucketName = "bucketname";
       GetBucketVersioningResponse response = client.GetBucketVersioning(request);
       Console.WriteLine("Get bucket version response: {0}", response.StatusCode);
       Console.WriteLine("Status: {0}", response.Configuration.Status);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  To handle the error codes possibly returned during the operation, see :ref:`OBS Server-Side Error Codes <obs_25_1601>`.
