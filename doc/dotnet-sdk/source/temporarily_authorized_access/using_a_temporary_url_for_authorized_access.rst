:original_name: obs_25_0701.html

.. _obs_25_0701:

Using a Temporary URL for Authorized Access
===========================================

**ObsClient** allows you to create a URL whose **Query** parameters are carried with authentication information by specifying the AK and SK, HTTP method, and request parameters. You can provide other users with this URL for temporary access. When generating a URL, you need to specify the validity period of the URL to restrict the access duration of visitors.

If you want to grant other users the permission to perform other operations on buckets or objects (for example, upload or download objects), generate a URL with the corresponding request (for example, to upload an object using the URL that generates the PUT request) and provide the URL for other users.

The following table lists operations can be performed through a signed URL.

+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| Operation                 | HTTP Request Method (Value in OBS .NET SDK) | Sub-resource (Value in OBS .NET SDK) | Bucket Name Required | Object Name Required |
+===========================+=============================================+======================================+======================+======================+
| PUT Bucket                | HttpVerb.PUT                                | N/A                                  | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Buckets               | HttpVerb.GET                                | N/A                                  | No                   | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| DELETE Bucket             | HttpVerb.DELETE                             | N/A                                  | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Objects               | HttpVerb.GET                                | N/A                                  | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Object versions       | HttpVerb.GET                                | SubResourceEnum.Versions             | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| List Multipart uploads    | HttpVerb.GET                                | SubResourceEnum.Uploads              | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| Obtain Bucket Metadata    | HttpVerb.HEAD                               | N/A                                  | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket location       | HttpVerb.GET                                | SubResourceEnum.Location             | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket storageinfo    | HttpVerb.GET                                | SubResourceEnum.StorageInfo          | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket quota          | HttpVerb.PUT                                | SubResourceEnum.Quota                | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket quota          | HttpVerb.GET                                | SubResourceEnum.Quota                | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket storagePolicy  | HttpVerb.PUT                                | SubResourceEnum.StoragePolicy        | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket storagePolicy  | HttpVerb.GET                                | SubResourceEnum.StoragePolicy        | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket ACL            | HttpVerb.PUT                                | SubResourceEnum.Acl                  | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket ACL            | HttpVerb.GET                                | SubResourceEnum.Acl                  | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket logging        | HttpVerb.PUT                                | SubResourceEnum.Logging              | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket logging        | HttpVerb.GET                                | SubResourceEnum.Logging              | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket policy         | HttpVerb.PUT                                | SubResourceEnum.Policy               | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket policy         | HttpVerb.GET                                | SubResourceEnum.Policy               | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| DELETE Bucket policy      | HttpVerb.DELETE                             | SubResourceEnum.Policy               | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket lifecycle      | HttpVerb.PUT                                | SubResourceEnum.Lifecycle            | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket lifecycle      | HttpVerb.GET                                | SubResourceEnum.Lifecycle            | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| DELETE Bucket lifecycle   | HttpVerb.DELETE                             | SubResourceEnum.Lifecycle            | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket website        | HttpVerb.PUT                                | SubResourceEnum.Website              | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket website        | HttpVerb.GET                                | SubResourceEnum.Website              | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| DELETE Bucket website     | HttpVerb.DELETE                             | SubResourceEnum.Website              | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket versioning     | HttpVerb.PUT                                | SubResourceEnum.Versioning           | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket versioning     | HttpVerb.GET                                | SubResourceEnum.Versioning           | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket cors           | HttpVerb.PUT                                | SubResourceEnum.Cors                 | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket cors           | HttpVerb.GET                                | SubResourceEnum.Cors                 | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| DELETE Bucket cors        | HttpVerb.DELETE                             | SubResourceEnum.Cors                 | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Bucket tagging        | HttpVerb.PUT                                | SubResourceEnum.Tagging              | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Bucket tagging        | HttpVerb.GET                                | SubResourceEnum.Tagging              | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| DELETE Bucket tagging     | HttpVerb.DELETE                             | SubResourceEnum.Tagging              | Yes                  | No                   |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Object                | HttpVerb.PUT                                | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| Append Object             | HttpVerb.POST                               | SubResourceEnum.Append               | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Object                | HttpVerb.GET                                | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Object - Copy         | HttpVerb.PUT                                | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| DELETE Object             | HttpVerb.DELETE                             | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| DELETE Objects            | HttpVerb.POST                               | SubResourceEnum.Delete               | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| Obtain Object Metadata    | HttpVerb.HEAD                               | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| PUT Object ACL            | HttpVerb.PUT                                | SubResourceEnum.Acl                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| GET Object ACL            | HttpVerb.GET                                | SubResourceEnum.Acl                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| Initiate Multipart Upload | HttpVerb.POST                               | SubResourceEnum.Uploads              | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| Upload Part               | HttpVerb.PUT                                | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| Upload Part - Copy        | HttpVerb.PUT                                | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| List Parts                | HttpVerb.GET                                | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| Complete Multipart Upload | HttpVerb.POST                               | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| Abort Multipart Upload    | HttpVerb.DELETE                             | N/A                                  | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+
| POST Object restore       | HttpVerb.POST                               | SubResourceEnum.Restore              | Yes                  | Yes                  |
+---------------------------+---------------------------------------------+--------------------------------------+----------------------+----------------------+

