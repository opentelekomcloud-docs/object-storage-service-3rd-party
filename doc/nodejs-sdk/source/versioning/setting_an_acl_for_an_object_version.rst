:original_name: obs_29_0808.html

.. _obs_29_0808:

Setting an ACL for an Object Version
====================================

Function
--------

This API calls **ObsClient.setObjectAcl** to set an ACL for an object version specified by the **VersionId** parameter. For details about the API definition, see :ref:`Configuring an Object ACL <obs_29_0604>`.

Code Examples
-------------

This example sets the ACL to allow all users to read object **example/objectname** from bucket **examplebucket** but only allow user **0a03f5833900d3730f13c00f49d5exxx** to write.

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

   async function setObjectAcl() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify an object. example/objectname is used in this example.
         Key: "example/objectname",
         // Specify the version ID of the object.
         VersionId: 'G001117FCE89978B0000401205D5DC9A',
         // Specify the owner of the object.
         Owner: { 'ID': 'ownerid' },
   // Specify the information about the authorized user.
         Grants: [
           // Grant the write permission to a specified user (0a03f5833900d3730f13c00f49d5exxx in this example).
           { Grantee: { Type: 'CanonicalUser', ID: '0a03f5833900d3730f13c00f49d5exxx' }, Permission: obsClient.enums.PermissionWrite },
           // Grant the read permission to all users.
           { Grantee: { Type: 'Group', URI: obsClient.enums.GroupAllUsers }, Permission: obsClient.enums.PermissionRead },
         ]
       };
       // Set the ACL.
       const result = await obsClient.setObjectAcl(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Set Object(%s)'s acl successful with Bucket(%s)!", params.Key, params.Bucket);
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

   setObjectAcl();

.. note::

   -  For details about the error codes returned during the configuration of permissions for versioned objects, see :ref:`OBS Server-Side Error Codes <obs_29_1601>`.
