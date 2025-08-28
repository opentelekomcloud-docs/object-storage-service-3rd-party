:original_name: obs_21_0100.html

.. _obs_21_0100:

Getting Started
===============

This section introduces how to use OBS SDK for Java to perform some basic actions, such as creating a bucket, and uploading, downloading, listing, and deleting objects.

Preparations
------------

Ensure you have made the following preparations before using the SDK:

#. :ref:`Before You Start <obs_21_0101>`: Select a proper SDK version.
#. :ref:`Preparations <obs_21_0102>`: Prepare the service and development environments.
#. :ref:`SDK Download and Installation <obs_21_0001>`: Download and install the OBS SDK for Java.

Creating a Bucket
-----------------

The example below shows how to create a bucket named **examplebucket**, and configure access, storage class, region, and redundancy type for the bucket. For more details about how to create a bucket, see :ref:`Creating a Bucket <obs_21_0401>`.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.AccessControlList;
   import com.obs.services.model.AvailableZoneEnum;
   import com.obs.services.model.CreateBucketRequest;
   import com.obs.services.model.ObsBucket;
   import com.obs.services.model.StorageClassEnum;

   public class CreateBucket001 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");

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
               CreateBucketRequest request = new CreateBucketRequest();
               // Example bucket name
               String exampleBucket = "examplebucket";
               // Example bucket location
               request.setBucketName(exampleBucket);
               // Set the bucket ACL to Private (the default value).
               request.setAcl(AccessControlList.REST_CANNED_PRIVATE);
               // Set the bucket storage class to Standard.
               request.setBucketStorageClass(StorageClassEnum.STANDARD);
               request.setLocation(exampleLocation);
               // Create a bucket.
               ObsBucket bucket = obsClient.createBucket(request);
               // The bucket is created.
               System.out.println("CreateBucket successfully");
               System.out.println("RequestId:"+bucket.getRequestId());


           } catch (ObsException e) {
               System.out.println("CreateBucket failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code: " + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message: " + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
           } catch (Exception e) {
               System.out.println("CreateBucket failed");
               // Print other error information.
               e.printStackTrace();

           }
       }
   }

Uploading an Object
-------------------

The example below shows how to upload two local files **localfile** and **localfile2** to the bucket **examplebucket**, and specify the names of the objects created as **objectkey** and **objectkey2** respectively. For more details about uploading an object, see :ref:`Object Upload <obs_21_0600>`.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.PutObjectRequest;
   import java.io.File;
   public class PutObject004 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
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
               // Upload files.
               // localfile indicates the path of the local file to be uploaded, in which the file name must be specified.
               PutObjectRequest request = new PutObjectRequest();
               request.setBucketName("examplebucket");
               request.setObjectKey("objectkey");
               request.setFile(new File("localfile"));
               obsClient.putObject(request);
               System.out.println("putObject successfully");
           } catch (ObsException e) {
               System.out.println("putObject failed");
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
               System.out.println("putObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Downloading an Object
---------------------

The example below shows how to download the object **objectname** from the bucket **examplebucket**. For more details about downloading an object, see :ref:`Object Download <obs_21_0700>`.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.ObsObject;
   import java.io.ByteArrayOutputStream;
   import java.io.InputStream;
   public class GetObject001 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
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
               // Download the object using streaming.
               ObsObject obsObject = obsClient.getObject("examplebucket", "objectname");
               // Read the object content.
               System.out.println("Object content:");
               InputStream input = obsObject.getObjectContent();
               byte[] b = new byte[1024];
               ByteArrayOutputStream bos = new ByteArrayOutputStream();
               int len;
               while ((len = input.read(b)) != -1) {
                   bos.write(b, 0, len);
               }
               System.out.println("getObjectContent successfully");
               System.out.println(new String(bos.toByteArray()));
               bos.close();
               input.close();
           } catch (ObsException e) {
               System.out.println("getObjectContent failed");
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
               System.out.println("getObjectContent failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Listing Objects
---------------

The example below shows how to list objects in the bucket **examplebucket**. For more details about object listing, see :ref:`Listing Objects <obs_21_0803>`.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.ObjectListing;
   import com.obs.services.model.ObsObject;
   public class ListObjects001 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
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
               // Listing objects.
               ObjectListing result = obsClient.listObjects("examplebucket");
               for (ObsObject obsObject : result.getObjects()) {
                   System.out.println("listObjects successfully");
                   System.out.println("ObjectKey:" + obsObject.getObjectKey());
                   System.out.println("Owner:" + obsObject.getOwner());
               }
           } catch (ObsException e) {
               System.out.println("listObjects failed");
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
               System.out.println("listObjects failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Deleting an Object
------------------

The example below shows how to delete the object **objectname** from the bucket **examplebucket**. For more details about deleting an object, see :ref:`Deleting an Object <obs_21_0804>`.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   public class DeleteObject001 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
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
               // Delete the object.
               obsClient.deleteObject("examplebucket", "objectname");
               System.out.println("deleteObject successfully");
           } catch (ObsException e) {
               System.out.println("deleteObject failed");
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
               System.out.println("deleteObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

.. _obs_21_0100__section8686104202916:

Using an OBS Client
-------------------

The example below shows how to use an ObsClient instance.

::

   // Make sure there is only one ObsClient instance in the whole project.
   // ObsClient is thread-safe and can be used in concurrency scenarios.
   ObsClient obsClient = null;
   try
   {
       String endPoint = "https://your-endpoint";
       // Hard-coded or plaintext access keys (AK/SK) are risky. For security purposes, encrypt your access keys and store them in the configuration file or environment variables. In this example, access keys are stored in environment variables for identity authentication. Before running the code in this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY_ID.
       // Obtain an AK/SK pair on the management console.
       String ak = System.getenv("ACCESS_KEY_ID");
       String sk = System.getenv("SECRET_ACCESS_KEY_ID");
       // Create an ObsClient instance.
       obsClient = new ObsClient(ak, sk, endPoint);
       // Call an API to perform an operation, for example, uploading an object.
   HeaderResponse response = obsClient.putObject("bucketname", "objectname", new File("localfile"));  // localfile indicates the path of the local file to be uploaded. Use the file path in your case.
       System.out.println(response);
   }
   catch (ObsException e)
   {
       System.out.println("HTTP Code: " + e.getResponseCode());
       System.out.println("Error Code:" + e.getErrorCode());
       System.out.println("Error Message: " + e.getErrorMessage());

       System.out.println("Request ID:" + e.getErrorRequestId());
       System.out.println("Host ID:" + e.getErrorHostId());
       Map<String, String> headers = e.getResponseHeaders();// Check all map entries and print all headers with errors reported.
       if(headers != null){
           for (Map.Entry<String, String> header : headers.entrySet()) {
               System.out.println(header.getKey()+":"+header.getValue());
           }
       }
       e.printStackTrace();
   }finally{
       // Close the ObsClient instance. If the instance is used globally, skip this step.
       // After the ObsClient instance is closed by calling ObsClient.close, it cannot be used again.
       if(obsClient != null){
           try
           {
               // obsClient.close();
           }
           catch (IOException e)
           {
           }
       }
   }
