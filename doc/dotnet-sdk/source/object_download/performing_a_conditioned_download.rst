:original_name: obs_25_0506.html

.. _obs_25_0506:

Performing a Conditioned Download
=================================

When downloading an object, you can specify one or more conditions. Only when the conditions are met, the object will be downloaded. Otherwise, an exception indicating a download failure will be thrown.

You can set the following conditions:

+---------------------+---------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
| Parameter           | Description                                                                                                                     | Property in OBS .NET SDK           |
+=====================+=================================================================================================================================+====================================+
| If-Modified-Since   | Returns the object if it has been modified since the specified time; otherwise, an error is returned.                           | GetObjectRequest.IfModifiedSince   |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
| If-Unmodified-Since | Returns the object if it has not been modified since the specified time; otherwise, an error is returned.                       | GetObjectRequest.IfUnmodifiedSince |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
| If-Match            | Returns the source object if its ETag is the same as the one specified by this parameter; otherwise, an exception is thrown.    | GetObjectRequest.IfMatch           |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------+------------------------------------+
| If-None-Match       | Returns the source object if its ETag is different from the one specified by this parameter; otherwise, an exception is thrown. | GetObjectRequest.IfNoneMatch       |
+---------------------+---------------------------------------------------------------------------------------------------------------------------------+------------------------------------+

.. note::

   -  The ETag of an object is the MD5 check value of the object.
   -  If the download request includes **IfUnmodifiedSince** or **IfMatch** and the specified condition is not met, an exception will be thrown with HTTP status code **412 Precondition Failed** returned.
   -  If the download request includes **IfModifiedSince** or **IfNoneMatch** and the specified condition is not met, an exception will be thrown with HTTP status code **304 Not Modified** returned.

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
   // Download an object in conditioned mode.
   try
   {
       DateTime datetime = new DateTime(2018, 3, 10, 12, 00, 00);
       GetObjectRequest request = new GetObjectRequest()
       {
           BucketName = "bucketname",
           ObjectKey = "objectname",
           IfModifiedSince = datetime,
       };
       using (GetObjectResponse response = client.GetObject(request))
       {
           string dest = "savepath";
           if (!File.Exists(dest))
           {
               response.WriteResponseStreamToFile(dest);
           }
           Console.WriteLine("Get object response: {0}", response.StatusCode);
       }
   }
   catch (ObsException ex)
   {
      Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
      Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
