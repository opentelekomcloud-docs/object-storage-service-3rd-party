:original_name: obs_21_1403.html

.. _obs_21_1403:

Obtaining a CORS Rule
=====================

Function
--------

CORS is a browser-standard mechanism defined by the W3C. It allows a web client in one origin to interact with resources in another. For general web page requests, website scripts and contents in one origin cannot interact with those in another due to SOPs. OBS supports CORS, allowing the resources in OBS to be requested across origins.

This API returns the CORS configuration of a bucket.

Restrictions
------------

-  To obtain the CORS configuration of a bucket, you must be the bucket owner or have the required permission (**obs:bucket:GetBucketCORS** in IAM or **GetBucketCORS** in a bucket policy).

Method
------

obsclient.getBucketCors(final :ref:`BaseBucketRequest <obs_21_1403__table43960571>` :ref:`request <obs_21_1403__table72121329103020>`)

Request Parameters
------------------

.. _obs_21_1403__table72121329103020:

.. table:: **Table 1** List of request parameters

   +-----------------+-------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                  | Mandatory (Yes/No) | Description                                                                                                 |
   +=================+=======================================================+====================+=============================================================================================================+
   | request         | :ref:`BaseBucketRequest <obs_21_1403__table43960571>` | Yes                | **Explanation:**                                                                                            |
   |                 |                                                       |                    |                                                                                                             |
   |                 |                                                       |                    | Request parameters for obtaining a CORS rule. For details, see :ref:`Table 2 <obs_21_1403__table43960571>`. |
   +-----------------+-------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------+

.. _obs_21_1403__table43960571:

.. table:: **Table 2** BaseBucketRequest

   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=================+====================+===================================================================================================================================================================================+
   | bucketName      | String          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Bucket name.                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                 |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** BucketCors

   +-----------------+----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                           | Mandatory (Yes/No) | Description                                                                                         |
   +=================+================================================================+====================+=====================================================================================================+
   | rules           | List<:ref:`BucketCorsRule <obs_21_1403__table17941121314177>`> | Yes                | **Explanation:**                                                                                    |
   |                 |                                                                |                    |                                                                                                     |
   |                 |                                                                |                    | List of CORS rules of a bucket. For details, see :ref:`Table 4 <obs_21_1403__table17941121314177>`. |
   +-----------------+----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+

.. _obs_21_1403__table17941121314177:

.. table:: **Table 4** BucketCorsRule

   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                                                                                    |
   +=================+=================+====================+================================================================================================================================================================================================================================================================================================================+
   | id              | String          | No                 | **Explanation:**                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | CORS rule ID.                                                                                                                                                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | The value must contain 1 to 255 characters.                                                                                                                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                                                             |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                                                           |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | allowedMethod   | List<String>    | Yes                | **Explanation:**                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | The allowed HTTP methods for a cross-origin request, indicating the operation types for buckets and objects.                                                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | The following HTTP methods are supported:                                                                                                                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | -  GET                                                                                                                                                                                                                                                                                                         |
   |                 |                 |                    | -  PUT                                                                                                                                                                                                                                                                                                         |
   |                 |                 |                    | -  HEAD                                                                                                                                                                                                                                                                                                        |
   |                 |                 |                    | -  POST                                                                                                                                                                                                                                                                                                        |
   |                 |                 |                    | -  DELETE                                                                                                                                                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                                                             |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                                                           |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | allowedOrigin   | List<String>    | Yes                | **Explanation:**                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | The origin from which the requests can access the bucket.                                                                                                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | Domain name of the origin. Each origin can contain only one wildcard character (``*``), for example, **https://*.vbs.example.com**.                                                                                                                                                                            |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                                                             |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                                                           |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | allowedHeader   | List<String>    | No                 | **Explanation:**                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | The allowed cross-origin request headers. Only CORS requests matching the allowed headers are valid.                                                                                                                                                                                                           |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | Each header can contain only one wildcard character (``*``). Spaces, ampersands (&), colons (:), and less-than signs (<) are not allowed.                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                                                             |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                                                           |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maxAgeSeconds   | int             | No                 | **Explanation:**                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | Duration your client can cache the response for a cross-origin request.                                                                                                                                                                                                                                        |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | Each bucket CORS rule can contain only one **maxAgeSeconds**.                                                                                                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | An integer greater than or equal to 0, in seconds.                                                                                                                                                                                                                                                             |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                                                             |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | 100                                                                                                                                                                                                                                                                                                            |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | exposeHeader    | List<String>    | No                 | **Explanation:**                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | The CORS-allowed additional headers in the response. These headers provide additional information to clients. By default, your browser can only access headers **Content-Length** and **Content-Type**. If your browser needs to access other headers, add them to the list of the allowed additional headers. |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | Spaces, wildcard characters (``*``), ampersands (&), colons (:), and less-than signs (<) are not allowed.                                                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                                                             |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                                                           |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example returns the CORS configuration of bucket **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.BucketCors;
   import com.obs.services.model.BucketCorsRule;
   public class GetBucketCors001 {
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
               // Obtain the CORS rules.
               BucketCors cors = obsClient.getBucketCors("examplebucket");
               for(BucketCorsRule rule : cors.getRules()){
                   System.out.println("Id:" + rule.getId());
                   System.out.println("MaxAgeSecond:" + rule.getMaxAgeSecond());
                   System.out.println("AllowedHeader:" + rule.getAllowedHeader());
                   System.out.println("AllowedOrigin:" + rule.getAllowedOrigin());
                   System.out.println("AllowedMethod:" + rule.getAllowedMethod());
                   System.out.println("ExposeHeader:" + rule.getExposeHeader());
               }
               System.out.println("getBucketCors successfully");
           } catch (ObsException e) {
               System.out.println("getBucketCors failed");
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
               System.out.println("getBucketCors failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
