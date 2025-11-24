:original_name: obs_29_0701.html

.. _obs_29_0701:

Using a Temporary URL for Authorized Access
===========================================

Function
--------

OBS allows you to create a URL whose Query parameters carry authentication information by specifying the AK and SK, HTTP method, and request parameters. You can provide this URL for other users to grant them temporary access. When generating a URL, you need to specify the validity period of the URL to restrict the access duration of visitors.

To grant other users the temporary permission to perform operations (such as upload), you need to generate a URL for the corresponding request (such as PUT) and provide it for users.

Restrictions
------------

-  If a CORS or signature mismatch error occurs, troubleshoot the issue as follows:

   #. If CORS is not configured, you need to configure CORS rules on OBS Console.
   #. If the signatures do not match, check whether signature parameters are missing or invalid. For example, during an object upload, the backend uses **Content-Type** to calculate the signature and generate a signed URL, but if **Content-Type** is not set or is set to an invalid value when the frontend uses that URL, a CORS error occurs. To resolve this issue, ensure **Content-Type** remains consistent at the frontend and backend.

Method
------

.. code-block::

   ObsClient.createSignedUrlSync(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                  | Mandatory (Yes/No) | Description                                                                                                                                                                          |
   +=================+=======================================================+====================+======================================================================================================================================================================================+
   | Method          | :ref:`HttpMethodType <obs_29_0701__table12153312211>` | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | HTTP method. For details, see :ref:`Table 2 <obs_29_0701__table12153312211>`.                                                                                                        |
   +-----------------+-------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Bucket          | string                                                | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | Bucket name                                                                                                                                                                          |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                     |
   |                 |                                                       |                    | -  A bucket name:                                                                                                                                                                    |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                         |
   |                 |                                                       |                    |    -  Cannot be formatted as an IP address.                                                                                                                                          |
   |                 |                                                       |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                           |
   |                 |                                                       |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                      |
   |                 |                                                       |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                            |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | The value can contain 3 to 63 characters.                                                                                                                                            |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   +-----------------+-------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key             | string                                                | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name.                  |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | The value can contain 1 to 1,024 characters.                                                                                                                                         |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   +-----------------+-------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SpecialParam    | :ref:`SpecialParam <obs_29_0701__table593654162113>`  | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | Sub-resource to be accessed                                                                                                                                                          |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | See :ref:`Table 3 <obs_29_0701__table593654162113>`.                                                                                                                                 |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   +-----------------+-------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Expires         | number                                                | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | Expiration time of the signed URL.                                                                                                                                                   |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | -  The value of this parameter for temporary credentials ranges from **0** to **86400**, in seconds.                                                                                 |
   |                 |                                                       |                    | -  The value of this parameter for permanent keys ranges from **0** to **630720000**, in seconds.                                                                                    |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | 300                                                                                                                                                                                  |
   +-----------------+-------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Headers         | object                                                | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | Headers in the request.                                                                                                                                                              |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   +-----------------+-------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | QueryParams     | object                                                | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | Query parameters in the request.                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Value range**:                                                                                                                                                                     |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | **Default value**:                                                                                                                                                                   |
   |                 |                                                       |                    |                                                                                                                                                                                      |
   |                 |                                                       |                    | None                                                                                                                                                                                 |
   +-----------------+-------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_0701__table12153312211:

.. table:: **Table 2** HttpMethodType

   ======== ====================
   Constant Description
   ======== ====================
   GET      HTTP GET request
   POST     HTTP POST request
   PUT      HTTP PUT request
   DELETE   HTTP DELETE request
   HEAD     HTTP HEAD request
   OPTIONS  HTTP OPTIONS request
   ======== ====================

.. _obs_29_0701__table593654162113:

.. table:: **Table 3** SpecialParam

   +---------------+---------------------------------------------------------------+
   | Constant      | Applicable API                                                |
   +===============+===============================================================+
   | storagePolicy | Specify or obtain bucket storage classes.                     |
   +---------------+---------------------------------------------------------------+
   | quota         | Specify or obtain bucket quotas.                              |
   +---------------+---------------------------------------------------------------+
   | storageinfo   | Obtain bucket storage information.                            |
   +---------------+---------------------------------------------------------------+
   | location      | Obtain bucket locations.                                      |
   +---------------+---------------------------------------------------------------+
   | acl           | Specify or obtain bucket ACLs or object ACLs.                 |
   +---------------+---------------------------------------------------------------+
   | policy        | Specify, obtain, or delete bucket policies.                   |
   +---------------+---------------------------------------------------------------+
   | cors          | Specify, obtain, or delete bucket CORS configurations.        |
   +---------------+---------------------------------------------------------------+
   | versioning    | Specify or obtain bucket versioning statuses.                 |
   +---------------+---------------------------------------------------------------+
   | website       | Specify, obtain, or delete bucket website configurations.     |
   +---------------+---------------------------------------------------------------+
   | logging       | Specify or obtain bucket logging settings.                    |
   +---------------+---------------------------------------------------------------+
   | lifecycle     | Specify, obtain, or delete lifecycle rules of buckets.        |
   +---------------+---------------------------------------------------------------+
   | notification  | Specify or obtain the notification configurations of buckets. |
   +---------------+---------------------------------------------------------------+
   | tagging       | Specify, obtain, or delete bucket tags.                       |
   +---------------+---------------------------------------------------------------+
   | append        | Append data to an object.                                     |
   +---------------+---------------------------------------------------------------+
   | delete        | Batch delete objects.                                         |
   +---------------+---------------------------------------------------------------+
   | versions      | List object versions in buckets.                              |
   +---------------+---------------------------------------------------------------+
   | uploads       | List or initiate multipart uploads in buckets.                |
   +---------------+---------------------------------------------------------------+
   | restore       | Restore Cold objects.                                         |
   +---------------+---------------------------------------------------------------+

Responses
---------

.. table:: **Table 4** Responses

   +----------------------------+-----------------------+---------------------------------------------------------------------------------+
   | Parameter                  | Type                  | Description                                                                     |
   +============================+=======================+=================================================================================+
   | SignedUrl                  | string                | **Explanation:**                                                                |
   |                            |                       |                                                                                 |
   |                            |                       | The signed URL that carries the authentication information.                     |
   +----------------------------+-----------------------+---------------------------------------------------------------------------------+
   | ActualSignedRequestHeaders | object                | **Explanation:**                                                                |
   |                            |                       |                                                                                 |
   |                            |                       | Headers that need to be included in the request initiated using the signed URL. |
   +----------------------------+-----------------------+---------------------------------------------------------------------------------+

To access OBS using a temporary URL generated by the OBS Node.js SDK, perform the following steps:

#. Call **ObsClient.createSignedUrlSync** to generate a signed URL.
#. Use any HTTP library to make an HTTP/HTTPS request to OBS.

.. caution::

   If a CORS or signature mismatch error occurs, refer to the following steps to troubleshoot the issue:

   #. If CORS is not configured, you need to configure CORS rules on OBS Console.
   #. If the signatures do not match, check whether signature parameters are correct by referring to . For example, during an object upload, the backend uses **Content-Type** to calculate the signature and generate an authorized URL, but if **Content-Type** is not set or set incorrectly when the frontend uses the authorized URL, a CORS error occurs. To avoid this issue, ensure that **Content-Type** fields at both the frontend and backend are kept consistent.

The following code examples use a temporary URL to create a bucket or upload, download, list, or delete objects.

Code Examples: Creating a Bucket
--------------------------------

This example creates a bucket using a temporary URL.

.. code-block::

   // Import the OBS library.
   // Use npm to install the client.
   var ObsClient = require('esdk-obs-nodejs');
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');
   var https = require('https');
   var urlLib = require('url');
   var crypto = require('crypto');

   // Create an ObsClient instance.
   var obsClient = new ObsClient({
          // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
          // Obtain an AK/SK pair on the management console.
          access_key_id: process.env.ACCESS_KEY_ID,
          secret_access_key: process.env.SECRET_ACCESS_KEY,
          server : 'https://your-endpoint'
   });

   let bucketName = 'bucketname';
   let method = 'PUT';
   let res = obsClient.createSignedUrlSync({Method : method, Bucket : bucketName});
   let location = 'your-location';
   let content  = `<CreateBucketConfiguration><LocationConstraint>${location}</LocationConstraint></CreateBucketConfiguration>`;

   // Make a PUT request to create a bucket.
   var url = urlLib.parse(res.SignedUrl);
   var req = https.request({
          method : method,
          host : url.hostname,
          port : url.port,
          path : url.path,
          rejectUnauthorized : false,
          headers : res.ActualSignedRequestHeaders || {}
   });


   console.log('Creating bucket using url:' + res.SignedUrl);

   req.on('response',   (serverback) => {
          var buffers = [];
          serverback.on('data', (data) => {
                 buffers.push(data);
          }).on('end', () => {

                 if(serverback.statusCode < 300){
                        console.log('Creating bucket using temporary signature succeed.');
                 }else{
                        console.log('Creating bucket using temporary signature failed!');
                        console.log('status:' + serverback.statusCode);
                        console.log('\n');
                 };
                 buffers = Buffer.concat(buffers);
                 if(buffers.length > 0){
                        console.log(buffers.toString());
                 };
                 console.log('\n');
          });
   }).on('error',(err) => {
          console.log('Creating bucket using temporary signature failed!');
          console.log(err);
          console.log('\n');
   });

   if(content){
          req.write(content);
   };
   req.end();

Code Examples: Uploading an Object
----------------------------------

This example uploads an object using a temporary URL.

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

   function createSignedUrlSync() {
     // Specify the HTTP method. PUT is used in this example.
     const method = 'PUT';
     const params = {
       // Specify the bucket name.
       Bucket: "examplebucket",
       // Specify an object (example/objectname in this example).
       Key: "example/objectname",
       // Specify the HTTP method.
       Method: method,
       // Specify the validity period of the signed URL, in seconds (3600 in this example).
       Expires: 3600,
       // Specify the headers carried in the request.
       Headers: {
         "Content-Type": "text/plain",
       }
     };

     // Create a signed URL for uploading an object.
     const res = obsClient.createSignedUrlSync(params);
     console.log("SignedUrl: %s", res.SignedUrl);
     console.log("ActualSignedRequestHeaders: %v", res.ActualSignedRequestHeaders);

     let content  = 'Hello OBS';
     // Make a PUT request to upload an object.
     var url = urlLib.parse(res.SignedUrl);
     var req = https.request({
       method: method,
       host: url.hostname,
       port: url.port,
       path: url.path,
       rejectUnauthorized: false,
       headers: res.ActualSignedRequestHeaders || {}
     });
     console.log('Creating object using url:' + res.SignedUrl);

     req.on('response', (serverback) => {
       var buffers = [];
       serverback.on('data', (data) => {
         buffers.push(data);
       }).on('end', () => {
         if (serverback.statusCode < 300) {
           console.log('Creating object using temporary signature succeed.');
         } else {
           console.log('Creating object using temporary signature failed!');
           console.log('status:' + serverback.statusCode);
           console.log('\n');
         };
         buffers = Buffer.concat(buffers);
         if (buffers.length > 0) {
           console.log(buffers.toString());
         };
         console.log('\n');
       });
     }).on('error', (err) => {
       console.log('Creating object using temporary signature failed!');
       console.log(err);
       console.log('\n');
     });
     if (content) {
       req.write(content);
     };
     req.end();
   };

   createSignedUrlSync();

Code Examples: Downloading an Object
------------------------------------

This example downloads an object using a temporary URL.

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

   function createSignedUrlSync() {
     // Specify the HTTP method. GET is used in this example.
     const method = 'GET';

     const params = {
       // Specify the bucket name.
       Bucket: "examplebucket",
       // Specify an object (example/objectname in this example).
       Key: "example/objectname",
       // Specify the HTTP method.
       Method: method,
       // Specify the validity period of the signed URL, in seconds (3600 in this example).
       Expires: 3600,
     };

     // Make a GET request to download an object.
     var url = urlLib.parse(res.SignedUrl);
     var req = https.request({
       method: method,
       host: url.hostname,
       port: url.port,
       path: url.path,
       rejectUnauthorized: false,
       headers: res.ActualSignedRequestHeaders || {}
     });
     console.log('Creating object using url:' + res.SignedUrl);

     req.on('response', (serverback) => {
       var buffers = [];
       serverback.on('data', (data) => {
         buffers.push(data);
       }).on('end', () => {
         if (serverback.statusCode < 300) {
           console.log('Getting object using temporary signature succeed.');
         } else {
           console.log('Getting object using temporary signature failed!');
           console.log('status:' + serverback.statusCode);
           console.log('\n');
         };
         buffers = Buffer.concat(buffers);
         if (buffers.length > 0) {
           console.log(buffers.toString());
         };
         console.log('\n');
       });
     }).on('error', (err) => {
       console.log('Getting object using temporary signature failed!');
       console.log(err);
       console.log('\n');
     });
     req.end();
   };

   createSignedUrlSync();

Code Examples: Listing Objects
------------------------------

This example lists objects using a temporary URL.

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

   function createSignedUrlSync() {
     // Specify the HTTP method. GET is used in this example.
     const method = 'GET';

     const params = {
       // Specify the bucket name.
       Bucket: "examplebucket",
       // Specify the HTTP method.
       Method: method,
       // Specify the validity period of the signed URL, in seconds (3600 in this example).
       Expires: 3600,
     };

     // Make a GET request to obtain the object list.
     var url = urlLib.parse(res.SignedUrl);
     var req = https.request({
       method: method,
       host: url.hostname,
       port: url.port,
       path: url.path,
       rejectUnauthorized: false,
       headers: res.ActualSignedRequestHeaders || {}
     });
     console.log('Listing object using url:' + res.SignedUrl);

     req.on('response', (serverback) => {
       var buffers = [];
       serverback.on('data', (data) => {
         buffers.push(data);
       }).on('end', () => {
         if (serverback.statusCode < 300) {
           console.log('Listing object using temporary signature succeed.');
         } else {
           console.log('Listing object using temporary signature failed!');
           console.log('status:' + serverback.statusCode);
           console.log('\n');
         };
         buffers = Buffer.concat(buffers);
         if (buffers.length > 0) {
           console.log(buffers.toString());
         };
         console.log('\n');
       });
     }).on('error', (err) => {
       console.log('Listing object using temporary signature failed!');
       console.log(err);
       console.log('\n');
     });
     req.end();
   };

   createSignedUrlSync();

Code Examples: Deleting an Object
---------------------------------

This example deletes an object using a temporary URL.

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

   function createSignedUrlSync() {
     // Specify the HTTP method. DELETE is used in this example.
     const method = 'DELETE';
     const params = {
       // Specify the bucket name.
       Bucket: "examplebucket",
       // Specify an object (example/objectname in this example).
       Key: "example/objectname",
       // Specify the HTTP method.
       Method: method,
       // Specify the validity period of the signed URL, in seconds (3600 in this example).
       Expires: 3600,
     };

     // Make a DELETE request to delete the object.
     var url = urlLib.parse(res.SignedUrl);
     var req = https.request({
       method: method,
       host: url.hostname,
       port: url.port,
       path: url.path,
       rejectUnauthorized: false,
       headers: res.ActualSignedRequestHeaders || {}
     });
     console.log('Deleting object using url:' + res.SignedUrl);
     req.on('response', (serverback) => {
       var buffers = [];
       serverback.on('data', (data) => {
         buffers.push(data);
       }).on('end', () => {
         if (serverback.statusCode < 300) {
           console.log('Deleting object using temporary signature succeed.');
         } else {
           console.log('Deleting object using temporary signature failed!');
           console.log('status:' + serverback.statusCode);
           console.log('\n');
         };
         buffers = Buffer.concat(buffers);
         if (buffers.length > 0) {
           console.log(buffers.toString());
         };
         console.log('\n');
       });
     }).on('error', (err) => {
       console.log('Deleting object using temporary signature failed!');
       console.log(err);
       console.log('\n');
     });
     req.end();
   };

   createSignedUrlSync();
