:original_name: obs_29_1901.html

.. _obs_29_1901:

Multipart Upload APIs
=====================

To upload a large file, multipart upload is recommended. Multipart upload is applicable to many scenarios. Below are some examples.

-  Files to be uploaded are larger than 100 MB.
-  The network connection to the OBS server breaks often.
-  Sizes of files to be uploaded are uncertain.

Multipart upload consists of three phases:

#. :ref:`Initiating a Multipart Upload <obs_29_1902>`
#. :ref:`Uploading a Part <obs_29_1903>`
#. :ref:`Assembling Parts <obs_29_1904>` or :ref:`Aborting a Multipart Upload <obs_29_1908>`

Multipart upload is mainly used for large file upload or when the network connection is poor. This example uploads a large file in parts concurrently:

.. code-block::

   // Import the OBS library.
   // Use npm to install the client.
   const ObsClient = require('esdk-obs-nodejs');
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');
   const fs = require('fs');

   // Create an ObsClient instance.
   var obsClient = new ObsClient({
     // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
     // Obtain an AK/SK pair on the management console.
     access_key_id: process.env.ACCESS_KEY_ID,
     secret_access_key: process.env.SECRET_ACCESS_KEY,
     // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
     // security_token: process.env.SECURITY_TOKEN,
     // Enter the endpoint of the region where the bucket is located.
     server: "https://your-endpoint"
   });

   // Specify the bucket name.
   const Bucket = 'bucketname'
   // Specify an object (example/objectname in this example).
   const Key = 'objectname'

   // Specify the part size.
   const DEFAULT_PART_SIZE = 9 * 1024 * 1024;
   // Set the number of concurrent parts to 20.
   const CONCURRENCY = 20

   // Prepare multipart upload parameters.
   const preparePartParams = (Bucket, Key, UploadId) => (sampleFile, partSize = DEFAULT_PART_SIZE) => {
       try {
           const fileSize = fs.lstatSync(sampleFile).size;
           const partCount = fileSize % partSize === 0 ? Math.floor(fileSize / partSize) : Math.floor(fileSize / partSize) + 1;

           const uploadPartParams = [];
           // Specify the concurrent upload.
           for (let i = 0; i < partCount; i++) {
               // Start position of parts in the file
               let Offset = i * partSize;
               // Part size
               let currPartSize = (i + 1 === partCount) ? fileSize - Offset : partSize;
               // Part number
               let PartNumber = i + 1;
               uploadPartParams.push({
                   Bucket,
                   Key,
                   PartNumber,
                   UploadId,
                   Offset,
                   SourceFile: sampleFile,
                   PartSize: currPartSize,
               });
           };

           return ({ uploadPartParams, fileSize });
       } catch (error) {
           console.log(error)
       };
   };


   /**
    * uploadSuccessSize: Size of the parts that have been uploaded
    * uploadSuccessCount: Number of the parts that have been uploaded
    * concurrency: Current concurrency
    */
   let uploadSuccessSize = 0;
   let uploadSuccessCount = 0;
   let concurrency = 0

   const parts = [];

   // Upload parts.
   const uploadPart = (uploadPartParam, otherUploadPartInfo) => {
       const partCount = otherUploadPartInfo.partCount;
       const fileSize = otherUploadPartInfo.fileSize;
       concurrency++;
       return obsClient
           .uploadPart(uploadPartParam)
           .then(result => {
               const { PartNumber, PartSize } = uploadPartParam;
               if (result.CommonMsg.Status < 300) {
                   uploadSuccessCount++;
                   uploadSuccessSize += PartSize;
                                   // Print the upload progress.
                   console.log(`the current concurrent count is ${concurrency} | uploaded segment: ${uploadSuccessCount}/${partCount}. the progress is ${((uploadSuccessSize / fileSize) * 100).toFixed(2)}% | the partNumber ${PartNumber} upload succeeded.`);
                   parts.push({ PartNumber, ETag: result.InterfaceResult.ETag });
               } else {
                   console.log(result.CommonMsg.Code, parts);
               };
               concurrency--;
           }).catch(function (err) {
               console.log(err);
               throw err;
           })
   };

   // Multipart upload
   const uploadFile = (sourceFile) => {
           // Initiate the multipart upload task.
       obsClient.initiateMultipartUpload({
           Bucket,
           Key
       }).then(res => {
           const Status = res.CommonMsg.Status;
           const UploadId = res.InterfaceResult.UploadId;

           if (typeof Status === 'number' && Status > 300) {
               console.log(`initiateMultipartUpload failed! Status:${Status}`);
               return;
           };

           const partParams = preparePartParams(Bucket, Key, UploadId)(sourceFile);
           const uploadPartParams = partParams.uploadPartParams;
           const fileSize = partParams.fileSize;
           const partCount = uploadPartParams.length;
           const otherUploadPartInfo = { fileSize, partCount };

           // Call the parallel upload function.
           parallelFunc(uploadPartParams, (param) => uploadPart(param, otherUploadPartInfo), CONCURRENCY)
               .then(() => {
                                   // Assemble parts.
                   obsClient.completeMultipartUpload({
                       Bucket,
                       Key,
                       UploadId,
                       Parts: parts.sort((a, b) => a.PartNumber - b.PartNumber)
                   }, (err, result) => {
                       if (err) {
                           console.log('Error-->' + err);
                       } else {
                           console.log('Status-->' + result.CommonMsg.Status);
                       };
                   });
               });

       }).catch(function (err) {
           console.log(err)
       });
   };


   /**
    * Implement the parallel function execution.
    * @param {Array} params Parameter array of the callback function
    * @param {Promise} promiseFn Callback function
    * @param {number} limit Number of parallel parts
    */
   const parallelFunc = (params, promiseFn, limit) => {
       return new Promise((resolve) => {
           let concurrency = 0;
           let finished = 0;
           const count = params.length;
           const run = (param) => {
               concurrency++;
               promiseFn(param)
                   .then(() => {
                       concurrency--;
                       drainQueue();
                       finished++;
                       if (finished === count) {
                           resolve();
                       };
                   });
           };
           const drainQueue = () => {
               while (params.length > 0 && concurrency < limit) {
                   var param = params.shift();
                   run(param);
               };
           };
           drainQueue();
       });

   };

   uploadFile('localfile');

.. note::

   When uploading a large file in parts, you need to use the **Offset** and **PartSize** parameters to specify the start and end positions of each part in the file.

.. caution::

   If the concurrency value is too great, timeout may occur due to network instability. In such case, you need to reduce that value.
