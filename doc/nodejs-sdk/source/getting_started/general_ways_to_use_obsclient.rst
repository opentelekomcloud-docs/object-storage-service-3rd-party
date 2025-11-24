:original_name: obs_29_0113.html

.. _obs_29_0113:

General Ways to Use ObsClient
=============================

Result Returned via a Callback Function
---------------------------------------

**ObsClient** returns the results by using a callback function that contains two parameters in sequence: the exception information parameter and the :ref:`SDK common result object <obs_29_1602>` parameter. If the exception information parameter in the callback function is not null, an error occurs during the API calling. Otherwise, the API is called. In such conditions, you need to obtain the HTTP status code from the :ref:`SDK common result object <obs_29_1602>` parameter to check whether the operation is successful. Sample code:

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

   // Construct request parameters for bucket operations.
   var requestParam1 = {
          Bucket : 'bucketname'
          // Other fields.
   };

   var callback1 = (err, result) => {
          // Process the result of a bucket-related API call.
   };

   // Call the APIs for bucket operations, such as creating a bucket.
   obsClient.createBucket(requestParam1, callback1);

   // Construct request parameters for object operations.
   var requestParam2 = {
          Bucket : 'bucketname',
          Key : 'objectname'
          // Other fields.
   };

   var callback2 = (err, result) => {
          // Process the result of an object-related API call.
   };

   // Call an object-related API, such as the API for downloading an object.
   obsClient.getObject(requestParam2, callback2);

.. note::

   For APIs used for bucket operations, the **Bucket** parameter contained in the request object indicates the bucket name. For APIs used for object operations, the **Bucket** and **Key** parameters contained in the request object specify the bucket name and object name, respectively.

Sample code:

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

   // Call APIs to perform operations, such as uploading an object.
   obsClient.putObject({
          Bucket : 'bucketname',
          Key : 'objectname',
          Body : 'Hello OBS'
   }, (err, result) => {
          // If the err parameter is not null, an error occurs during the API calling.
          if(err){
                 console.log('Error-->' + err);
          }else{
                 // If the exception information is null, the API call is complete. In such conditions, you need to check the HTTP status code.
                 if(result.CommonMsg.Status < 300){// The operation is successful.
                        if(result.InterfaceResult){
                              // Process the business logic after the operation is successful.
                        };
                 }else{// The operation fails. Obtain details about the exception.
                        console.log('Code-->' + result.CommonMsg.Code);
                        console.log('Message-->' + result.CommonMsg.Message);
                        console.log('HostId-->' + result.CommonMsg.HostId);
                        console.log('RequestId-->' + result.CommonMsg.RequestId);
                 };
          };
   });

Result Returned via the Promise Object
--------------------------------------

**ObsClient** supports results returned via the **Promise** object. If no exception is caught by the **catch** method of the **Promise** object, the API calling is complete. In such conditions, you need to obtain the HTTP status code from the :ref:`SDK Common Result Object <obs_29_1602>` to check whether the operation is successful. The following is a code sample:

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


   // Construct request parameters for bucket operations.
   var requestParam1 = {
          Bucket : 'bucketname'
          // Other fields.
   };

   // Call the APIs for bucket operations, such as creating a bucket.
   var promise1 = obsClient.createBucket(requestParam1);
   promise1.then((result) => {
      // Process the API call result.
   }).catch((err)=>{
      // Rectify the fault.
   });

   // Construct request parameters for object operations.
   var requestParam2 = {
          Bucket : 'bucketname',
          Key : 'objectname'
          // Other fields.
   };

   // Call an object-related API, such as the API for downloading an object.
   var promise2 = obsClient.getObject(requestParam2);
   promise2.then((result) => {
      // Process the API call result.
   }).catch((err)=>{
      // Rectify the fault.
   });

.. note::

   For APIs used for bucket operations, the **Bucket** parameter contained in the request object indicates the bucket name. For APIs used for object operations, the **Bucket** and **Key** parameters contained in the request object specify the bucket name and object name, respectively.

Sample code:

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

   // Call APIs to perform operations, such as uploading an object.
   obsClient.putObject({
          Bucket : 'bucketname',
          Key : 'objectname',
          Body : 'Hello OBS'
   }).then((result) => {
       // If no exception occurs and the API call is complete, check the HTTP status code.
       if(result.CommonMsg.Status < 300){// Operation succeeded
           if(result.InterfaceResult){
               // Process the business logic after the operation is successful.
           };
   }else{// The operation fails. Obtain details about the exception.
           console.log('Code-->' + result.CommonMsg.Code);
           console.log('Message-->' + result.CommonMsg.Message);
           console.log('HostId-->' + result.CommonMsg.HostId);
           console.log('RequestId-->' + result.CommonMsg.RequestId);
       };
   }).catch((err) => {
       // An exception occurred after the API is called.
       console.error('Error-->' + err);
   });
