:original_name: obs_21_0901.html

.. _obs_21_0901:

Accessing OBS Using a Signed URL
================================

Function
--------

ObsClient allows you to create a URL with **Query** parameters that carry authentication information by specifying the AK and SK, HTTP method, and request parameters. You can provide this URL to other users for them to make a temporary access. When generating a URL, you need to specify the validity period of the URL to restrict the access duration of visitors.

If you want to grant other users the permission to perform operations on buckets or objects (for example, upload or download objects), you need to generate a URL for the corresponding request (for example, a URL with the PUT request for uploading an object) and provide the URL to other users.

If a CORS or signature mismatch error occurs, refer to the following steps to troubleshoot the issue:

#. If CORS is not configured, you need to configure CORS rules on OBS Console.
#. If the signatures do not match, check whether signature parameters are correct. For example, during an object upload, the backend uses **Content-Type** to calculate the signature and generate an authorized URL, but if **Content-Type** is not set or is set to an incorrect value when the frontend uses the authorized URL, a CORS error occurs. To avoid this issue, ensure that **Content-Type** fields are the same at the frontend and backend.
#. A CDN acceleration domain name cannot be used to create a signed URL.

The following table lists operations that can be performed through a signed URL.

.. _obs_21_0901__table1281912486367:

.. table:: **Table 1** HttpMethodEnum & SpecialParamEnum

   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Operation                 | HTTP Request Method (Value in OBS SDK for Java) | Special Operator (Value in OBS SDK for Java) | Bucket Name Required (Yes/No) | Object Name Required (Yes/No) |
   +===========================+=================================================+==============================================+===============================+===============================+
   | Create Bucket             | HttpMethodEnum.PUT                              | N/A                                          | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | List Buckets              | HttpMethodEnum.GET                              | N/A                                          | No                            | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Delete Bucket             | HttpMethodEnum.DELETE                           | N/A                                          | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | List Objects              | HttpMethodEnum.GET                              | N/A                                          | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | List Object Versions      | HttpMethodEnum.GET                              | SpecialParamEnum.VERSIONS                    | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | List Multipart Uploads    | HttpMethodEnum.GET                              | SpecialParamEnum.UPLOADS                     | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Bucket Metadata       | HttpMethodEnum.HEAD                             | N/A                                          | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Bucket Location       | HttpMethodEnum.GET                              | SpecialParamEnum.LOCATION                    | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Bucket Storageinfo    | HttpMethodEnum.GET                              | SpecialParamEnum.STORAGEINFO                 | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Set Bucket Quota          | HttpMethodEnum.PUT                              | SpecialParamEnum.QUOTA                       | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Bucket Quota          | HttpMethodEnum.GET                              | SpecialParamEnum.QUOTA                       | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Set Bucket Storage Policy | HttpMethodEnum.PUT                              | SpecialParamEnum.STORAGEPOLICY               | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Bucket Storage Policy | HttpMethodEnum.GET                              | SpecialParamEnum.STORAGEPOLICY               | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Configure Bucket ACL      | HttpMethodEnum.PUT                              | SpecialParamEnum.ACL                         | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Obtain Bucket ACL         | HttpMethodEnum.GET                              | SpecialParamEnum.ACL                         | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Set Bucket Logging        | HttpMethodEnum.PUT                              | SpecialParamEnum.LOGGING                     | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Bucket Logging        | HttpMethodEnum.GET                              | SpecialParamEnum.LOGGING                     | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Set Bucket Policy         | HttpMethodEnum.PUT                              | SpecialParamEnum.POLICY                      | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Bucket Policy         | HttpMethodEnum.GET                              | SpecialParamEnum.POLICY                      | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Delete Bucket Policy      | HttpMethodEnum.DELETE                           | SpecialParamEnum.POLICY                      | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Set Lifecycle Rule        | HttpMethodEnum.PUT                              | SpecialParamEnum.LIFECYCLE                   | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Lifecycle Rule        | HttpMethodEnum.GET                              | SpecialParamEnum.LIFECYCLE                   | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Delete Lifecycle Rule     | HttpMethodEnum.DELETE                           | SpecialParamEnum.LIFECYCLE                   | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Set Website Hosting       | HttpMethodEnum.PUT                              | SpecialParamEnum.WEBSITE                     | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Website Hosting       | HttpMethodEnum.GET                              | SpecialParamEnum.WEBSITE                     | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Delete Website Hosting    | HttpMethodEnum.DELETE                           | SpecialParamEnum.WEBSITE                     | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Set Bucket Versioning     | HttpMethodEnum.PUT                              | SpecialParamEnum.VERSIONING                  | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Bucket Versioning     | HttpMethodEnum.GET                              | SpecialParamEnum.VERSIONING                  | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Set CORS Rule             | HttpMethodEnum.PUT                              | SpecialParamEnum.CORS                        | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get CORS Rule             | HttpMethodEnum.GET                              | SpecialParamEnum.CORS                        | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Delete CORS Rule          | HttpMethodEnum.DELETE                           | SpecialParamEnum.CORS                        | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Set Bucket Tagging        | HttpMethodEnum.PUT                              | SpecialParamEnum.TAGGING                     | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Bucket Tagging        | HttpMethodEnum.GET                              | SpecialParamEnum.TAGGING                     | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Delete Bucket Tagging     | HttpMethodEnum.DELETE                           | SpecialParamEnum.TAGGING                     | Yes                           | No                            |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Upload Object             | HttpMethodEnum.PUT                              | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Append Object             | HttpMethodEnum.POST                             | SpecialParamEnum.APPEND                      | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Object                | HttpMethodEnum.GET                              | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Copy Object               | HttpMethodEnum.PUT                              | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Delete Object             | HttpMethodEnum.DELETE                           | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Delete Objects            | HttpMethodEnum.POST                             | SpecialParamEnum.DELETE                      | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Get Object Metadata       | HttpMethodEnum.HEAD                             | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Configure Object ACL      | HttpMethodEnum.PUT                              | SpecialParamEnum.ACL                         | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Obtain Object ACL         | HttpMethodEnum.GET                              | SpecialParamEnum.ACL                         | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Initiate Multipart Upload | HttpMethodEnum.POST                             | SpecialParamEnum.UPLOADS                     | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Upload Part               | HttpMethodEnum.PUT                              | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Copy Part                 | HttpMethodEnum.PUT                              | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | List Parts                | HttpMethodEnum.GET                              | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Assemble Parts            | HttpMethodEnum.POST                             | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Delete Multipart Upload   | HttpMethodEnum.DELETE                           | N/A                                          | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+
   | Restore Cold Objects      | HttpMethodEnum.POST                             | SpecialParamEnum.RESTORE                     | Yes                           | Yes                           |
   +---------------------------+-------------------------------------------------+----------------------------------------------+-------------------------------+-------------------------------+

