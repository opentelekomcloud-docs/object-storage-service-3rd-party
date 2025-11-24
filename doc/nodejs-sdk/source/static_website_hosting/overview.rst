:original_name: obs_29_1201.html

.. _obs_29_1201:

Overview
========

You can upload the content files of the static website to your bucket in OBS as objects and configure the **public-read** permission on the files, and then configure the static website hosting mode for your bucket to host your static websites in OBS. After this, when third-party users access your websites, they actually access the objects in your bucket in OBS. When using static website hosting, you can configure request redirection to redirect specific or all requests.

You can perform the following to host a website file in a bucket:

#. Upload a website file to your bucket in OBS as an object and specify the MIME type for the object.
#. Set the object ACL to public read.
#. Access the object using a browser.

Sample code:

::

   // Import the OBS library.
   // Use npm for installation.
   const ObsClient = require("esdk-obs-nodejs");
   // Use the source code for installation.
   // var ObsClient = require('./lib/obs');

   // Create an ObsClient instance.
   const obsClient = new ObsClient({
     //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
     //Obtain an AK/SK pair on the management console.
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
         // Specify an object. test.html is used in this example.
         Key: 'test.html',
         Body: '<html><header></header><body><h1>Hello OBS</h1></body></html>',
         // Set the MIME type for the object.
         ContentType: 'text/html',
         // Set the object ACL to public read.
         ACL: obsClient.enums.AclPublicRead

       };
       // Upload the object.
       const result = await obsClient.putObject(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Put object(%s) under the bucket(%s) successful!!", params.Key, params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         console.log("StorageClass:%s, ETag:%s", result.InterfaceResult.StorageClass, result.InterfaceResult.ETag);
         return;
       }
       console.log("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
       console.log("Status: %d", result.CommonMsg.Status);
       console.log("Code: %s", result.CommonMsg.Code);
       console.log("Message: %s", result.CommonMsg.Message);
       console.log("RequestId: %s", result.CommonMsg.RequestId);
     } catch (error) {
       console.log("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
       console.log(error);
     }
   }

   putObject();

.. note::

   -  You can enter **http://**\ examplebucket\ **.**\ *your-endpoint*\ **/test.html** in a browser to access the file hosted using the sample code.
