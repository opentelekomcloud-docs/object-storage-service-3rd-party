:original_name: obs_21_1402.html

.. _obs_21_1402:

Configuring a CORS Rule
=======================

Function
--------

Cross-origin resource sharing (CORS) is a mechanism defined by the World Wide Web Consortium (W3C) that allows a web application program in one domain to access resources located in another one. For general web page requests, website scripts and contents in one domain cannot interact with those in another because of Same Origin Policies (SOPs). OBS supports CORS rules that allow the resources in OBS to be requested by other domains.

You can call **ObsClient.setBucketCors** to set CORS rules for a bucket. The configured CORS rules follow the principle of new ones overwriting old ones.

Restrictions
------------

-  To configure CORS for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketCORS** in IAM or **PutBucketCORS** in a bucket policy).

Method
------

obsclient.setBucketCors(final :ref:`SetBucketCorsRequest <obs_21_1402__table14455523>` :ref:`request <obs_21_1402__table1210700>`)

Request Parameters
------------------

.. _obs_21_1402__table1210700:

.. table:: **Table 1** List of request parameters

   +-----------+----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter | Type                                                     | Mandatory (Yes/No) | Description                                                                                               |
   +===========+==========================================================+====================+===========================================================================================================+
   | request   | :ref:`SetBucketCorsRequest <obs_21_1402__table14455523>` | Yes                | Request parameters for setting a CORS rule. For details, see :ref:`Table 2 <obs_21_1402__table14455523>`. |
   +-----------+----------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------+

.. _obs_21_1402__table14455523:

.. table:: **Table 2** SetBucketCorsRequest

   +-----------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                 | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+======================================================+====================+===================================================================================================================================================================================+
   | bucketName      | String                                               | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                      |                    |                                                                                                                                                                                   |
   |                 |                                                      |                    | Bucket name.                                                                                                                                                                      |
   |                 |                                                      |                    |                                                                                                                                                                                   |
   |                 |                                                      |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                      |                    |                                                                                                                                                                                   |
   |                 |                                                      |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                      |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                      |                    |                                                                                                                                                                                   |
   |                 |                                                      |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                      |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                      |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                      |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                      |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                                                      |                    |                                                                                                                                                                                   |
   |                 |                                                      |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                      |                    |                                                                                                                                                                                   |
   |                 |                                                      |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                      |                    |                                                                                                                                                                                   |
   |                 |                                                      |                    | None                                                                                                                                                                              |
   +-----------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bucketCors      | :ref:`BucketCors <obs_21_1402__table15614918174818>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                      |                    |                                                                                                                                                                                   |
   |                 |                                                      |                    | List of CORS rules of a bucket. For details, see :ref:`Table 3 <obs_21_1402__table15614918174818>`.                                                                               |
   +-----------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1402__table15614918174818:

.. table:: **Table 3** BucketCors

   +-----------------+----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                           | Mandatory (Yes/No) | Description                                                                                         |
   +=================+================================================================+====================+=====================================================================================================+
   | rules           | List<:ref:`BucketCorsRule <obs_21_1402__table17941121314177>`> | Yes                | **Explanation:**                                                                                    |
   |                 |                                                                |                    |                                                                                                     |
   |                 |                                                                |                    | List of CORS rules of a bucket. For details, see :ref:`Table 4 <obs_21_1402__table17941121314177>`. |
   +-----------------+----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+

.. _obs_21_1402__table17941121314177:

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

Responses
---------

.. table:: **Table 5** Common response headers

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================+
   | statusCode            | int                   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP status code.                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | responseHeaders       | Map<String, Object>   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example configures CORS rules for bucket **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.BucketCors;
   import com.obs.services.model.BucketCorsRule;
   import com.obs.services.model.DeleteObjectsRequest;
   import com.obs.services.model.DeleteObjectsResult;
   import com.obs.services.model.KeyAndVersion;
   import java.util.ArrayList;
   import java.util.List;
   public class SetBucketCors001 {
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
               //Configure CORS rules.
               BucketCors cors = new BucketCors();
               List<BucketCorsRule> rules = new ArrayList<BucketCorsRule>();
               BucketCorsRule rule = new BucketCorsRule();
               ArrayList<String> allowedOrigin = new ArrayList<String>();
               // Specify the origin of the cross-origin request.
               allowedOrigin.add( "http://www.a.com");
               allowedOrigin.add( "http://www.b.com");
               rule.setAllowedOrigin(allowedOrigin);
               ArrayList<String> allowedMethod = new ArrayList<String>();
               // Specify the request method, which can be GET, PUT, DELETE, POST, or HEAD.
               allowedMethod.add("GET");
               allowedMethod.add("HEAD");
               allowedMethod.add("PUT");
               rule.setAllowedMethod(allowedMethod);
               ArrayList<String> allowedHeader = new ArrayList<String>();
               // Specify whether headers specified in Access-Control-Request-Headers in the OPTIONS request can be used.
               allowedHeader.add("x-obs-header");
               rule.setAllowedHeader(allowedHeader);
               ArrayList<String> exposeHeader = new ArrayList<String>();
               // Specify response headers that users can access using application programs.
               exposeHeader.add("x-obs-expose-header");
               rule.setExposeHeader(exposeHeader);
               // Specify the browser's cache time of the returned results of OPTIONS requests for specific resources, in seconds.
               rule.setMaxAgeSecond(10);
               rules.add(rule);
               cors.setRules(rules);
               obsClient.setBucketCors("examplebucket", cors);
               System.out.println("setBucketCors successfully");
           } catch (ObsException e) {
               System.out.println("setBucketCors failed");
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
               System.out.println("setBucketCors failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
