:original_name: obs_21_0708.html

.. _obs_21_0708:

Restoring a Cold Object
=======================

Function
--------

Cold objects must first be restored before you can download them. Cold objects can be restored in either of the following ways.

+-----------+-----------------------------------------------------------------------+---------------------------+
| Option    | Description                                                           | Value in OBS Java SDK     |
+===========+=======================================================================+===========================+
| Expedited | Data can be restored within 1 to 5 minutes.                           | RestoreTierEnum.EXPEDITED |
+-----------+-----------------------------------------------------------------------+---------------------------+
| Standard  | Data can be restored within 3 to 5 hours. This is the default option. | RestoreTierEnum.STANDARD  |
+-----------+-----------------------------------------------------------------------+---------------------------+

Restrictions
------------

-  To restore a Cold object, you must be the bucket owner or have the required permission (**obs:object:RestoreObject** in IAM or **RestoreObject** in a bucket policy.)
-  To prolong the validity period of the Cold data restored, you can repeatedly restore the data, but you will be billed for each restore. After a second restore, the validity period of Standard object copies will be prolonged, and you need to pay for storing these copies during the prolonged period.

-  The object specified in **ObsClient.restoreObject** must be in the Cold storage class. Otherwise, an exception will be thrown when you call this API.

Method
------

obsClient.restoreObject(:ref:`RestoreObjectRequest <obs_21_0708__table14455523>` :ref:`request <obs_21_0708__table1210700>`)

Request Parameters
------------------

.. _obs_21_0708__table1210700:

.. table:: **Table 1** List of request parameters

   +-----------------+----------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                     | Mandatory (Yes/No) | Description                                                                                                 |
   +=================+==========================================================+====================+=============================================================================================================+
   | request         | :ref:`RestoreObjectRequest <obs_21_0708__table14455523>` | Yes                | **Explanation:**                                                                                            |
   |                 |                                                          |                    |                                                                                                             |
   |                 |                                                          |                    | Request parameters for downloading an object. For details, see :ref:`Table 2 <obs_21_0708__table14455523>`. |
   +-----------------+----------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------+

.. _obs_21_0708__table14455523:

.. table:: **Table 2** RestoreObjectRequest

   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                      | Mandatory (Yes/No) | Description                                                                                                                                                                                |
   +=================+===========================================================+====================+============================================================================================================================================================================================+
   | bucketName      | String                                                    | Yes                | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | Bucket name.                                                                                                                                                                               |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Restrictions:**                                                                                                                                                                          |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                           |
   |                 |                                                           |                    | -  A bucket name:                                                                                                                                                                          |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                               |
   |                 |                                                           |                    |    -  Cannot be formatted as an IP address.                                                                                                                                                |
   |                 |                                                           |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                 |
   |                 |                                                           |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                            |
   |                 |                                                           |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                    |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.          |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | None                                                                                                                                                                                       |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey       | String                                                    | Yes                | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                                      |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | The value must contain 1 to 1,024 characters.                                                                                                                                              |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | None                                                                                                                                                                                       |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | versionId       | String                                                    | No                 | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | Version ID of the Cold object to be restored                                                                                                                                               |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | None. If this parameter is left blank, the latest version of the object is specified.                                                                                                      |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | days            | int                                                       | Yes                | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | After an object is restored, a Standard copy of it is generated. This parameter specifies how long the Standard copy can be retained, that is, the validity period of the restored object. |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Restrictions:**                                                                                                                                                                          |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | The value must be a positive integer.                                                                                                                                                      |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | The value ranges from 1 to 30, in days.                                                                                                                                                    |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | None                                                                                                                                                                                       |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | tier            | :ref:`RestoreTierEnum <obs_21_0708__table81731855162317>` | No                 | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | The restore option, which indicates the time spent on restoring the object.                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | For details, see :ref:`Table 3 <obs_21_0708__table81731855162317>`.                                                                                                                        |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | Standard                                                                                                                                                                                   |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0708__table81731855162317:

.. table:: **Table 3** RestoreTierEnum

   +-----------+---------------+----------------------------------------------------------------------+
   | Constant  | Default Value | Description                                                          |
   +===========+===============+======================================================================+
   | EXPEDITED | Expedited     | Objects can be restored at an expedited speed within 1 to 5 minutes. |
   +-----------+---------------+----------------------------------------------------------------------+
   | STANDARD  | Standard      | Objects can be restored at a standard speed within 3 to 5 hours.     |
   +-----------+---------------+----------------------------------------------------------------------+

Responses
---------

.. table:: **Table 4** RestoreObjectStatus

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
   |                       |                       | Response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header.      |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example restores object **objectname** from the Cold storage class using **ObsClient.restoreObject** and downloads it using **ObsClient.getObject**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.ObsObject;
   import com.obs.services.model.RestoreObjectRequest;
   import com.obs.services.model.RestoreTierEnum;
   public class GetObject007 {
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
               // Restore the Cold object.
               RestoreObjectRequest request = new RestoreObjectRequest();
               request.setBucketName("examplebucket");
               request.setObjectKey("objectname");
               request.setDays(1);
               request.setRestoreTier(RestoreTierEnum.EXPEDITED);
               obsClient.restoreObject(request);
               // Wait for the object to be restored.
               Thread.sleep(60 * 6 * 1000);
               // Download the object.
               ObsObject obsObject = obsClient.getObject("examplebucket", "objectname");
               System.out.println("getObject successfully");
               obsObject.getObjectContent().close();
           } catch (ObsException e) {
               System.out.println("getObject failed");
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
               System.out.println("getObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
