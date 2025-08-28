:original_name: obs_21_0807.html

.. _obs_21_0807:

Checking Whether an Object Exists
=================================

Function
--------

This API checks whether an object exists. If the returned HTTP status code is **200**, the object exists. If the returned HTTP status code is **404**, the object or bucket does not exist.

Restrictions
------------

-  To check whether an object exists, you must be the bucket owner or have the required permission (**obs:object:GetObject** in IAM or **GetObject** in a bucket policy).

Method
------

doesObjectExist(final :ref:`GetObjectMetadataRequest <obs_21_0807__obs_21_0801_table14455523>` :ref:`request <obs_21_0807__obs_21_0801_table1210700>`)

Request Parameters
------------------

.. _obs_21_0807__obs_21_0801_table1210700:

.. table:: **Table 1** List of request parameters

   +-----------------+--------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                                     | Mandatory (Yes/No) | Description                                                                                   |
   +=================+==========================================================================+====================+===============================================================================================+
   | request         | :ref:`GetObjectMetadataRequest <obs_21_0807__obs_21_0801_table14455523>` | Yes                | **Explanation:**                                                                              |
   |                 |                                                                          |                    |                                                                                               |
   |                 |                                                                          |                    | Request parameters. For details, see :ref:`Table 2 <obs_21_0807__obs_21_0801_table14455523>`. |
   +-----------------+--------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------+

.. _obs_21_0807__obs_21_0801_table14455523:

.. table:: **Table 2** GetObjectMetadataRequest

   +-----------------+-------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                              | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                        |
   +=================+===================================================================+====================+====================================================================================================================================================================================================================================================+
   | bucketName      | String                                                            | Yes                | **Explanation:**                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | Bucket name.                                                                                                                                                                                                                                       |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Restrictions:**                                                                                                                                                                                                                                  |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                                   |
   |                 |                                                                   |                    | -  A bucket name:                                                                                                                                                                                                                                  |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                       |
   |                 |                                                                   |                    |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                        |
   |                 |                                                                   |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                         |
   |                 |                                                                   |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                                    |
   |                 |                                                                   |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                            |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.                                                                  |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Default value**:                                                                                                                                                                                                                                 |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | None                                                                                                                                                                                                                                               |
   +-----------------+-------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey       | String                                                            | Yes                | **Explanation:**                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                                                                                              |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Value range**:                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                      |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Default value**:                                                                                                                                                                                                                                 |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | None                                                                                                                                                                                                                                               |
   +-----------------+-------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | versionId       | String                                                            | No                 | **Explanation:**                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | Object version ID.                                                                                                                                                                                                                                 |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Value range**:                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | The value must contain 32 characters.                                                                                                                                                                                                              |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Default value**:                                                                                                                                                                                                                                 |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | None                                                                                                                                                                                                                                               |
   +-----------------+-------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | userHeaders     | HashMap<String, String>                                           | No                 | **Explanation:**                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | User header list. In **HashMap**, the **String** key and value indicate the name and value of the user header field respectively. The SDK does not process the **userHeaders** and instead transparently transmits it to the server for later use. |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Value range**:                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | The value must contain 32 characters.                                                                                                                                                                                                              |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Default value**:                                                                                                                                                                                                                                 |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | None                                                                                                                                                                                                                                               |
   +-----------------+-------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | encodeHeaders   | boolean                                                           | No                 | **Explanation:**                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | Whether to encode and decode HTTP headers.                                                                                                                                                                                                         |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Value range**:                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **true**: HTTP headers are encoded and decoded.                                                                                                                                                                                                    |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **false**: HTTP headers are not encoded or decoded.                                                                                                                                                                                                |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **Default value**:                                                                                                                                                                                                                                 |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | **true**                                                                                                                                                                                                                                           |
   +-----------------+-------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | sseHeader       | :ref:`SseCHeader <obs_21_0807__obs_21_0801_table166661610121615>` | No                 | **Explanation:**                                                                                                                                                                                                                                   |
   |                 |                                                                   |                    |                                                                                                                                                                                                                                                    |
   |                 |                                                                   |                    | Server-side decryption headers. For details, see :ref:`Table 3 <obs_21_0807__obs_21_0801_table166661610121615>`.                                                                                                                                   |
   +-----------------+-------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0807__obs_21_0801_table166661610121615:

.. table:: **Table 3** SseCHeader

   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                       | Mandatory (Yes/No) | Description                                                                                                                             |
   +=================+============================================================+====================+=========================================================================================================================================+
   | algorithm       | :ref:`ServerAlgorithm <obs_21_0807__table195461527192917>` | Yes                | **Explanation:**                                                                                                                        |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | SSE-C is used for encrypting objects on the server side.                                                                                |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | **Value range**:                                                                                                                        |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | **AES256**, indicating AES is used to encrypt the object in SSE-C. For details, see :ref:`Table 4 <obs_21_0807__table195461527192917>`. |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | **Default value**:                                                                                                                      |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | None                                                                                                                                    |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | sseAlgorithm    | :ref:`SSEAlgorithmEnum <obs_21_0807__table098813376299>`   | No                 | **Explanation:**                                                                                                                        |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | Encryption algorithm.                                                                                                                   |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | **Restrictions:**                                                                                                                       |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | Only AES256 is supported.                                                                                                               |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | **Value range**:                                                                                                                        |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | See :ref:`Table 5 <obs_21_0807__table098813376299>`.                                                                                    |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | **Default value**:                                                                                                                      |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | None                                                                                                                                    |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | sseCKey         | byte[]                                                     | Yes                | **Explanation:**                                                                                                                        |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | Key used for encrypting the object when SSE-C is used, in byte[] format.                                                                |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | **Default value**:                                                                                                                      |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | None                                                                                                                                    |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
   | sseCKeyBase64   | String                                                     | No                 | **Explanation:**                                                                                                                        |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | Base64-encoded key used for encrypting the object when SSE-C is used.                                                                   |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | **Default value**:                                                                                                                      |
   |                 |                                                            |                    |                                                                                                                                         |
   |                 |                                                            |                    | None                                                                                                                                    |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0807__table195461527192917:

.. table:: **Table 4** ServerAlgorithm

   ======== =============
   Constant Default Value
   ======== =============
   AES256   AES256
   ======== =============

.. _obs_21_0807__table098813376299:

.. table:: **Table 5** SSEAlgorithmEnum

   ======== =============
   Constant Default Value
   ======== =============
   KMS      kms
   AES256   AES256
   ======== =============

Responses
---------

.. table:: **Table 6** Response headers

   +--------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+------------------------------------------+
   | Method                                                                                                                                                 | Return Value Type | Description                              |
   +========================================================================================================================================================+===================+==========================================+
   | doesObjectExist(final :ref:`GetObjectMetadataRequest <obs_21_0807__obs_21_0801_table14455523>` :ref:`request <obs_21_0807__obs_21_0801_table1210700>`) | boolean           | Whether the object exists in the bucket. |
   +--------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+------------------------------------------+

Code Examples
-------------

This example checks whether object **objectname** exists in bucket **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   public class DoesObjectExist001 {
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
               // Check whether the specified object exists.
               System.out.println(obsClient.doesObjectExist("examplebucket", "objectname") ? "exists!" : "does not exist!");
               System.out.println("doesObjectExist successfully");
           } catch (ObsException e) {
               System.out.println("doesObjectExist failed");
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
               System.out.println("doesObjectExist failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