To access OBS using a temporary URL generated by the OBS .NET SDK, perform the following steps:

#. Call **ObsClient.CreateTemporarySignature** to generate a signed URL.
#. Use any HTTP library to make an HTTP/HTTPS request to OBS.

.. caution::

   If a CORS or signature mismatch error occurs, refer to the following steps to troubleshoot the issue:

   #. If CORS is not configured, you need to configure CORS rules on OBS Console..
   #. If the signatures do not match, check whether signature parameters are correct by referring to . For example, during an object upload, the backend uses **Content-Type** to calculate the signature and generate an authorized URL, but if **Content-Type** is not set or is set to an incorrect value when the frontend uses the authorized URL, a CORS error occurs. To avoid this issue, ensure that **Content-Type** fields at both the frontend and backend are kept consistent.

The following content provides examples of accessing OBS using a temporary URL, including bucket creation, as well as object upload, download, listing, and deletion.

Creating a Bucket
-----------------

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an ObsClient instance.
   ObsClient client = new ObsClient(accessKey, secretKey, config);

   // Specify the validity period of the URL to 3600 seconds.
   long exipreSeconds = 3600;

   CreateTemporarySignatureRequest request = new CreateTemporarySignatureRequest();
   request.BucketName = "bucketname";
   request.Method = HttpVerb.PUT;
   request.Expires = exipreSeconds;

   CreateTemporarySignatureResponse response = client.CreateTemporarySignature(request);
   Console.WriteLine("Creating bucket using temporary signature url:");
   Console.WriteLine("\t" + response.SignUrl);

   // Use a PUT request to create a bucket.
   HttpWebRequest webRequest = WebRequest.Create(response.SignUrl) as HttpWebRequest;
   webRequest.Method = "PUT";


   foreach (KeyValuePair<string, string> header in response.ActualSignedRequestHeaders)
   {
       if (!header.Key.Equals("host", StringComparison.OrdinalIgnoreCase))
       {
           webRequest.Headers.Add(header.Key, header.Value);
       }
   }

   string location = "your bucket location";

   webRequest.SendChunked = true;
   webRequest.AllowWriteStreamBuffering = false;
   using (Stream requestStream = webRequest.GetRequestStream())
   {
       byte[] buffer = Encoding.UTF8.GetBytes("<CreateBucketConfiguration><LocationConstraint>" + location + "</LocationConstraint></CreateBucketConfiguration>");
       requestStream.Write(buffer, 0, buffer.Length);
   }

   HttpWebResponse webResponse = null;
   try
   {
       webResponse = webRequest.GetResponse() as HttpWebResponse;
   }
   catch (WebException ex)
   {
       webResponse = ex.Response as HttpWebResponse;
   }
   Console.WriteLine("Response Status:" + Convert.ToInt32(webResponse.StatusCode));
   using (MemoryStream dest = new MemoryStream())
   {
       using (Stream stream = webResponse.GetResponseStream())
       {
           byte[] buffer = new byte[8192];
           int bytesRead;
           while ((bytesRead = stream.Read(buffer, 0, buffer.Length)) > 0)
           {
               dest.Write(buffer, 0, bytesRead);
           }

       }
       Console.WriteLine("Response Content:");
       Console.WriteLine(Encoding.UTF8.GetString(dest.ToArray()));
   }

