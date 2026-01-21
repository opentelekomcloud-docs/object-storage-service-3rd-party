:original_name: obs_25_1202.html

.. _obs_25_1202:

Website File Hosting
====================

You can perform the following to implement website file hosting:

#. Upload the website files to your bucket in OBS as objects and set the MIME type for the objects.
#. Set the object ACL to public read.
#. Access the objects using a browser.

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
   try
   {
       //Set the MIME type for an object.
       PutObjectRequest request = new PutObjectRequest
       {
           BucketName = "bucketname",
           ObjectKey = "test.html",
           FilePath = "localfile.html",// Path of the local file uploaded. The file name must be specified.
           CannedAcl = CannedAclEnum.PublicRead,//Set the object ACL to public read.
           ContentType = "text/html",
       };
       // Upload an object.
       PutObjectResponse response = client.PutObject(request);
       Console.WriteLine("put object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   You can use **https://**\ *bucketname*\ **.**\ *your-endpoint*\ **/test.html** in a browser to access files hosted using the sample code.
