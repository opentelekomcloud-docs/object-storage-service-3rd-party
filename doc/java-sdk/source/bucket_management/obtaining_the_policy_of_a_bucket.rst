:original_name: obs_21_0413.html

.. _obs_21_0413:

Obtaining the Policy of a Bucket
================================

Function
--------

OBS provides access control over buckets. You can use an access policy to define whether a user can perform certain operations on a specific bucket. OBS access control can be implemented using IAM permissions, bucket policies, and ACLs. For more information, see .

This API returns the policy of a bucket.

Restrictions
------------

-  OBS returns **404 NoSuchBucketPolicy** when you call this API in the following scenarios:

   -  The specified bucket policy does not exist.
   -  The standard policy of the specified bucket is set to **Private** and no advanced policies are configured.

-  To obtain the policy of a bucket, you must be the bucket owner or the bucket owner's IAM user with the required permission (**obs:bucket:GetBucketPolicy** in IAM or **GetBucketPolicy** in a bucket policy).

Method
------

obsClient.getBucketPolicy(String :ref:`bucketName <obs_21_0413__table25490811>`)

Request Parameters
------------------

.. _obs_21_0413__table25490811:

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

.. table:: **Table 2** List of returned results

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                   |
   +=======================+=======================+===============================================================================================================================================+
   | policy                | String                | **Explanation:**                                                                                                                              |
   |                       |                       |                                                                                                                                               |
   |                       |                       | Policy information in JSON format                                                                                                             |
   |                       |                       |                                                                                                                                               |
   |                       |                       | **Restrictions:**                                                                                                                             |
   |                       |                       |                                                                                                                                               |
   |                       |                       | -  The bucket name contained in the **Resource** parameter of the policy must be the same as the one specified for the current bucket policy. |
   |                       |                       |                                                                                                                                               |
   |                       |                       | **Default value**:                                                                                                                            |
   |                       |                       |                                                                                                                                               |
   |                       |                       | None                                                                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example returns the policy of bucket **exampleBucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   public class GetBucketPolicy001 {
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
               String policy = obsClient.getBucketPolicy(exampleBucket);
               System.out.println("\t" + policy);
           } catch (ObsException e) {
               System.out.println("GetBucketAcl failed");
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
               System.out.println("GetBucketAcl failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