Uploading an Object
-------------------

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an ObsClient instance.
   ObsClient client = new ObsClient(accessKey, secretKey, config);

   // Specify the validity period of the URL to 3600 seconds.
   long exipreSeconds = 3600;

   CreateTemporarySignatureRequest request = new CreateTemporarySignatureRequest();
   request.BucketName = "bucketname";
   request.ObjectKey = "objectkey";
   request.Method = HttpVerb.PUT;
   request.Expires = exipreSeconds;

   CreateTemporarySignatureResponse response = client.CreateTemporarySignature(request);
   Console.WriteLine("Creating object using temporary signature url:");
   Console.WriteLine("\t" + response.SignUrl);

   // Use a PUT request to upload an object.
   HttpWebRequest webRequest = WebRequest.Create(response.SignUrl) as HttpWebRequest;
   webRequest.Method = "PUT";


   foreach (KeyValuePair<string, string> header in response.ActualSignedRequestHeaders)
   {
       if (!header.Key.Equals("host", StringComparison.OrdinalIgnoreCase))
       {
           webRequest.Headers.Add(header.Key, header.Value);
       }
   }

   webRequest.SendChunked = true;
   webRequest.AllowWriteStreamBuffering = false;
   using (Stream requestStream = webRequest.GetRequestStream())
   {
       byte[] buffer = Encoding.UTF8.GetBytes("Hello OBS");
       requestStream.Write(buffer, 0, buffer.Length);
   }

   HttpWebResponse webResponse = null;
   try
   {
       webResponse = webRequest.GetResponse() as HttpWebResponse;
   }
   catch (WebException ex)
   {
       webResponse = ex.Response as HttpWebResponse;
   }
   Console.WriteLine("Response Status:" + Convert.ToInt32(webResponse.StatusCode));
   using (MemoryStream dest = new MemoryStream())
   {
       using (Stream stream = webResponse.GetResponseStream())
       {
           byte[] buffer = new byte[8192];
           int bytesRead;
           while ((bytesRead = stream.Read(buffer, 0, buffer.Length)) > 0)
           {
               dest.Write(buffer, 0, bytesRead);
           }

       }
       Console.WriteLine("Response Content:");
       Console.WriteLine(Encoding.UTF8.GetString(dest.ToArray()));
   }

Downloading an Object
---------------------

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an ObsClient instance.
   ObsClient client = new ObsClient(accessKey, secretKey, config);

   // Specify the validity period of the URL to 3600 seconds.
   long exipreSeconds = 3600;

   CreateTemporarySignatureRequest request = new CreateTemporarySignatureRequest();
   request.BucketName = "bucketname";
   request.ObjectKey = "objectkey";
   request.Method = HttpVerb.GET;
   request.Expires = exipreSeconds;

   CreateTemporarySignatureResponse response = client.CreateTemporarySignature(request);
   Console.WriteLine("Getting object using temporary signature url:");
   Console.WriteLine("\t" + response.SignUrl);

   // Make a GET request to download an object.
   HttpWebRequest webRequest = WebRequest.Create(response.SignUrl) as HttpWebRequest;
   webRequest.Method = "GET";


   foreach (KeyValuePair<string, string> header in response.ActualSignedRequestHeaders)
   {
       if (!header.Key.Equals("host", StringComparison.OrdinalIgnoreCase))
       {
           webRequest.Headers.Add(header.Key, header.Value);
       }
   }

   HttpWebResponse webResponse = null;
   try
   {
       webResponse = webRequest.GetResponse() as HttpWebResponse;
   }
   catch (WebException ex)
   {
       webResponse = ex.Response as HttpWebResponse;
   }
   Console.WriteLine("Response Status:" + Convert.ToInt32(webResponse.StatusCode));
   using (MemoryStream dest = new MemoryStream())
   {
       using (Stream stream = webResponse.GetResponseStream())
       {
           byte[] buffer = new byte[8192];
           int bytesRead;
           while ((bytesRead = stream.Read(buffer, 0, buffer.Length)) > 0)
           {
               dest.Write(buffer, 0, bytesRead);
           }

       }
       Console.WriteLine("Response Content:");
       Console.WriteLine(Encoding.UTF8.GetString(dest.ToArray()));
   }

