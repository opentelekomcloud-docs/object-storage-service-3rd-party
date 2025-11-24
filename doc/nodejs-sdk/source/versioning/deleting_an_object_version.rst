:original_name: obs_29_0809.html

.. _obs_29_0809:

Deleting an Object Version
==========================

Function
--------

You can call **ObsClient.deleteObject** to delete an object version specified by the **VersionId** parameter. For details about the API definition, see :ref:`Deleting an Object <obs_29_0606>`.

You can also call **ObsClient.deleteObjects** to delete multiple object versions at a time by passing all of their **VersionId** values. For details about the API definition, see :ref:`Batch Deleting Objects <obs_29_0607>`.

Code Examples: Deleting an Object Version
-----------------------------------------

This example deletes version **G001117FCE89978B0000401205D5DC9A** of object **example/objectname** from bucket **examplebucket**.

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

   async function deleteObject() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify the object (example/objectname in this example) to delete.
         Key: 'example/objectname',
         // Specify the ID of the object version.
         VersionId: 'G001117FCE89978B0000401205D5DC9A'
       };
       // Delete a version of an object.
       const result = await obsClient.deleteObject(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Delete object(%s) under the bucket(%s) successful!", params.Key, params.Bucket);
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

   deleteObject();

Code Examples: Deleting Object Versions
---------------------------------------

This example deletes objects **objectname1**, **objectname2**, and **objectname3** from bucket **examplebucket** in a batch.

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

   async function deleteObjects() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify the object list to delete.
         Objects: [
           { Key: 'objectname1', VersionId: "version1" },
           { Key: 'objectname2', VersionId: "version2" },
           { Key: 'objectname3', VersionId: "version3" }
         ]
       };
       // Delete the objects in a batch.
       const result = await obsClient.deleteObjects(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Delete objects under the bucket(%s) successful!", params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         // Return details about which objects were deleted.
         console.log('Deleteds:');
         for (let i = 0; i < result.InterfaceResult.Deleteds.length; i++) {
           const deleted = result.InterfaceResult.Deleteds[i];
           console.log("Deleted[%d]-Key:%s, VersionId:%s", i, deleted.Key, deleted.VersionId);
         };
         // Return details about which objects were not deleted.
         console.log('Errors:');
         for (let i = 0; i < result.InterfaceResult.Errors.length; i++) {
           const err = result.InterfaceResult.Errors[i];
           console.log("Errors[%d]-Key:%s, Code:%s", i, err.Key, err.Code);
         };
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

   deleteObjects();
