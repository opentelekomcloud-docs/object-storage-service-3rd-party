:original_name: obs_29_0111.html

.. _obs_29_0111:

Listing Objects
===============

After objects are uploaded, you may want to view the objects contained in a bucket. Sample code is as follows:

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

   async function listObjects() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
       };
       // List objects in a bucket.
       const result = await obsClient.listObjects(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("List objects under the bucket(%s) successful!", params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         for (let j = 0; j < result.InterfaceResult.Contents.length; j++) {
           const val = result.InterfaceResult.Contents[j];
           console.log('Content[%d]-OwnerId:%s, ETag:%s, Key:%s, LastModified:%s, Size:%d',
             j, val.Owner.ID, val.ETag, val.Key, val.LastModified, val.Size);
         };
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

   listObjects();

.. note::

   -  In the sample code, 1000 objects will be listed, by default.
   -  For more information, see :ref:`Listing Objects <obs_29_0605>`.