Listing Objects
---------------

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an ObsClient instance.
   ObsClient client = new ObsClient(accessKey, secretKey, config);

   // Specify the validity period of the URL to 3600 seconds.
   long exipreSeconds = 3600;

   CreateTemporarySignatureRequest request = new CreateTemporarySignatureRequest();
   request.BucketName = "bucketname";
   request.Method = HttpVerb.GET;
   request.Expires = exipreSeconds;

   CreateTemporarySignatureResponse response = client.CreateTemporarySignature(request);
   Console.WriteLine("Getting object list using temporary signature url:");
   Console.WriteLine("\t" + response.SignUrl);

   // Use a GET request to obtain the object list.
   HttpWebRequest webRequest = WebRequest.Create(response.SignUrl) as HttpWebRequest;
   webRequest.Method = "GET";


   foreach (KeyValuePair<string, string> header in response.ActualSignedRequestHeaders)
   {
       if (!header.Key.Equals("host", StringComparison.OrdinalIgnoreCase))
       {
           webRequest.Headers.Add(header.Key, header.Value);
       }
   }

   HttpWebResponse webResponse = null;
   try
   {
       webResponse = webRequest.GetResponse() as HttpWebResponse;
   }
   catch (WebException ex)
   {
       webResponse = ex.Response as HttpWebResponse;
   }
   Console.WriteLine("Response Status:" + Convert.ToInt32(webResponse.StatusCode));
   using (MemoryStream dest = new MemoryStream())
   {
       using (Stream stream = webResponse.GetResponseStream())
       {
           byte[] buffer = new byte[8192];
           int bytesRead;
           while ((bytesRead = stream.Read(buffer, 0, buffer.Length)) > 0)
           {
               dest.Write(buffer, 0, bytesRead);
           }

       }
       Console.WriteLine("Response Content:");
       Console.WriteLine(Encoding.UTF8.GetString(dest.ToArray()));
   }

Deleting an Object
------------------

.. code-block::

   // Initialize configuration parameters.
   ObsConfig config = new ObsConfig();
   config.Endpoint = "https://your-endpoint";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables AccessKeyID and SecretAccessKey.
   // Obtain an AK/SK pair on the management console.
   string accessKey= Environment.GetEnvironmentVariable("AccessKeyID", EnvironmentVariableTarget.Machine);
   string secretKey= Environment.GetEnvironmentVariable("SecretAccessKey", EnvironmentVariableTarget.Machine);
   // Create an ObsClient instance.
   ObsClient client = new ObsClient(accessKey, secretKey, config);

   // Specify the validity period of the URL to 3600 seconds.
   long exipreSeconds = 3600;

   CreateTemporarySignatureRequest request = new CreateTemporarySignatureRequest();
   request.BucketName = "bucketname";
   request.ObjectKey = "objectkey";
   request.Method = HttpVerb.DELETE;
   request.Expires = exipreSeconds;

   CreateTemporarySignatureResponse response = client.CreateTemporarySignature(request);
   Console.WriteLine("Deleting object using temporary signature url:");
   Console.WriteLine("\t" + response.SignUrl);

   // Use a DELETE request to delete an object.
   HttpWebRequest webRequest = WebRequest.Create(response.SignUrl) as HttpWebRequest;
   webRequest.Method = "DELETE";


   foreach (KeyValuePair<string, string> header in response.ActualSignedRequestHeaders)
   {
       if (!header.Key.Equals("host", StringComparison.OrdinalIgnoreCase))
       {
           webRequest.Headers.Add(header.Key, header.Value);
       }
   }

   HttpWebResponse webResponse = null;
   try
   {
       webResponse = webRequest.GetResponse() as HttpWebResponse;
   }
   catch (WebException ex)
   {
       webResponse = ex.Response as HttpWebResponse;
   }
   Console.WriteLine("Response Status:" + Convert.ToInt32(webResponse.StatusCode));
   using (MemoryStream dest = new MemoryStream())
   {
       using (Stream stream = webResponse.GetResponseStream())
       {
           byte[] buffer = new byte[8192];
           int bytesRead;
           while ((bytesRead = stream.Read(buffer, 0, buffer.Length)) > 0)
           {
               dest.Write(buffer, 0, bytesRead);
           }

       }
       Console.WriteLine("Response Content:");
       Console.WriteLine(Encoding.UTF8.GetString(dest.ToArray()));
   }

.. note::

   **HttpVerb** is an enumeration type defined in OBS .NET SDK, whose value indicates the request method types.
