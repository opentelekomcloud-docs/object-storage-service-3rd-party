:original_name: obs_29_0407.html

.. _obs_29_0407:

Configuring a Lifecycle Rule When Uploading an Object
=====================================================

Function
--------

When uploading an object or initiating a multipart upload, you can set an expiration time for the object using **Expires**. This method only supports setting the object expiration time in days, and the expired objects will be automatically deleted by OBS, with a higher priority than bucket lifecycle rules.

Code Examples: Uploading an Object
----------------------------------

When uploading an object, you can specify when it expires after being created.

.. code-block::

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

   async function putObject() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify an object (example/objectname in this example).
         Key: "example/objectname",
         // localfile indicates the path of the local file to be uploaded, which must include the file name.
         SourceFile : 'localfile',
         // Specify how many days can pass before the object expires (30 in this example).
         Expires : 30
       };
       // Upload a file.
       const result = await obsClient.putObject(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Put bucket(%s) successful!", params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
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

   putObject()

Code Examples: Initiating a Multipart Upload
--------------------------------------------

When initiating a multipart upload, you can specify when the object expires after it is created.

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

   async function initiateMultipartUpload() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify an object (example/objectname in this example).
         Key: "example/objectname",
         // Specify how many days can pass before the object expires (30 in this example).
         Expires : 30
       };
       // Initiate the multipart upload.
       const result = await obsClient.initiateMultipartUpload(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Initiate multipart upload successfully with bucket(%s) and object(%s)!", params.Bucket, params.Key);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         console.log("UploadId: %s", result.InterfaceResult.UploadId);
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

   initiateMultipartUpload();
