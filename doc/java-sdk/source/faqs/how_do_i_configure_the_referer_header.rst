:original_name: obs_23_1715.html

.. _obs_23_1715:

How Do I Configure the **referer** Header?
==========================================

This example uploads **localfile** to **examplebucket** as **objectkey** and sets the **referer** header to **https://example.com\***.

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
           // Enter the endpoint corresponding to the region where the bucket is located.
           String endPoint = "https://your-endpoint";
           // Obtain an endpoint using environment variables or import it in other ways.
           //String endPoint = System.getenv("ENDPOINT");

           // Create an ObsClient instance.
           // Use a permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use a temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               // Upload a file.
               // localfile indicates the path of the local file to be uploaded, in which the file name must be specified.
               PutObjectRequest request = new PutObjectRequest();
               request.setBucketName("examplebucket");
               request.setObjectKey("objectkey");
               request.setFile(new File("localfile"));
               HashMap<String, String> userHeaders = new HashMap<>();
               // Specify the referer header when uploading an object.
               userHeaders.put("referer","https://example.com*");
               request.setUserHeaders(userHeaders);
               PutObjectResult putObjectResult = obsClient.putObject(request);
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
