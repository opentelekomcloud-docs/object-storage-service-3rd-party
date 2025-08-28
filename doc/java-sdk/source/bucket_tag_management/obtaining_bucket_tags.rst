:original_name: obs_21_1703.html

.. _obs_21_1703:

Obtaining Bucket Tags
=====================

Function
--------

If you add tags to a bucket, SDRs generated for the requests sent to this bucket will include these tags, so you can use the tags to classify SDRs for detailed cost analysis. For example, if you have an application that uploads its running data to a bucket, you can tag the bucket with the application name. In this manner, the costs of the application can be analyzed using tags in SDRs.

This API returns the tags of a bucket.

Restrictions
------------

-  To obtain the bucket tags, you must be the bucket owner or have the required permission (**obs:bucket:GetBucketTagging** in IAM or **GetBucketTagging** in a bucket policy).

Method
------

obsClient.getBucketTagging(final :ref:`BaseBucketRequest <obs_21_1703__table43960571>` :ref:`request <obs_21_1703__table72121329103020>`)

Request Parameters
------------------

.. _obs_21_1703__table72121329103020:

.. table:: **Table 1** List of request parameters

   +-----------------+-------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                  | Mandatory (Yes/No) | Description                                                                                                           |
   +=================+=======================================================+====================+=======================================================================================================================+
   | request         | :ref:`BaseBucketRequest <obs_21_1703__table43960571>` | Yes                | **Explanation:**                                                                                                      |
   |                 |                                                       |                    |                                                                                                                       |
   |                 |                                                       |                    | Request parameters related to basic bucket information. For details, see :ref:`Table 2 <obs_21_1703__table43960571>`. |
   +-----------------+-------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1703__table43960571:

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

.. table:: **Table 3** BucketTagInfo

   +-----------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                         | Description                                                                                                                                                                 |
   +=======================+==============================================+=============================================================================================================================================================================+
   | tagSet                | :ref:`TagSet <obs_21_1703__table1541933712>` | **Explanation:**                                                                                                                                                            |
   |                       |                                              |                                                                                                                                                                             |
   |                       |                                              | Tag set. For details, see :ref:`Table 4 <obs_21_1703__table1541933712>`.                                                                                                    |
   +-----------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | statusCode            | int                                          | **Explanation:**                                                                                                                                                            |
   |                       |                                              |                                                                                                                                                                             |
   |                       |                                              | HTTP status code.                                                                                                                                                           |
   |                       |                                              |                                                                                                                                                                             |
   |                       |                                              | **Value range**:                                                                                                                                                            |
   |                       |                                              |                                                                                                                                                                             |
   |                       |                                              | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                                              |                                                                                                                                                                             |
   |                       |                                              | **Default value**:                                                                                                                                                          |
   |                       |                                              |                                                                                                                                                                             |
   |                       |                                              | None                                                                                                                                                                        |
   +-----------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | responseHeaders       | Map<String, Object>                          | **Explanation:**                                                                                                                                                            |
   |                       |                                              |                                                                                                                                                                             |
   |                       |                                              | HTTP response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header. |
   |                       |                                              |                                                                                                                                                                             |
   |                       |                                              | **Default value**:                                                                                                                                                          |
   |                       |                                              |                                                                                                                                                                             |
   |                       |                                              | None                                                                                                                                                                        |
   +-----------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1703__table1541933712:

.. table:: **Table 4** TagSet

   +-----------------------+---------------------------------------------------+-----------------------------------------------------------------------------+
   | Parameter             | Type                                              | Description                                                                 |
   +=======================+===================================================+=============================================================================+
   | tags                  | List<:ref:`Tag <obs_21_1703__table183868246819>`> | **Explanation:**                                                            |
   |                       |                                                   |                                                                             |
   |                       |                                                   | Tag list. For details, see :ref:`Table 5 <obs_21_1703__table183868246819>`. |
   +-----------------------+---------------------------------------------------+-----------------------------------------------------------------------------+

.. _obs_21_1703__table183868246819:

.. table:: **Table 5** Tag

   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                                                                                                     |
   +=================+=================+====================+=================================================================================================================================================================================================================================================================================================================================+
   | key             | String          | Yes                | **Explanation:**                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | Tag key.                                                                                                                                                                                                                                                                                                                        |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | -  The tag key in the same bucket must be unique.                                                                                                                                                                                                                                                                               |
   |                 |                 |                    | -  You can define tags or select the ones predefined on TMS.                                                                                                                                                                                                                                                                    |
   |                 |                 |                    | -  The key must contain 1 to 128 characters.                                                                                                                                                                                                                                                                                    |
   |                 |                 |                    | -  Unicode is supported.                                                                                                                                                                                                                                                                                                        |
   |                 |                 |                    | -  Tag keys cannot start or end with a space and cannot contain commas (,), asterisks (*), vertical bars (|), slashes (/), less-than signs (<), greater-than signs (>), equal signs (=), backslashes (\\), or ASCII control characters (0x00 to 0x1F). Tag keys and values must be URL encoded before being sent to a server.   |
   |                 |                 |                    | -  The value is case-sensitive.                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                                                                            |
   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | value           | String          | Yes                | **Explanation:**                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | Tag value.                                                                                                                                                                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | -  Tag values can be duplicated or left blank.                                                                                                                                                                                                                                                                                  |
   |                 |                 |                    | -  The value must contain 0 to 255 characters.                                                                                                                                                                                                                                                                                  |
   |                 |                 |                    | -  Unicode is supported.                                                                                                                                                                                                                                                                                                        |
   |                 |                 |                    | -  Tag values cannot start or end with a space and cannot contain commas (,), asterisks (*), vertical bars (|), slashes (/), less-than signs (<), greater-than signs (>), equal signs (=), backslashes (\\), or ASCII control characters (0x00 to 0x1F). Tag keys and values must be URL encoded before being sent to a server. |
   |                 |                 |                    | -  The value is case-sensitive.                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                                                                            |
   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example returns tags of bucket **examplebucket** using **obsClient.getBucketTagging**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.BucketTagInfo;
   public class GetBucketTagging001
   {
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
               // Obtain bucket tags.
               BucketTagInfo bucketTagInfo = obsClient.getBucketTagging("examplebucket");
               for(BucketTagInfo.TagSet.Tag tag : bucketTagInfo.getTagSet().getTags()){
                   System.out.println("\t" + tag.getKey() + ":" + tag.getValue());}
               System.out.println("getBucketTagging successfully");
           } catch (ObsException e) {
               System.out.println("getBucketTagging failed");
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
               System.out.println("getBucketTagging failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
