:original_name: obs_25_0807.html

.. _obs_25_0807:

Listing Versioning Objects
==========================

You can call **ObsClient.ListVersions** to list versioning objects.

The following table describes the parameters involved in this API.

+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| Parameter       | Description                                                                                                                                                                                                                                                                                                                                    | Property in OBS .NET SDK            |
+=================+================================================================================================================================================================================================================================================================================================================================================+=====================================+
| BucketName      | Bucket name                                                                                                                                                                                                                                                                                                                                    | ListVersionsRequest.BucketName      |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| Prefix          | Name prefix that the objects to be listed must contain                                                                                                                                                                                                                                                                                         | ListVersionsRequest.Prefix          |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| KeyMarker       | Object name to start with when listing versioning objects in a bucket. All versioning objects following this parameter are listed in the lexicographical order.                                                                                                                                                                                | ListVersionsRequest.KeyMarker       |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| MaxKeys         | Maximum number of listed versioning objects. The value ranges from **1** to **1000**. If the specified value exceeds **1000**, only 1,000 versioning objects are returned by default.                                                                                                                                                          | ListVersionsRequest.MaxKeys         |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| Delimiter       | Character used to group object names. If the object name contains the **Delimiter** parameter, the character string from the first character to the first delimiter in the object name is grouped under a single result element, **CommonPrefix**. (If a prefix is specified in the request, the prefix must be removed from the object name.) | ListVersionsRequest.Delimiter       |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
| VersionIdMarker | Object name to start with when listing versioning objects in a bucket. All versioning objects are listed in the lexicographical order by object name and version ID. This parameter must be used together with **KeyMarker**.                                                                                                                  | ListVersionsRequest.VersionIdMarker |
+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+

.. note::

   -  If the value of **VersionIdMarker** is not a version ID specified by **KeyMarker**, **VersionIdMarker** is ineffective.
   -  The returned result of **ObsClient.ListVersions** includes the versioning objects and delete markers.

Listing Versioning Objects in Simple Mode
-----------------------------------------

The following sample code shows how to list versioning objects in simple mode. A maximum of 1000 versioning objects can be returned.

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
   //List versioning objects.
   try
   {
       ListVersionsRequest request = new ListVersionsRequest();
       request.BucketName = "bucketname";
       ListVersionsResponse response = client.ListVersions(request);
       foreach (ObsObjectVersion objectVersion in response.Versions)
       {
           Console.WriteLine("Key: {0}", objectVersion.ObjectKey);
           Console.WriteLine("VersionId: {0}", objectVersion.VersionId);
       }
       Console.WriteLine("List versions response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

.. note::

   Information about a maximum of 1000 versioning objects can be listed each time. If a bucket contains more than 1000 objects and **ListVersionsResponse.IsTruncated** is **true** in the returned result, not all versioning objects are listed. In such cases, you can use **ListVersionsResponse.NextKeyMarker** and **ListVersionsResponse.NextVersionIdMarker** to obtain the start position for next listing.

Listing Versioning Objects by Specifying the Number
---------------------------------------------------

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
   //List versioning objects by specifying the number.
   try
   {
       ListVersionsRequest request = new ListVersionsRequest();
       request.BucketName = "bucketname";
       request.MaxKeys = 100;
       ListVersionsResponse response = client.ListVersions(request);
       foreach (ObsObjectVersion objectVersion in response.Versions)
       {
           Console.WriteLine("Key: {0}", objectVersion.ObjectKey);
           Console.WriteLine("VersionId: {0}", objectVersion.VersionId);
       }
       Console.WriteLine("List versions response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing Versioning Objects by Specifying a Prefix
-------------------------------------------------

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
   //List versioning objects by specifying a prefix.
   try
   {
       ListVersionsRequest request = new ListVersionsRequest();
       request.BucketName = "bucketname";
       request.MaxKeys = 100;
       request.Prefix = "prefix";
       ListVersionsResponse response = client.ListVersions(request);
       foreach (ObsObjectVersion objectVersion in response.Versions)
       {
           Console.WriteLine("Key: {0}", objectVersion.ObjectKey);
           Console.WriteLine("VersionId: {0}", objectVersion.VersionId);
       }
       Console.WriteLine("List versions response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing Versioning Objects by Specifying the Start Position
-----------------------------------------------------------

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
   //Specify the start position for listing.
   try
   {
       ListVersionsRequest request = new ListVersionsRequest();
       request.BucketName = "bucketname";
       request.MaxKeys = 100;
       request.Prefix = "prefix";
       request.KeyMarker = "keyMarker";
       ListVersionsResponse response = client.ListVersions(request);
       foreach (ObsObjectVersion objectVersion in response.Versions)
       {
           Console.WriteLine("Key: {0}", objectVersion.ObjectKey);
           Console.WriteLine("VersionId: {0}", objectVersion.VersionId);
       }
       Console.WriteLine("List versions response: {0}", response.StatusCode);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing All Versioning Objects in Paging Mode
---------------------------------------------

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
   //List all versioning objects in paging mode.
   try
   {
       ListVersionsRequest request = new ListVersionsRequest();
       request.BucketName = "bucketname";
       request.MaxKeys = 100;
       ListVersionsResponse response;
       do
       {
           response = client.ListVersions(request);
           Console.WriteLine("List versions response: {0}", response.StatusCode);
           foreach (ObsObjectVersion objectVersion in response.Versions)
           {
               Console.WriteLine("Key: {0}", objectVersion.ObjectKey);
               Console.WriteLine("VersionId: {0}", objectVersion.VersionId);
           }
           request.KeyMarker = response.NextKeyMarker;
           request.VersionIdMarker = response.NextVersionIdMarker;
       }
       while (response.IsTruncated);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }

Listing All Versioning Objects in a Folder
------------------------------------------

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
   //List all versioning objects in paging mode.
   try
   {
       ListVersionsRequest request = new ListVersionsRequest();
       request.BucketName = "bucketname";
       request.MaxKeys = 1000;
       // Set the prefix to dir/.
       request.Prefix = "dir/";
       ListVersionsResponse response;
       do
       {
           response = client.ListVersions(request);
           Console.WriteLine("List versions response: {0}", response.StatusCode);
           foreach (ObsObjectVersion objectVersion in response.Versions)
           {
               Console.WriteLine("Key: {0}", objectVersion.ObjectKey);
               Console.WriteLine("VersionId: {0}", objectVersion.VersionId);
           }
           request.KeyMarker = response.NextKeyMarker;
           request.VersionIdMarker = response.NextVersionIdMarker;
       }
       while (response.IsTruncated);
   }
   catch (ObsException ex)
   {
       Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);
       Console.WriteLine("ErrorMessage: {0}", ex.ErrorMessage);
   }
