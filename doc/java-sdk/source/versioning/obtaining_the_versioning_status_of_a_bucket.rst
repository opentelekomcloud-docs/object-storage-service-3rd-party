:original_name: obs_21_1003.html

.. _obs_21_1003:

Obtaining the Versioning Status of a Bucket
===========================================

Function
--------

You can enable versioning to automatically maintain previous versions of an object. When versioning is enabled, you can access earlier versions of an object to recover your data in the event of accidental actions or application failures.

This API obtains the versioning status of a bucket.

Restrictions
------------

-  To view the versioning status of a bucket, you must be the bucket owner or have the required permission (**obs:bucket:GetBucketVersioning** in IAM or **GetBucketVersioning** in a bucket policy).

Method
------

obsClient.getBucketVersioning(final :ref:`BaseBucketRequest <obs_21_1003__table13982202>` :ref:`request <obs_21_1003__table1210700>`)

Request Parameters
------------------

.. _obs_21_1003__table1210700:

.. table:: **Table 1** List of request parameters

   +-----------------+-------------------------------------------------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                  | Mandatory (Yes/No) | Description                                                                                                                     |
   +=================+=======================================================+====================+=================================================================================================================================+
   | request         | :ref:`BaseBucketRequest <obs_21_1003__table13982202>` | Yes                | **Explanation:**                                                                                                                |
   |                 |                                                       |                    |                                                                                                                                 |
   |                 |                                                       |                    | Request parameters for viewing the versioning status of a bucket. For details, see :ref:`Table 2 <obs_21_1003__table13982202>`. |
   +-----------------+-------------------------------------------------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1003__table13982202:

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

.. table:: **Table 3** BucketVersioningConfiguration

   +-----------------------+----------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                           | Description                                                                                                                                                                 |
   +=======================+================================================================+=============================================================================================================================================================================+
   | statusCode            | int                                                            | **Explanation:**                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | HTTP status code.                                                                                                                                                           |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Value range**:                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Default value**:                                                                                                                                                          |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | None                                                                                                                                                                        |
   +-----------------------+----------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | responseHeaders       | Map<String, Object>                                            | **Explanation:**                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | Response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header.      |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Default value**:                                                                                                                                                          |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | None                                                                                                                                                                        |
   +-----------------------+----------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                | :ref:`VersioningStatusEnum <obs_21_1003__table98461528202618>` | **Explanation:**                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | Versioning status of the bucket.                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | **Value range**:                                                                                                                                                            |
   |                       |                                                                |                                                                                                                                                                             |
   |                       |                                                                | See :ref:`Table 4 <obs_21_1003__table98461528202618>`.                                                                                                                      |
   +-----------------------+----------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1003__table98461528202618:

.. table:: **Table 4** VersioningStatusEnum

   ========= ============= ========================
   Constant  Default Value Description
   ========= ============= ========================
   SUSPENDED Suspended     Versioning is suspended.
   ENABLED   Enabled       Versioning is enabled.
   ========= ============= ========================

Code Examples
-------------

This example views the versioning status of bucket **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.BucketVersioningConfiguration;
   public class GetBucketVersioning001 {
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
               // View the versioning status of a bucket.
               BucketVersioningConfiguration status = obsClient.getBucketVersioning("examplebucket");
               System.out.println("getBucketVersioning successfully");
               System.out.println("getVersioningStatus:" + status.getVersioningStatus());
           } catch (ObsException e) {
               System.out.println("getBucketVersioning failed");
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
               System.out.println("getBucketVersioning failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
