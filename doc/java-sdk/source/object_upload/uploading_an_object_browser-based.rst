:original_name: obs_21_0612.html

.. _obs_21_0612:

Uploading an Object - Browser-Based
===================================

Function
--------

This API uploads an object up to 5 GB to a specified bucket in HTML form.

You can call **ObsClient.createPostSignature** to generate request parameters for a browser-based upload. The procedure is as follows:

#. Call **ObsClient.createPostSignature** to generate request parameters for authentication.
#. Prepare an HTML form.
#. Enter the request parameters in the page.
#. Select a local file and upload it in browser-based mode.

.. note::

   There are two request parameters generated for authentication:

   -  **Policy**, which corresponds to the **policy** parameter in the form
   -  **Signature**, which corresponds to the **signature** parameter in the form

Restrictions
------------

-  To upload an object, you must be the bucket owner or have the required permission (**obs:object:PutObject** in IAM or **PutObject** in a bucket policy).

-  Values of **policy** and **signature** in the HTML form are obtained from the returned results of **ObsClient.createPostSignature**.
-  During the object upload, the value of **contentType** needs to be manually changed to the corresponding **Content-Type** value.

Method
------

obsClient.createPostSignature(:ref:`PostSignatureRequest <obs_21_0612__table9147151314100>` :ref:`request <obs_21_0612__table1824117496403>`)

.. _obs_21_0612__table1824117496403:

.. table:: **Table 1** createPostSignature

   +-----------------+---------------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                          | Mandatory (Yes/No) | Description                                                                                                       |
   +=================+===============================================================+====================+===================================================================================================================+
   | request         | :ref:`PostSignatureRequest <obs_21_0612__table9147151314100>` | Yes                | **Explanation:**                                                                                                  |
   |                 |                                                               |                    |                                                                                                                   |
   |                 |                                                               |                    | Request parameters for a browser-based upload. For details, see :ref:`Table 2 <obs_21_0612__table9147151314100>`. |
   +-----------------+---------------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0612__table9147151314100:

.. table:: **Table 2** PostSignatureRequest

   +-----------------+---------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=====================+====================+===================================================================================================================================================================================+
   | bucketName      | String              | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | Bucket name.                                                                                                                                                                      |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                     |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                     |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                     |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                     |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                     |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Default value**:                                                                                                                                                                |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | None                                                                                                                                                                              |
   +-----------------+---------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey       | String              | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                             |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Value range**:                                                                                                                                                                  |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Default value**:                                                                                                                                                                |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | None                                                                                                                                                                              |
   +-----------------+---------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | requestDate     | Date                | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | Time the request is initiated.                                                                                                                                                    |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Default value**:                                                                                                                                                                |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | None                                                                                                                                                                              |
   +-----------------+---------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | expiryDate      | Date                | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | Date of expiry.                                                                                                                                                                   |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Default value**:                                                                                                                                                                |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | None                                                                                                                                                                              |
   +-----------------+---------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | expires         | long                | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | Validity period of authentication for a browser-based upload                                                                                                                      |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Value range**:                                                                                                                                                                  |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | An integer greater than 0, in seconds.                                                                                                                                            |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Default value**:                                                                                                                                                                |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | 300                                                                                                                                                                               |
   +-----------------+---------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | conditions      | List<String>        | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | The conditions specified for the form. The SDK uses the specified value to calculate the policy and ignores the **formParams**.                                                   |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Default value**:                                                                                                                                                                |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | None                                                                                                                                                                              |
   +-----------------+---------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | formParams      | Map<String, Object> | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | Form parameters in the request. *String* indicates the name of the form parameter, and *Object* indicates the value of the form parameter.                                        |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | **Default value**:                                                                                                                                                                |
   |                 |                     |                    |                                                                                                                                                                                   |
   |                 |                     |                    | None                                                                                                                                                                              |
   +-----------------+---------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** PostSignatureResponse

   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                      |
   +=======================+=======================+==================================================================================================================================================================================================+
   | OriginPolicy          | String                | **Explanation:**                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | Value of **Policy** that is not encoded by Base64. This parameter can only be used for verification. For example:                                                                                |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **{"expiration":"2023-09-12T12:52:59Z","conditions":[{"content-type":"text/plain"},{"bucket":"examplebucket"},{"key":"example/objectname"},]}"**                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Policy                | String                | **Explanation:**                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | Base64-encoded value of the policy. For example:                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **eyJleHBpcmF0aW9uIjoiMjAyMy0wOS0xMlQxMjo1Mjo1OVoiLCJjb25kaXRpb25zIjpbeyJjb250ZW50LXR5cGUiOiJ0ZXh0L3BsYWluIn0seyJidWNrZXQiOiJleGFtcGxlYnVja2V0In0seyJrZXkiOiJleGFtcGxlL29iamVjdG5hbWUifSxdfQ==** |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Signature             | String                | **Explanation:**                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **signature** in the form. For example:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **g0jQr4v9VWd1Q2FOFDG6LGfV9Cw=**                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example generates authorization parameters for a browser-based upload.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.PostSignatureRequest;
   import com.obs.services.model.PostSignatureResponse;
   import java.util.HashMap;
   import java.util.Map;
   public class PostObject001 {
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
               // Generate a request for a browser-based upload.
               PostSignatureRequest request = new PostSignatureRequest();
               // Set form parameters.
               Map<String, Object> formParams = new HashMap<String, Object>();
               // Set the object ACL to public read.
               formParams.put("x-obs-acl", "public-read");
               // Set the MIME type for an object.
               formParams.put("content-type", "text/plain");
               request.setFormParams(formParams);
               // Set the validity period for the browser-based upload request, in seconds.
               request.setExpires(3600);
               PostSignatureResponse response = obsClient.createPostSignature(request);
               System.out.println("createPostSignature successfully");
               // Obtain the request parameters.
               System.out.println("Policy:" + response.getPolicy());
               System.out.println("Signature:" + response.getSignature());
           } catch (ObsException e) {
               System.out.println("createPostSignature failed");
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
               System.out.println("createPostSignature failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

This example is an HTML form.

::

   <html>
   <head>
       <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
   </head>
   <body>
   <form action="http://bucketname.your-endpoint/" method="post" enctype="multipart/form-data">
       Object key
       <!-- Object name -->
       <input type="text" name="key" value="objectname" />
       <p>
           ACL
           <!-- Object ACL -->
           <input type="text" name="x-obs-acl" value="public-read" />
       <p>
           Content-Type
           <!-- Object MIME type -->
           <input type="text" name="content-type" value="text/plain" />
       <p>
           <!-- Use the value returned by PostSignatureResponse.getPolicy(). -->
           <input type="hidden" name="policy" value="*** Provide your policy ***" />
           <!-- AK -->
           <input type="hidden" name="AccessKeyId" value="*** Provide your access key ***"/>
           <!-- Signature string -->
           <input type="hidden" name="signature" value="*** Provide your signature ***"/>
           <!-- If x-obs-security-token exists, remove the comment for the following line and specify the actual value of x-obs-security-token. -->
           <!-- <input type="hidden" name="x-obs-security-token" value="*** Provide your x-obs-security-token ***"/>-->
           <input name="file" type="file" />
           <input name="submit" value="Upload" type="submit" />
   </form>
   </body>
   </html>
