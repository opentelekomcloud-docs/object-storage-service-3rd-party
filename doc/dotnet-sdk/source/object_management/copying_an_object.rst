:original_name: obs_25_0605.html

.. _obs_25_0605:

Copying an Object
=================

The object copy operation can create a copy for an existing object in OBS.

You can call **ObsClient.CopyObject** to copy an object. When copying an object, you can specify properties and ACL for it.

.. note::

   -  If the source object to be copied is in the Cold storage class, you must restore it first.

Copying an Object in Simple Mode
--------------------------------

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

   // Copy an object.
   try
   {
       CopyObjectRequest request = new CopyObjectRequest();
       request.SourceBucketName = "sourcebucketname";
       request.SourceObjectKey = "sourceobjectname";
       request.BucketName = "destbucketname";
       request.ObjectKey = "destobjectName";
       CopyObjectResponse response = client.CopyObject(request);
       Console.WriteLine("Copy object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Rewriting Object Properties
---------------------------

The following sample code shows how to rewrite object properties.

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
   //Rewrite object properties.
   try
   {
       CopyObjectRequest request = new CopyObjectRequest();
       request.SourceBucketName = "sourcebucketname";
       request.SourceObjectKey = "sourceobjectname";
       request.BucketName = "destbucketname";
       request.ObjectKey = "destobjectName";
       request.StorageClass = StorageClassEnum.Warm;
       request.ContentType = "image/jpeg";
       request.MetadataDirective = MetadataDirectiveEnum.Replace;
       CopyObjectResponse response = client.CopyObject(request);
       Console.WriteLine("Copy object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Copying an Object by Specifying Conditions
------------------------------------------

When copying an object, you can specify one or more restriction conditions. If the conditions are met, the object will be copied. Otherwise, an exception will be thrown and the copy will fail.

You can set the following conditions:

+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| Parameter                       | Description                                                                                                                    | Property in OBS .NET SDK            |
+=================================+================================================================================================================================+=====================================+
| Copy-Source-If-Modified-Since   | Copies the source object if it has been modified since the specified time; otherwise, an exception is thrown.                  | CopyObjectRequest.IfModifiedSince   |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| Copy-Source-If-Unmodified-Since | Copies the source object if it has not been modified since the specified time; otherwise, an exception is thrown.              | CopyObjectRequest.IfUnmodifiedSince |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| Copy-Source-If-Match            | Copies the source object if its ETag is the same as the one specified by this parameter; otherwise, an exception is thrown.    | CopyObjectRequest.IfMatch           |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| Copy-Source-If-None-Match       | Copies the source object if its ETag is different from the one specified by this parameter; otherwise, an exception is thrown. | CopyObjectRequest.IfNoneMatch       |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+

.. note::

   -  The ETag of the source object is the MD5 check value of the source object.
   -  If the object copy request includes **IfUnmodifiedSince**, **IfMatch**, **IfModifiedSince**, or **IfNoneMatch**, and the specified condition is not met, the copy will fail and an exception will be thrown with HTTP status code **412 Precondition Failed** returned.
   -  **IfModifiedSince** and **IfNoneMatch** can be used together and so do **IfUnmodifiedSince** and **IfMatch**.

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

   // Set the condition for restricting the copy.
   try
   {
       CopyObjectRequest request = new CopyObjectRequest();
       request.SourceBucketName = "sourcebucketname";
       request.SourceObjectKey = "sourceobjectname";
       request.BucketName = "destbucketname";
       request.ObjectKey = "destobjectName";

       request.IfModifiedSince = new DateTime(2018, 3, 10, 12, 00, 00);
       CopyObjectResponse response = client.CopyObject(request);
       Console.WriteLine("Copy object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Rewriting an Object ACL
-----------------------

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
   // Rewrite the object ACL.
   try
   {
       CopyObjectRequest request = new CopyObjectRequest();
       request.SourceBucketName = "sourcebucketname";
       request.SourceObjectKey = "sourceobjectname";
       request.BucketName = "destbucketname";
       request.ObjectKey = "destobjectName";
       request.CannedAcl = CannedAclEnum.PublicRead;
       CopyObjectResponse response = client.CopyObject(request);
       Console.WriteLine("Copy object response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
