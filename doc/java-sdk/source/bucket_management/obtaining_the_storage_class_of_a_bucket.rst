:original_name: obs_21_0416.html

.. _obs_21_0416:

Obtaining the Storage Class of a Bucket
=======================================

Function
--------

This API returns the storage class of a bucket.

Restrictions
------------

-  To obtain a bucket's storage class, you must be the bucket owner or have the required permission (**obs:bucket:GetBucketStoragePolicy** in IAM or **GetBucketStoragePolicy** in a bucket policy).

Method
------

obsClient.getBucketStoragePolicy(String :ref:`bucketName <obs_21_0416__table52189740>`)

Request Parameters
------------------

.. _obs_21_0416__table52189740:

.. table:: **Table 1** List of request parameters

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

.. table:: **Table 2** BucketStoragePolicyConfiguration

   +-----------------------+-----------------------------------------------------------+-------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                      | Description                                                                                     |
   +=======================+===========================================================+=================================================================================================+
   | storageClass          | :ref:`StorageClassEnum <obs_21_0416__table1038544124819>` | **Explanation:**                                                                                |
   |                       |                                                           |                                                                                                 |
   |                       |                                                           | Storage class of the bucket. For details, see :ref:`Table 3 <obs_21_0416__table1038544124819>`. |
   +-----------------------+-----------------------------------------------------------+-------------------------------------------------------------------------------------------------+

.. _obs_21_0416__table1038544124819:

.. table:: **Table 3** StorageClassEnum

   ======== ============= =======================
   Constant Default Value Description
   ======== ============= =======================
   STANDARD STANDARD      Standard storage class.
   WARM     WARM          Warm storage class.
   COLD     COLD          Cold storage class.
   ======== ============= =======================

Code Examples
-------------

This example configures a storage class for bucket **exampleBucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.BucketStoragePolicyConfiguration;
   public class GetBucketStoragePolicy001 {
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
               // Obtain the bucket's storage class.
               BucketStoragePolicyConfiguration storagePolicy = obsClient.getBucketStoragePolicy(exampleBucket);
               System.out.println("GetBucketStoragePolicy successfully");
               System.out.println("GetBucketStorageClass:" + storagePolicy.getBucketStorageClass());
           } catch (ObsException e) {
               System.out.println("GetBucketStoragePolicy failed");
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
               System.out.println("GetBucketStoragePolicy failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
