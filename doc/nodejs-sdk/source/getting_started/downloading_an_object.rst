:original_name: obs_29_0110.html

.. _obs_29_0110:

Downloading an Object
=====================

This example downloads object **example/objectname** from bucket **examplebucket**.

The example code is as follows:

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
         // Specify the object to download (example/objectname in this example).
         Key: 'example/objectname',
       };

       // Download the object as text.
       const result = await obsClient.getObject(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Get object(%s) under the bucket(%s) successful!", params.Key, params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         console.log('Object Content: %s', result.InterfaceResult.Content);
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

.. note::

   -  For more information, see :ref:`Overview <obs_29_0501>`.
