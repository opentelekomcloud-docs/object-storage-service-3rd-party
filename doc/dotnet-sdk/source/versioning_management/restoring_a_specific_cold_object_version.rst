:original_name: obs_25_0806.html

.. _obs_25_0806:

Restoring a Specific Cold Object Version
========================================

You can call **ObsClient.RestoreObject** to restore a Cold object version by specifying **VersionId**.

This example specifies **versionId** to restore Cold object **destobjectname** in **destbucketname** as a Standard object.

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
   // Restore a specific Cold object version.
   try
   {
       RestoreObjectRequest request = new RestoreObjectRequest();
       request.BucketName = "bucketname";
       request.ObjectKey = "objectname";
       request.Days = 5;
       // Restore a versioned object at an expedited speed.
       request.Tier = RestoreTierEnum.Expedited;
       request.VersionId = "versionId";
       RestoreObjectResponse response = client.RestoreObject(request);
       Console.WriteLine("Restore object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. caution::

   To prolong the validity period of the Cold data restored, you can repeatedly restore the data, but you will be billed for each restoration. After a second restore, the validity period of Standard object copies will be prolonged, and you need to pay for storing these copies during the prolonged period.
