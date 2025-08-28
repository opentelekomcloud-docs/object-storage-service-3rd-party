:original_name: obs_21_0411.html

.. _obs_21_0411:

Configuring a Storage Class for a Bucket
========================================

Function
--------

This API configures a storage class for a bucket. If you do not specify a storage class when uploading or copying an object, or initiating a multipart upload, the object inherits the bucket's storage class.

The following table lists the three available storage classes.

+---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+
| Storage Class | Description                                                                                                                                                                       | Value in OBS Java SDK     |
+===============+===================================================================================================================================================================================+===========================+
| Standard      | Features low access latency and high throughput and is used for storing massive, frequently accessed (multiple times a month) or small objects (< 1 MB) requiring quick response. | StorageClassEnum.STANDARD |
+---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------+

Restrictions
------------

-  To configure a storage class for a bucket, you must be the bucket owner or have the required permission (**obs:PutBucketStoragePolicy** in IAM or **PutBucketStoragePolicy** in a bucket policy).
-  The bucket storage class is independent from the storage classes of objects in the bucket. When uploading an object, if you do not specify a storage class for the object, the object will use the same storage class that the bucket uses. However, after the object is uploaded, its storage class will not change as that of the bucket changes. Likewise, the storage class of the bucket will also not change if the storage class of any objects therein changes.

Method
------

obsClient.setBucketStoragePolicy(String :ref:`bucketName <obs_21_0411__table14455523>`, :ref:`BucketStoragePolicyConfiguration <obs_21_0411__table94701456392>` :ref:`bucketStorage <obs_21_0411__table14455523>`)

Request Parameters
------------------

.. _obs_21_0411__table14455523:

.. table:: **Table 1** Request parameters

   +-----------------+-------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                                    | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=========================================================================+====================+===================================================================================================================================================================================+
   | bucketName      | String                                                                  | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | Bucket name.                                                                                                                                                                      |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                                         |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                                         |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                                         |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                                         |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                                         |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | None                                                                                                                                                                              |
   +-----------------+-------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bucketStorage   | :ref:`BucketStoragePolicyConfiguration <obs_21_0411__table94701456392>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 | (Inheriting :ref:`HeaderResponse <obs_21_0411__table1177392644719>`)    |                    | Storage class of the bucket.                                                                                                                                                      |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | See :ref:`Table 2 <obs_21_0411__table94701456392>`.                                                                                                                               |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                                         |                    | None                                                                                                                                                                              |
   +-----------------+-------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0411__table94701456392:

.. table:: **Table 2** BucketStoragePolicyConfiguration

   +-----------------------+-----------------------------------------------------------+-------------------------------------------------------+
   | Parameter             | Type                                                      | Description                                           |
   +=======================+===========================================================+=======================================================+
   | storageClass          | :ref:`StorageClassEnum <obs_21_0411__table1038544124819>` | **Explanation:**                                      |
   |                       |                                                           |                                                       |
   |                       |                                                           | Storage class of the bucket.                          |
   |                       |                                                           |                                                       |
   |                       |                                                           | **Value range**:                                      |
   |                       |                                                           |                                                       |
   |                       |                                                           | See :ref:`Table 3 <obs_21_0411__table1038544124819>`. |
   |                       |                                                           |                                                       |
   |                       |                                                           | **Default value**:                                    |
   |                       |                                                           |                                                       |
   |                       |                                                           | None                                                  |
   +-----------------------+-----------------------------------------------------------+-------------------------------------------------------+

.. _obs_21_0411__table1038544124819:

.. table:: **Table 3** StorageClassEnum

   ======== ============= =======================
   Constant Default Value Description
   ======== ============= =======================
   STANDARD STANDARD      Standard storage class.
   WARM     WARM          Warm storage class.
   COLD     COLD          Cold storage class.
   ======== ============= =======================

Responses
---------

.. _obs_21_0411__table1177392644719:

.. table:: **Table 4** Common response headers

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

This example configures a storage class for bucket **exampleBucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.AccessControlList;
   import com.obs.services.model.AvailableZoneEnum;
   import com.obs.services.model.CreateBucketRequest;
   import com.obs.services.model.ObsBucket;
   import com.obs.services.model.StorageClassEnum;

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
               CreateBucketRequest request = new CreateBucketRequest();
               // Example bucket name
               String exampleBucket = "examplebucket";
               // Example bucket location
               request.setBucketName(exampleBucket);
               // Set the bucket ACL to Private (the default value).
               request.setAcl(AccessControlList.REST_CANNED_PRIVATE);
               // Set the bucket storage class to Standard.
               request.setBucketStorageClass(StorageClassEnum.STANDARD);
               request.setLocation(exampleLocation);
               // Create a bucket.
               ObsBucket bucket = obsClient.createBucket(request);
               // The bucket is created.
               System.out.println("CreateBucket successfully");
               System.out.println("RequestId:"+bucket.getRequestId());


           } catch (ObsException e) {
               System.out.println("CreateBucket failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code: " + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message: " + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
           } catch (Exception e) {
               System.out.println("CreateBucket failed");
               // Print other error information.
               e.printStackTrace();

           }
       }
   }
