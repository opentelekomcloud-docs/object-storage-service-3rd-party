:original_name: obs_29_1308.html

.. _obs_29_1308:

Obtaining the ACL of an Object Version
======================================

Function
--------

This API calls **ObsClient.getObjectAcl** to obtain the ACL of an object version specified by the **VersionId** parameter. For details about the API definition, see :ref:`Obtaining the ACL of an Object <obs_29_0603>`.

Code Examples
-------------

This example obtains the ACL of version **G001117FCE89978B0000401205D5DC9A** of object **example/objectname** in bucket **examplebucket**.

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

   async function getObjectAcl() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify the object (example/objectname in this example).
         Key: 'example/objectname',
         // Specify the version ID of the object.
         VersionId: 'G001117FCE89978B0000401205D5DC9A'
       };
       // Obtain the object ACL.
       const result = await obsClient.getObjectAcl(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Get object(%s)'s acl successful with bucket(%s)!", params.Key, params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         console.log('Owner[ID]: %s', result.InterfaceResult.Owner.ID);
         console.log('Owner[Name]: %s', result.InterfaceResult.Owner.Name);
         for (let i = 0; i < result.InterfaceResult.Grants.length; i++) {
           const grant = result.InterfaceResult.Grants[i];
           fmt.Printf("Grant[%d]-Type:%s, ID:%s, URI:%s, Permission:%s\n",
             index, grant.Grantee.Type, grant.Grantee.ID, grant.Grantee.URI, grant.Permission);
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

   getObjectAcl();

.. note::

   -  For details about the error codes returned during the configuration of permissions for versioned objects, see :ref:`OBS Server-Side Error Codes <obs_29_1601>`.
