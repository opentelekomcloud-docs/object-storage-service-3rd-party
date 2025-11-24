:original_name: obs_29_0507.html

.. _obs_29_0507:

Rewriting Response Headers
==========================

When downloading an object, you can rewrite some HTTP/HTTPS response headers. The following table lists rewritable response headers.

+----------------------------+-----------------------------------------------------------+
| Parameter                  | Description                                               |
+============================+===========================================================+
| ResponseContentType        | Rewrites **Content-Type** in HTTP/HTTPS responses.        |
+----------------------------+-----------------------------------------------------------+
| ResponseContentLanguage    | Rewrites **Content-Language** in HTTP/HTTPS responses.    |
+----------------------------+-----------------------------------------------------------+
| ResponseExpires            | Rewrites **Expires** in HTTP/HTTPS responses.             |
+----------------------------+-----------------------------------------------------------+
| ResponseCacheControl       | Rewrites **Cache-Control** in HTTP/HTTPS responses.       |
+----------------------------+-----------------------------------------------------------+
| ResponseContentDisposition | Rewrites **Content-Disposition** in HTTP/HTTPS responses. |
+----------------------------+-----------------------------------------------------------+
| ResponseContentEncoding    | Rewrites **Content-Encoding** in HTTP/HTTPS responses.    |
+----------------------------+-----------------------------------------------------------+

Code Examples
-------------

This code example rewrites response headers.

::

   // Import the OBS library.
   // Use npm to install the client.
   const ObsClient = require("esdk-obs-nodejs");
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');
   // Create an instance of ObsClient.
   const obsClient = new ObsClient({
     // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
     // Obtain an AK/SK pair on the management console.
     access_key_id: process.env.ACCESS_KEY_ID,
     secret_access_key: process.env.SECRET_ACCESS_KEY,
     // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
     // security_token: process.env.SECURITY_TOKEN,
     // Enter the endpoint of the region where the bucket is located.
     server: "https://your-endpoint"
   });

   async function getObject() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify the object (example/objectname in this example).
         Key: 'example/objectname',
         // Rewrite a response header (Content-Type in this example).
         ResponseContentType : 'image/jpeg'
       };

       // Rewrite the response header.
       const result = await obsClient.getObject(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Get object(%s) under the bucket(%s) successful!", params.Key, params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         // Obtain the response header that was rewritten.
         console.log("ContentType:%s", result.InterfaceResult.ContentType)
         return;
       };
       console.log("An ObsError was found, which means your request sent to OBS was rejected with an error response.");
       console.log("Status: %d", result.CommonMsg.Status);
       console.log("Code: %s", result.CommonMsg.Code);
       console.log("Message: %s", result.CommonMsg.Message);
       console.log("RequestId: %s", result.CommonMsg.RequestId);
     } catch (error) {
       console.log("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.");
       console.log(error);
     };
   };

   getObject();
