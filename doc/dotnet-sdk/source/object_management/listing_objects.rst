:original_name: obs_25_0603.html

.. _obs_25_0603:

Listing Objects
===============

You can call **ObsClient.ListObjects** to list objects in a bucket.

The following table describes the parameters involved in this API.

+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------+
| Parameter             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Property in OBS .NET SDK      |
+=======================+============================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+===============================+
| BucketName            | Bucket name                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | ListObjectsRequest.BucketName |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------+
| Prefix                | Name prefix that the objects to be listed must contain                                                                                                                                                                                                                                                                                                                                                                                                                                     | ListObjectsRequest.Prefix     |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------+
| Marker                | Object name to start with when listing objects in a bucket. All objects are listed in the lexicographical order.                                                                                                                                                                                                                                                                                                                                                                           | ListObjectsRequest.Marker     |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------+
| MaxKeys               | Maximum number of objects listed in the response body. The value ranges from **1** to **1000**. If the value exceeds **1000**, only 1,000 objects are returned.                                                                                                                                                                                                                                                                                                                            | ListObjectsRequest.MaxKeys    |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------+
| Delimiter             | Character used to group object names. If the object name contains the **Delimiter** parameter, the character string from the first character to the first delimiter in the object name is grouped under a single result element, **CommonPrefix**. (If a prefix is specified in the request, the prefix must be removed from the object name.)                                                                                                                                             | ListObjectsRequest.Delimiter  |
|                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |                               |
|                       | For a parallel file system, if this parameter is not specified, all the content in the directory is recursively listed by default, and subdirectories are also listed. In big data scenarios, parallel file systems usually have deep directory levels and each directory has a large number of files. In such case, you are advised to configure **[delimiter="/"]** to list the content in the current directory, but not list subdirectories, thereby improving the listing efficiency. |                               |
+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------+

Listing Objects in Simple Mode
------------------------------

The following sample code shows how to list objects in simple mode. A maximum of 1000 objects can be returned.

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
   // Simple listing
   try
   {
       ListObjectsRequest request = new ListObjectsRequest();
       request.BucketName = "bucketname";
       ListObjectsResponse response = client.ListObjects(request);
       foreach (ObsObject entry in response.ObsObjects)
       {
           Console.WriteLine("key = {0} size = {1}", entry.ObjectKey, entry.Size);
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   Information about a maximum of 1000 objects can be listed each time. If a bucket contains more than 1000 objects and **ListObjectsResponse.IsTruncated** is **true** in the returned result, not all objects are listed. In such cases, you can use **ListObjectsResponse.NextMarker** to obtain the start position for next listing.

Listing Objects by Specifying the Number
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
   // Specify the number.
   try
   {
       ListObjectsRequest request = new ListObjectsRequest();
       request.BucketName = "bucketname";
          // Set the number of objects to be listed to 100.
       request.MaxKeys = 100;
       ListObjectsResponse response = client.ListObjects(request);
       foreach (ObsObject entry in response.ObsObjects)
       {
           Console.WriteLine("key = {0} size = {1}", entry.ObjectKey, entry.Size);
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing Objects by Specifying a Prefix
--------------------------------------

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
   // List objects by specifying a prefix.
   try
   {
       ListObjectsRequest request = new ListObjectsRequest();
       request.BucketName = "bucketname";
       //Specify the prefix.
       request.Prefix = "prefix";
       ListObjectsResponse response = client.ListObjects(request);
       foreach (ObsObject entry in response.ObsObjects)
       {
           Console.WriteLine("key = {0} size = {1}", entry.ObjectKey, entry.Size);
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing Objects by Specifying the Start Position
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
   // List objects by specifying the start position.
   try
   {
       ListObjectsRequest request = new ListObjectsRequest();
       request.BucketName = "bucketname";
       //Specify the start position for listing.
       request.Marker = "marker";
       ListObjectsResponse response = client.ListObjects(request);
       foreach (ObsObject entry in response.ObsObjects)
       {
           Console.WriteLine("key = {0} size = {1}", entry.ObjectKey, entry.Size);
       }
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing All Objects in Paging Mode
----------------------------------

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
   //List all objects in paging mode.
   try
   {
       ListObjectsRequest request = new ListObjectsRequest();
       ListObjectsResponse response;
       request.BucketName = "bucketname";
       request.MaxKeys = 100;
       do
       {
           response = client.ListObjects(request);
           foreach (ObsObject entry in response.ObsObjects)
           {
               Console.WriteLine("key = {0} size = {1}", entry.ObjectKey, entry.Size);
           }
           request.Marker = response.NextMarker;
       }
       while (response.IsTruncated);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing All Objects in a Folder
-------------------------------

There is no folder concept in OBS. All elements in buckets are objects. Folders are actually objects whose sizes are 0 and whose names end with a slash (/). When you set a folder name as the prefix, objects in this folder will be listed. Sample code is as follows:

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
   //List all objects in a folder.
   try
   {
       ListObjectsRequest request = new ListObjectsRequest();
       ListObjectsResponse response;
       request.BucketName = "bucketname";
       request.MaxKeys = 1000;
       // Set the prefix to dir/.
       request.Prefix = "dir/";
       do
       {
           response = client.ListObjects(request);
           foreach (ObsObject entry in response.ObsObjects)
           {
               Console.WriteLine("key = {0} size = {1}", entry.ObjectKey, entry.Size);
           }
           request.Marker = response.NextMarker;
       }
       while (response.IsTruncated);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
