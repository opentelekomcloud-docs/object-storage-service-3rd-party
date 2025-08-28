:original_name: obs_21_0618.html

.. _obs_21_0618:

Code Example of a Multipart Upload
==================================

Multipart upload is mainly used for large file upload or when the network connection is poor.

You can use **UploadPartRequest.setOffset** and **UploadPartRequest.setPartSize** to set the start and end positions for uploading a part.

This example uploads a large file by concurrently uploading parts.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.CompleteMultipartUploadRequest;
   import com.obs.services.model.InitiateMultipartUploadRequest;
   import com.obs.services.model.InitiateMultipartUploadResult;
   import com.obs.services.model.PartEtag;
   import com.obs.services.model.UploadPartRequest;
   import com.obs.services.model.UploadPartResult;
   import java.io.File;
   import java.util.ArrayList;
   import java.util.Collections;
   import java.util.List;
   import java.util.concurrent.ExecutorService;
   import java.util.concurrent.Executors;
   import java.util.concurrent.TimeUnit;
   public class ConcurrentUploadPart001 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           String securityToken = System.getenv("SECURITY_TOKEN");
           // Enter the endpoint corresponding to the region where the bucket is to be created.
           String endPoint = "https://your-endpoint";
           // Obtain an endpoint using environment variables or import it in other ways.
           //String endPoint = System.getenv("ENDPOINT");

           // Create an ObsClient instance.
           // Use the permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use the temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               final String bucketName = "examplebucket";
               final String objectKey = "objectname";
               // Initialize the thread pool.
               ExecutorService executorService = Executors.newFixedThreadPool(20);
               final File largeFile = new File("localfile");
               // Initiate a multipart upload.
               InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, objectKey);
               InitiateMultipartUploadResult result = obsClient.initiateMultipartUpload(request);
               final String uploadId = result.getUploadId();
               System.out.println("\t" + uploadId + "\n");
               // Set the part size to 100 MB.
               long partSize = 100 * 1024 * 1024L;
               long fileSize = largeFile.length();
               // Calculate the number of parts to be uploaded.
               long partCount = fileSize % partSize == 0 ? fileSize / partSize : fileSize / partSize + 1;
               final List<PartEtag> partEtags = Collections.synchronizedList(new ArrayList<PartEtag>());
               // Start uploading parts concurrently.
               for (int i = 0; i < partCount; i++) {
                   // Set the start position of a part in the file.
                   final long offset = i * partSize;
                   // Set the part size.
                   final long currPartSize = (i + 1 == partCount) ? fileSize - offset : partSize;
                   // Set the part number.
                   final int partNumber = i + 1;
                   executorService.execute(
                           new Runnable() {
                               @Override
                               public void run() {
                                   UploadPartRequest uploadPartRequest = new UploadPartRequest();
                                   uploadPartRequest.setBucketName(bucketName);
                                   uploadPartRequest.setObjectKey(objectKey);
                                   uploadPartRequest.setUploadId(uploadId);
                                   uploadPartRequest.setFile(largeFile);
                                   uploadPartRequest.setPartSize(currPartSize);
                                   uploadPartRequest.setOffset(offset);
                                   uploadPartRequest.setPartNumber(partNumber);
                                   UploadPartResult uploadPartResult;
                                   try {
                                       uploadPartResult = obsClient.uploadPart(uploadPartRequest);
                                       System.out.println("Part#" + partNumber + " done\n");
                                       partEtags.add(
                                               new PartEtag(uploadPartResult.getEtag(), uploadPartResult.getPartNumber()));
                                   } catch (ObsException e) {
                                       e.printStackTrace();
                                   }
                               }
                           });
               }
               // Wait until the upload is complete.
               executorService.shutdown();
               while (!executorService.isTerminated()) {
                   try {
                       executorService.awaitTermination(5, TimeUnit.SECONDS);
                   } catch (InterruptedException e) {
                       e.printStackTrace();
                   }
               }
               // Assemble parts.
               CompleteMultipartUploadRequest completeMultipartUploadRequest =
                       new CompleteMultipartUploadRequest(bucketName, objectKey, uploadId, partEtags);
               obsClient.completeMultipartUpload(completeMultipartUploadRequest);
               System.out.println("completeMultipartUpload successfully");
           } catch (ObsException e) {
               System.out.println("CompleteMultipartUpload failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code:" + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message:" + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
               e.printStackTrace();
           } catch (Exception e) {
               System.out.println("completeMultipartUpload failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
