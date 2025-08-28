:original_name: obs_21_1903.html

.. _obs_21_1903:

Code Examples for Server-Side Encryption
========================================

Code Example: Encrypting (SSE-C) and Uploading an Object
--------------------------------------------------------

The following code shows an example of encrypting an object with SSE-C before uploading it:

::

   // Hard-coded or plaintext access keys (AK/SK) are risky. For security purposes, encrypt your access keys and store them in the configuration file or environment variables. In this example, access keys are stored in the environment variables for identity authentication. Before running the code in this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY_ID.
   // Obtain an AK/SK pair on the management console.
   String ak = System.getenv("ACCESS_KEY_ID");
   String sk = System.getenv("SECRET_ACCESS_KEY_ID");
   // Create an ObsClient instance.
   ObsClient obsClient = new ObsClient(ak, sk, endPoint);

   PutObjectRequest request = new PutObjectRequest();
   request.setBucketName("bucketname");
   request.setObjectKey("objectname");
   request.setFile(new File("localfile"));

   HashMap<String, String> userHeaders = new HashMap<>();
   userHeaders.put("x-obs-server-side-encryption-customer-algorithm","AES256");
   //The key for encrypting objects when SSE-C is used. Its value is a Base64-encoded 256-bit key.
   userHeaders.put("x-obs-server-side-encryption-customer-key","your-encryption-customer-key");
   userHeaders.put("x-obs-server-side-encryption-customer-key-MD5",
                       ServiceUtils.toBase64(ServiceUtils.computeMD5Hash(ServiceUtils.fromBase64("your-encryption-customer-key"))));            request.setUserHeaders(userHeaders);
   HeaderResponse response = obsClient.putObject(request);
   System.out.println("response:"+response.getRequestId());

Code Example: Decrypting and Downloading an Object
--------------------------------------------------

The following code shows an example of downloading an object encrypted with SSE-C:

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.internal.utils.ServiceUtils;
   import com.obs.services.model.GetObjectRequest;
   import com.obs.services.model.ObsObject;
   import java.util.HashMap;
   import java.util.Map;

   public class SseCGetObject{
       public static void main(String[] args) {
           // Hard-coded or plaintext AK and SK are risky. For security purposes, encrypt your AK and SK and store them in the configuration file or environment variables. In this example, the AK and SK are stored in environment variables for identity authentication.
           //Before running the code in this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY_ID.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
           // Create an ObsClient instance and use the permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use the temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               // Call APIs to perform operations, for example, downloading an encrypted object.
               GetObjectRequest request=new GetObjectRequest("bucketname","objectname");
               // Set the SSE-C decryption algorithm.
               HashMap<String, String> userHeaders=new HashMap<>();
               userHeaders.put("x-obs-server-side-encryption-customer-algorithm","AES256");
               The header indicates the key used to encrypt objects in SSE-C mode. The header value is a Base64-encoded 256-bit key.
               userHeaders.put("x-obs-server-side-encryption-customer-key","your-encryption-customer-key");
               userHeaders.put("x-obs-server-side-encryption-customer-key-MD5",
                       ServiceUtils.toBase64(ServiceUtils.computeMD5Hash(ServiceUtils.fromBase64("your-encryption-customer-key"))));
               request.setUserHeaders(userHeaders);
               ObsObject obsObject=obsClient.getObject(request);
               // You can use other methods to read streams.
               System.out.println(obsObject.getObjectContent());
           }
           catch(ObsException e) {
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
               Map<String, String> headers=e.getResponseHeaders();
               if(headers!=null){
                   Check all map entries and print all headers with errors reported.
                   for(Map.Entry<String, String> header:headers.entrySet()){
                       if(header.getKey().contains("error")){
                           System.out.println(header.getKey()+":"+header.getValue());
                       }
                   }
               }
               e.printStackTrace();
           } catch (Exception e) {
               System.out.println("putObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

.. note::

   -  For details about the encryption key calculation, see :ref:`How Do I Generate an SSE-C Encryption Key? <obs_21_2119>`
