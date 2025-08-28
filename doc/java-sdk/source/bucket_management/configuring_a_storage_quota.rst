:original_name: obs_21_0410.html

.. _obs_21_0410:

Configuring a Storage Quota
===========================

Function
--------

A quota limits the maximum capacity allowed in a bucket. By default, there is no limit on the storage capacity of the entire OBS system or a single bucket, and any number of objects can be stored. You can set a storage quota to control the total size of objects that can be uploaded to the bucket. After the storage quota has been reached, object upload will fail.

A quota limit does not apply to the objects uploaded before the quota is configured. If the specified quota is already smaller than the total size of existing objects in the bucket, the existing objects in the bucket will not be deleted, but no more object can be uploaded to the bucket later. In this case, to upload new objects, you must delete some of the existing objects to make the used space below the quota limit.

Restrictions
------------

-  A bucket quota must be a non-negative integer in bytes.
-  OBS does not provide an API for deleting bucket storage quotas. You can set the bucket storage quota to **0** to cancel the limit.
-  To configure a storage quota for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketQuota** in IAM or **PutBucketQuota** in a bucket policy).

Method
------

obsClient.setBucketQuota(String :ref:`bucketName <obs_21_0410__table14455523>`, :ref:`BucketQuota <obs_21_0410__table195191356482>` :ref:`bucketQuota <obs_21_0410__table14455523>`)

Request Parameters
------------------

.. _obs_21_0410__table14455523:

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=====================================================+====================+===================================================================================================================================================================================+
   | bucketName      | String                                              | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    | Bucket name.                                                                                                                                                                      |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                     |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                     |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                     |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                     |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                     |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    | None                                                                                                                                                                              |
   +-----------------+-----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bucketQuota     | :ref:`BucketQuota <obs_21_0410__table195191356482>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    | Bucket quota information                                                                                                                                                          |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                     |                    |                                                                                                                                                                                   |
   |                 |                                                     |                    | See :ref:`Table 2 <obs_21_0410__table195191356482>`.                                                                                                                              |
   +-----------------+-----------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0410__table195191356482:

.. table:: **Table 2** BucketQuota

   +-----------------+-----------------+--------------------+---------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                   |
   +=================+=================+====================+===============================================================+
   | bucketQuota     | long            | Yes                | **Explanation:**                                              |
   |                 |                 |                    |                                                               |
   |                 |                 |                    | Bucket quota.                                                 |
   |                 |                 |                    |                                                               |
   |                 |                 |                    | **Value range**:                                              |
   |                 |                 |                    |                                                               |
   |                 |                 |                    | A non-negative integer, in bytes.                             |
   |                 |                 |                    |                                                               |
   |                 |                 |                    | **Default value**:                                            |
   |                 |                 |                    |                                                               |
   |                 |                 |                    | **0**, indicating that there is no limit on the bucket quota. |
   +-----------------+-----------------+--------------------+---------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** Common response headers

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

This example configures a quota for bucket **exampleBucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.BucketQuota;
   public class SetBucketQuota001 {
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
               // Example bucket name
               String exampleBucket = "examplebucket";
               // Example bucket quota
               long exampleBucketQuota = 1024 * 1024 * 100L;
               // Set the bucket quota to 100 MB.
               BucketQuota quota = new BucketQuota(exampleBucketQuota);
               obsClient.setBucketQuota(exampleBucket, quota);
               System.out.println("SetBucketQuota successfully");
           } catch (ObsException e) {
               System.out.println("SetBucketQuota failed");
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
               System.out.println("SetBucketQuota failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