To access OBS using a signed URL generated by the OBS SDK for Java, perform the following steps:

#. Use **ObsClient.createTemporarySignature** to create a signed URL. Note that the **ObsClient.createTemporarySignature** function has encoded the generated URL. The browser will automatically decode the URL. You do not need to encode it again.
#. Use an HTTP library to make an HTTP/HTTPS request to OBS.

Method
------

obsClient.createTemporarySignature(:ref:`TemporarySignatureRequest <obs_21_0901__table91617616238>` :ref:`request <obs_21_0901__table14591111716211>`)

Request Parameters
------------------

.. _obs_21_0901__table14591111716211:

.. table:: **Table 2** List of request parameters

   +-----------------+------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                             | Mandatory (Yes/No) | Description                                                                                                    |
   +=================+==================================================================+====================+================================================================================================================+
   | request         | :ref:`TemporarySignatureRequest <obs_21_0901__table91617616238>` | Yes                | **Explanation:**                                                                                               |
   |                 |                                                                  |                    |                                                                                                                |
   |                 |                                                                  |                    | Request parameters for creating a signed URL. For details, see :ref:`Table 3 <obs_21_0901__table91617616238>`. |
   +-----------------+------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------+

.. _obs_21_0901__table91617616238:

.. table:: **Table 3** TemporarySignatureRequest

   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                      | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+===========================================================+====================+===================================================================================================================================================================================+
   | bucketName      | String                                                    | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | Bucket name.                                                                                                                                                                      |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                           |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                           |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                           |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                           |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                           |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey       | String                                                    | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                             |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | specialParam    | :ref:`SpecialParamEnum <obs_21_0901__table1281912486367>` | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | Special parameters that may be used in the request, indicating the sub-operations.                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | See :ref:`Table 1 <obs_21_0901__table1281912486367>`.                                                                                                                             |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | method          | :ref:`HttpMethodEnum <obs_21_0901__table1281912486367>`   | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | HTTP method type.                                                                                                                                                                 |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | See :ref:`Table 1 <obs_21_0901__table1281912486367>`.                                                                                                                             |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | headers         | Map<String, String>                                       | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | Headers in the request. In **Map**, the **String** key and value indicate the name and value of the request header respectively.                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | queryParams     | Map<String, Object>                                       | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | Query parameters in the request. In **Map**, the **String** key indicates the name of the query parameter, and the **Object** value indicates the value of the query parameter.   |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | expires         | long                                                      | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | Expiration time of the signed URL.                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | -  If you use a temporary key to call the SDK API, the value of **expires** ranges from 0 to 86400 seconds.                                                                       |
   |                 |                                                           |                    | -  If you use a permanent key to call the SDK API, the value of **expires** ranges from 0 to 630720000 seconds.                                                                   |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | 300                                                                                                                                                                               |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | requestDate     | Date                                                      | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | Time when the request is initiated.                                                                                                                                               |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                   |
   |                 |                                                           |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 4** TemporarySignatureResponse

   +----------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                  | Type                  | Description                                                                                                                                                            |
   +============================+=======================+========================================================================================================================================================================+
   | signedUrl                  | String                | **Explanation:**                                                                                                                                                       |
   |                            |                       |                                                                                                                                                                        |
   |                            |                       | The signed URL that carries the authentication information.                                                                                                            |
   |                            |                       |                                                                                                                                                                        |
   |                            |                       | **Default value**:                                                                                                                                                     |
   |                            |                       |                                                                                                                                                                        |
   |                            |                       | None                                                                                                                                                                   |
   +----------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | actualSignedRequestHeaders | Map<String, String>   | **Explanation:**                                                                                                                                                       |
   |                            |                       |                                                                                                                                                                        |
   |                            |                       | Actual headers in the request initiated using the signed URL. In **Map**, the **String** key and value indicate the name and value of the request header respectively. |
   |                            |                       |                                                                                                                                                                        |
   |                            |                       | **Default value**:                                                                                                                                                     |
   |                            |                       |                                                                                                                                                                        |
   |                            |                       | None                                                                                                                                                                   |
   +----------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Example: Creating a Bucket
