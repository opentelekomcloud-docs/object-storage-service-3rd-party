:original_name: obs_25_0509.html

.. _obs_25_0509:

Downloading a Cold Object
=========================

Before you can download a Cold object, you must restore it. Cold objects can be restored in either of the following ways.

+-------------------+-----------------------------------------------------------------------+---------------------------+
| Option            | Description                                                           | Value in OBS .NET SDK     |
+===================+=======================================================================+===========================+
| Expedited restore | Data can be restored within 1 to 5 minutes.                           | RestoreTierEnum.Expedited |
+-------------------+-----------------------------------------------------------------------+---------------------------+
| Standard restore  | Data can be restored within 3 to 5 hours. This is the default option. | RestoreTierEnum.Standard  |
+-------------------+-----------------------------------------------------------------------+---------------------------+

.. caution::

   To prolong the validity period of the Cold data restored, you can repeatedly restore the data, but you will be billed for each restoration. After a second restore, the validity period of Standard object copies will be prolonged, and you need to pay for storing these copies during the prolonged period.

You can call **ObsClient.RestoreObject** to restore Cold objects. Sample code is as follows:

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

   try
   {
       RestoreObjectRequest request = new RestoreObjectRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       request.Days = 5;
       request.Tier = RestoreTierEnum.Expedited;
       // This parameter is optional. By default, the latest object version is restored. You can set versionId to restore a specified object version.
       // request.VersionId = "versionId";
       RestoreObjectResponse response = client.RestoreObject(request);
       Console.WriteLine("Restore object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
      Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
      Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   -  The object specified in **ObsClient.RestoreObject** must be in the OBS Cold storage class. Otherwise, an exception will be thrown when you call this API.
   -  **RestoreObjectRequest.Days** specifies the retention period (1 to 30 days) of the restored object.
   -  **RestoreObjectRequest.Tier** specifies the restore option, which indicates the time spend on restoring an object.
