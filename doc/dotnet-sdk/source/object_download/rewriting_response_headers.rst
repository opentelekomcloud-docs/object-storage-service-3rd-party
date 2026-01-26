:original_name: obs_25_0507.html

.. _obs_25_0507:

Rewriting Response Headers
==========================

When downloading an object, you can rewrite some HTTP/HTTPS response headers. The following table lists rewritable response headers.

+--------------------+-----------------------------------------------------------+-------------------------------------------------------------+
| Parameter          | Description                                               | Property in OBS .NET SDK                                    |
+====================+===========================================================+=============================================================+
| ContentType        | Rewrites **Content-Type** in HTTP/HTTPS responses.        | GetObjectRequest.ResponseHeaderOverrides.ContentType        |
+--------------------+-----------------------------------------------------------+-------------------------------------------------------------+
| ContentLanguage    | Rewrites **Content-Language** in HTTP/HTTPS responses.    | GetObjectRequest.ResponseHeaderOverrides.ContentLanguage    |
+--------------------+-----------------------------------------------------------+-------------------------------------------------------------+
| Expires            | Rewrites **Expires** in HTTP/HTTPS responses.             | ObjectRepleaceMetadata.Expires                              |
+--------------------+-----------------------------------------------------------+-------------------------------------------------------------+
| CacheControl       | Rewrites **Cache-Control** in HTTP/HTTPS responses.       | GetObjectRequest.ResponseHeaderOverrides.CacheControl       |
+--------------------+-----------------------------------------------------------+-------------------------------------------------------------+
| ContentDisposition | Rewrites **Content-Disposition** in HTTP/HTTPS responses. | GetObjectRequest.ResponseHeaderOverrides.ContentDisposition |
+--------------------+-----------------------------------------------------------+-------------------------------------------------------------+
| ContentEncoding    | Rewrites **Content-Encoding** in HTTP/HTTPS responses.    | GetObjectRequest.ResponseHeaderOverrides.ContentEncoding    |
+--------------------+-----------------------------------------------------------+-------------------------------------------------------------+

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
   // Rewrite response headers when downloading an object.
   try
   {
       ResponseHeaderOverrides responseHeaderOverrides = new ResponseHeaderOverrides();
       responseHeaderOverrides.ContentType = "image/jpeg";
       GetObjectRequest request = new GetObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           ResponseHeaderOverrides = responseHeaderOverrides,
       };
       GetObjectResponse response = client.GetObject(request);
       Console.WriteLine("Get object response: {0}", response.StatusCode);
       Console.WriteLine("ContentType: {0}", response.ContentType);
       response.Dispose();
   }
   catch (ObsException ex)
   {
      Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
      Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