-------------------------------

This example uses **HttpMethodEnum.PUT** to create bucket **examplebucket** based on a signed URL. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.RequestBody;
   import okhttp3.Response;
   import java.util.Map;
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
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
               request.setBucketName("examplebucket");
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("Creating bucket using temporary signature url:");
               System.out.println("\t" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // Make a PUT request to create a bucket.
               String location = "your bucket location";
               Request httpRequest =
                       builder.url(response.getSignedUrl())
                               .put(
                                       RequestBody.create(
                                               null,
                                               ("<CreateBucketConfiguration><Location>"
                                                       + location
                                                       + "</Location></CreateBucketConfiguration>").getBytes()))
                               .build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("\tStatus:" + res.code());
               if (res.body() != null) {
                   System.out.println("\tContent:" + res.body().string() + "\n");
               }
               res.close();
               System.out.println("CreateBucket successfully");
           } catch (ObsException e) {
               System.out.println("CreateBucket failed");
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
               System.out.println("CreateBucket failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Uploading an Object
---------------------------------

This example uses **HttpMethodEnum.PUT** to upload object **objectname** to bucket **examplebucket** based on a signed URL. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.MediaType;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.RequestBody;
   import okhttp3.Response;
   import java.util.HashMap;
   import java.util.Map;
   public class PutObject001 {
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
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               Map<String, String> headers = new HashMap<>();
               String contentType = "text/plain";
               headers.put("Content-Type", contentType);
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               request.setHeaders(headers);
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("Creating object using temporary signature url:");
               System.out.println("\t" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // Make a PUT request to upload an object.
               Request httpRequest =
                       builder.url(response.getSignedUrl())
                               .put(RequestBody.create(MediaType.parse(contentType), "Hello OBS".getBytes("UTF-8")))
                               .build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("Status:" + res.code());
               if (res.body() != null) {
                   System.out.println("Content:" + res.body().string() + "\n");
               }
               res.close();
               System.out.println("PutObject successfully");
           } catch (ObsException e) {
               System.out.println("PutObject failed");
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
               System.out.println("PutObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Downloading an Object
-----------------------------------

This example uses **HttpMethodEnum.GET** to download object **objectname** from bucket **examplebucket** based on a signed URL. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.Response;
   import java.io.InputStream;
   import java.util.Map;
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
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("Getting object using temporary signature url:");
               System.out.println("SignedUrl:" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // Make a GET request to download an object.
               Request httpRequest = builder.url(response.getSignedUrl()).get().build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("Status:" + res.code());
               InputStream objectContent = null;
               if (res.body() != null) {
                   objectContent = res.body().byteStream();
                   System.out.println("Content:" + res.body().string() + "\n");
               }
               if(objectContent != null) {
                   // objectContent is the file stream to download.
                   // You can read the objectContent stream to download the file. If the stream is not read for a long time, it will be disconnected from the server.
               }
               res.close();
               System.out.println("getObject successfully");
           } catch (ObsException e) {
               System.out.println("getObject failed");
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
               System.out.println("getObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Listing Objects
-----------------------------

This example uses **HttpMethodEnum.GET** to list object in bucket **examplebucket** based on a signed URL. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.Response;
   import java.util.Map;
   public class ListObject001 {
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
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
               request.setBucketName("examplebucket");
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("Getting object list using temporary signature url:");
               System.out.println("\t" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // Make a GET request to obtain the object list.
               Request httpRequest = builder.url(response.getSignedUrl()).get().build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("Status:" + res.code());
               if (res.body() != null) {
                   System.out.println("Content:" + res.body().string() + "\n");
               }
               res.close();
               System.out.println("ListObject successfully");
           } catch (ObsException e) {
               System.out.println("ListObject failed");
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
               System.out.println("ListObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Deleting an Object
--------------------------------

This example uses **HttpMethodEnum.DELETE** to delete object **objectname** from bucket **examplebucket** based on a signed URL. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.Response;
   import java.util.Map;
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
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.DELETE, expireSeconds);
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("Deleting object using temporary signature url:");
               System.out.println("\t" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // Make a DELETE request to delete an object.
               Request httpRequest = builder.url(response.getSignedUrl()).delete().build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("\tStatus:" + res.code());
               if (res.body() != null) {
                   System.out.println("\tContent:" + res.body().string() + "\n");
               }
               res.close();
               System.out.println("deleteObjects successfully");
           } catch (ObsException e) {
               System.out.println("deleteObjects failed");
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
               System.out.println("deleteObjects failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Initiating a Multipart Upload
-------------------------------------------

This example uses **HttpMethodEnum.POST** to initiate a multipart upload based on a signed URL. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.SpecialParamEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.RequestBody;
   import okhttp3.Response;
   import java.util.Map;
   public class InitiateMultiPartUpload001 {
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
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.POST, expireSeconds);
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               request.setSpecialParam(SpecialParamEnum.UPLOADS);
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("initiate multipart upload using temporary signature url:");
               System.out.println("\t" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // Make a POST request to initiate the multipart upload.
               Request httpRequest = builder.url(response.getSignedUrl()).post(RequestBody.create(null, "")).build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("Status:" + res.code());
               if (res.body() != null) {
                   System.out.println("Content:" + res.body().string() + "\n");
               }
               res.close();
               System.out.println("InitiateMultiPartUpload successfully");
           } catch (ObsException e) {
               System.out.println("InitiateMultiPartUpload failed");
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
               System.out.println("InitiateMultiPartUpload failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Uploading a Part
------------------------------

This example uses **HttpMethodEnum.PUT** to upload a part based on a signed URL. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.RequestBody;
   import okhttp3.Response;
   import java.util.HashMap;
   import java.util.Map;
   public class UploadPart001 {
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
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               Map<String, Object> queryParams = new HashMap<String, Object>();
               // Set the partNumber parameter, for example, queryParams.put("partNumber", "1").
               queryParams.put("partNumber", "partNumber");
               queryParams.put("uploadId", "your uploadId");
               request.setQueryParams(queryParams);
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("upload part using temporary signature url:");
               System.out.println("SignedUrl:" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // Make a PUT request to upload a part.
               Request httpRequest =
                       builder.url(response.getSignedUrl())
                               .put(RequestBody.create(null, new byte[6 * 1024 * 1024]))
                               .build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("Status:" + res.code());
               if (res.body() != null) {
                   System.out.println("Content:" + res.body().string() + "\n");
               }
               res.close();
               System.out.println("UploadPart successfully");
           } catch (ObsException e) {
               System.out.println("UploadPart failed");
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
               System.out.println("UploadPart failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Listing Uploaded Parts
------------------------------------

This example uses **HttpMethodEnum.PUT** to list uploaded parts based on a signed URL. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.Response;
   import java.util.HashMap;
   import java.util.Map;
   public class ListUploadedParts001 {
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
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               Map<String, Object> queryParams = new HashMap<String, Object>();
               queryParams.put("uploadId", "your uploadId");
               request.setQueryParams(queryParams);
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("list parts using temporary signature url:");
               System.out.println("\t" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // Make a GET request to list uploaded parts.
               Request httpRequest = builder.url(response.getSignedUrl()).get().build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("Status:" + res.code());
               if (res.body() != null) {
                   System.out.println("Content:" + res.body().string() + "\n");
               }
               res.close();
               System.out.println("ListParts successfully");
           } catch (ObsException e) {
               System.out.println("ListParts failed");
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
               System.out.println("ListParts failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Assembling Parts
------------------------------

This example uses **HttpMethodEnum.POST** to assemble parts based on a signed URL. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.MediaType;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.RequestBody;
   import okhttp3.Response;
   import java.util.HashMap;
   import java.util.Map;
   public class CompleteMultiPartUpload001 {
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
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.POST, expireSeconds);
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               Map<String, String> headers = new HashMap<>();
               String contentType = "application/xml";
               headers.put("Content-Type", contentType);
               request.setHeaders(headers);
               Map<String, Object> queryParams = new HashMap<>();
               queryParams.put("uploadId", "your uploadId");
               request.setQueryParams(queryParams);
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("complete multipart upload using temporary signature url:");
               System.out.println("\t" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // The following content is used as an example. You need to replace it with the responses of the request for listing uploaded parts.
               String content = "<CompleteMultipartUpload>";
               content += "<Part>";
               content += "<PartNumber>1</PartNumber>";
               content += "<ETag>da6a0d097e307ac52ed9b4ad551801fc</ETag>";
               content += "</Part>";
               content += "<Part>";
               content += "<PartNumber>2</PartNumber>";
               content += "<ETag>da6a0d097e307ac52ed9b4ad551801fc</ETag>";
               content += "</Part>";
               content += "</CompleteMultipartUpload>";
               // Make a POST request to assemble the uploaded parts.
               Request httpRequest =
                       builder.url(response.getSignedUrl())
                               .post(RequestBody.create(MediaType.parse(contentType), content.getBytes("UTF-8")))
                               .build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("\tStatus:" + res.code());
               if (res.body() != null) {
                   System.out.println("\tContent:" + res.body().string() + "\n");
               }
               res.close();
           } catch (ObsException e) {
               System.out.println("CompleteMultiPartUpload failed");
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
               System.out.println("CompleteMultiPartUpload failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

.. _obs_21_0901__section195111828105617:

Code Example: Downloading an Object Encrypted Using SSE-C
---------------------------------------------------------

This example uses **HttpMethodEnum.GET** to download an object encrypted using SSE-C. The validity period of the URL is 3,600 seconds.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HttpMethodEnum;
   import com.obs.services.model.TemporarySignatureRequest;
   import com.obs.services.model.TemporarySignatureResponse;
   import okhttp3.Call;
   import okhttp3.OkHttpClient;
   import okhttp3.Request;
   import okhttp3.Response;
   import java.util.HashMap;
   import java.util.Map;
   public class GetObject003 {
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
               // Download an object encrypted using SSE-C.
               // Set the validity period of the URL to 3600 seconds.
               long expireSeconds = 3600L;
               TemporarySignatureRequest request = new TemporarySignatureRequest(HttpMethodEnum.GET, expireSeconds);
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               // Set the encryption method to SSE-C.
               Map<String, String> headers = new HashMap<>();
               headers.put("x-obs-server-side-encryption-customer-algorithm", "AES256");
               // Set the key used for encryption, which is a Base64-encoded 256-bit value.
               headers.put(
                       "x-obs-server-side-encryption-customer-key",
                       "your base64 sse-c key generated by AES-256 algorithm");
               // Set the MD5 value of the key used for encryption, which is a Base64-encoded, 128-bit MD5 value.
               headers.put("x-obs-server-side-encryption-customer-key-MD5", "the md5 value of your sse-c key");
               request.setHeaders(headers);
               TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
               System.out.println("Getting object using temporary signature url:");
               System.out.println("\t" + response.getSignedUrl());
               Request.Builder builder = new Request.Builder();
               for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
                   builder.header(entry.getKey(), entry.getValue());
               }
               // Make a GET request to download an object.
               Request httpRequest = builder.url(response.getSignedUrl()).get().build();
               OkHttpClient httpClient =
                       new OkHttpClient.Builder()
                               .followRedirects(false)
                               .retryOnConnectionFailure(false)
                               .cache(null)
                               .build();
               Call c = httpClient.newCall(httpRequest);
               Response res = c.execute();
               System.out.println("Status:" + res.code());
               if (res.body() != null) {
                   System.out.println("Content:" + res.body().string() + "\n");
               }
               res.close();
               System.out.println("getObject successfully");
           } catch (ObsException e) {
               System.out.println("getObject failed");
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
               System.out.println("getObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

.. note::

   -  **HttpMethodEnum** is an enumeration function defined in OBS SDK for Java, whose value indicates the request method types.

   -  For details about the encryption key calculation, see :ref:`How Do I Generate an SSE-C Encryption Key? <obs_21_2119>`

Integrity Check When Uploading an Object
----------------------------------------

This example uses content-md5 for integrity check when using a temporary URL to upload an object to OBS.

::

   import com.obs.services.ObsClient;
   import com.obs.services.internal.utils.ServiceUtils;
   import com.obs.services.model.*;
   import okhttp3.*;
   import java.io.ByteArrayOutputStream;
   import java.io.File;
   import java.io.FileInputStream;
   import java.io.IOException;
   import java.security.NoSuchAlgorithmException;
   import java.util.HashMap;
   import java.util.Map;
   public class Create_TemporarySignature_Uploadobject {
      public static void main(String[] args) throws IOException, NoSuchAlgorithmException {
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
           // Create an instance of ObsClient.
           // Use a permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use a temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);
           // Set the validity period of the URL to 3600 seconds.
           long expireSeconds = 3600L;
           Map<String, String> headers = new HashMap<String, String>();
           String localFile_path = "localFile_path";
           //Convert the local file into a stream and calculate its MD5 value.
           try (FileInputStream fileInputStream = new FileInputStream(localFile_path)) {
               String md5 = ServiceUtils.toBase64(ServiceUtils.computeMD5Hash(fileInputStream));
               headers.put("content-md5",md5);
           }
           TemporarySignatureRequest request = new  TemporarySignatureRequest(HttpMethodEnum.PUT, expireSeconds);
           request.setBucketName("your_bucketname");
           request.setObjectKey("objectkey");
           request.setHeaders(headers);
           TemporarySignatureResponse response = obsClient.createTemporarySignature(request);
           System.out.println("Creating object using temporary signature url:");
           System.out.println("\t" + response.getSignedUrl());
           Request.Builder builder = new Request.Builder();
           for (Map.Entry<String, String> entry : response.getActualSignedRequestHeaders().entrySet()) {
               builder.header(entry.getKey(), entry.getValue());
           }
           // Make a PUT request to upload the file.
           Request httpRequest = builder.url(response.getSignedUrl())
                   .put(RequestBody.create(getBytesByFile(localFile_path))).build();
           OkHttpClient httpClient = new OkHttpClient.Builder().followRedirects(false).retryOnConnectionFailure(false)
                   .cache(null).build();
           Call c = httpClient.newCall(httpRequest);
           Response res = c.execute();
           System.out.println("\tStatus:" + res.code());
           if (res.body() != null) {
               System.out.println("\tContent:" + res.body().string() + "\n");
           }
           res.close();
       }
       public static byte[] getBytesByFile(String pathStr) {
           File file = new File(pathStr);
           try (FileInputStream fis = new FileInputStream(file);
                ByteArrayOutputStream bos = new ByteArrayOutputStream(1000)) {
               byte[] b = new byte[1000];
               int n;
               while ((n = fis.read(b)) != -1) {
                   bos.write(b, 0, n);
               }
               return bos.toByteArray();
           } catch (Exception e) {
               e.printStackTrace();
           }
           return null;
       }
   }
