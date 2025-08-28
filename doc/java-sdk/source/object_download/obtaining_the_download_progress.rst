:original_name: obs_21_0704.html

.. _obs_21_0704:

Obtaining the Download Progress
===============================

Function
--------

This API returns the download progress of a specified object.

You can call **GetObjectRequest.setProgressInterval** to obtain the download progress.

Restrictions
------------

-  To obtain the download progress, you must be the bucket owner or have the required permission (**obs:object:GetObject** in IAM or **GetObject** in a bucket policy).
-  You can obtain the download progress when downloading an object in streaming, partial, or resumable mode.

Method
------

GetObjectRequest.setProgressListener(:ref:`ProgressListener <obs_21_0704__obs_21_0604_table06508445110>` :ref:`progressListener <obs_21_0704__obs_21_0604_table06508445110>`)

Request parameters
------------------

.. _obs_21_0704__obs_21_0604_table06508445110:

.. table:: **Table 1** List of request parameters

   +------------------+-------------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Type                                                                    | Mandatory (Yes/No) | Description                                                                                                                                  |
   +==================+=========================================================================+====================+==============================================================================================================================================+
   | progressListener | :ref:`ProgressListener <obs_21_0704__obs_21_0604_table134092034114420>` | Yes                | **Explanation:**                                                                                                                             |
   |                  |                                                                         |                    |                                                                                                                                              |
   |                  |                                                                         |                    | Data transmission listener used for obtaining the progress. For details, see :ref:`Table 2 <obs_21_0704__obs_21_0604_table134092034114420>`. |
   +------------------+-------------------------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0704__obs_21_0604_table134092034114420:

.. table:: **Table 2** ProgressListener

   +-----------------------------------------------------------------+-------------------+--------------------+------------------------------------------------------------------------------------------------------------+
   | Method                                                          | Return Value Type | Mandatory (Yes/No) | Description                                                                                                |
   +=================================================================+===================+====================+============================================================================================================+
   | :ref:`progressChanged <obs_21_0704__obs_21_0604_table14455523>` | void              | Yes                | **Explanation:**                                                                                           |
   |                                                                 |                   |                    |                                                                                                            |
   |                                                                 |                   |                    | Used for obtaining the progress. For details, see :ref:`Table 3 <obs_21_0704__obs_21_0604_table14455523>`. |
   +-----------------------------------------------------------------+-------------------+--------------------+------------------------------------------------------------------------------------------------------------+

.. _obs_21_0704__obs_21_0604_table14455523:

.. table:: **Table 3** progressChanged

   +-----------------+------------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                             | Mandatory (Yes/No) | Description                                                                                |
   +=================+==================================================================+====================+============================================================================================+
   | status          | :ref:`ProgressStatus <obs_21_0704__obs_21_0604_table8474713764>` | Yes                | **Explanation:**                                                                           |
   |                 |                                                                  |                    |                                                                                            |
   |                 |                                                                  |                    | Progress data. For details, see :ref:`Table 4 <obs_21_0704__obs_21_0604_table8474713764>`. |
   +-----------------+------------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------+

.. _obs_21_0704__obs_21_0604_table8474713764:

.. table:: **Table 4** ProgressStatus

   +----------------------------+-------------------+---------------------------------------------+
   | Method                     | Return Value Type | Description                                 |
   +============================+===================+=============================================+
   | getAverageSpeed()          | double            | Average transmission rate.                  |
   +----------------------------+-------------------+---------------------------------------------+
   | getInstantaneousSpeed()    | double            | Instantaneous transmission rate.            |
   +----------------------------+-------------------+---------------------------------------------+
   | getTransferPercentage()    | int               | Transmission progress, in percentage.       |
   +----------------------------+-------------------+---------------------------------------------+
   | getNewlyTransferredBytes() | long              | Number of the newly transmitted bytes.      |
   +----------------------------+-------------------+---------------------------------------------+
   | getTransferredBytes()      | long              | Number of bytes that have been transmitted. |
   +----------------------------+-------------------+---------------------------------------------+
   | getTotalBytes()            | long              | Number of the bytes to be transmitted.      |
   +----------------------------+-------------------+---------------------------------------------+

Code Examples
-------------

This example returns the progress of downloading object **objectname**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.GetObjectRequest;
   import com.obs.services.model.ObsObject;
   import com.obs.services.model.ProgressListener;
   import com.obs.services.model.ProgressStatus;
   import java.io.ByteArrayOutputStream;
   import java.io.InputStream;
   public class GetObject003 {
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
               // Obtain the download progresses.
               GetObjectRequest request = new GetObjectRequest("examplebucket", "objectname");
               request.setProgressListener(
                       new ProgressListener() {
                           @Override
                           public void progressChanged(ProgressStatus status) {
                               // Obtain the average download rate.
                               System.out.println("AverageSpeed:" + status.getAverageSpeed());
                               // Obtain the download progress in percentage.
                               System.out.println("TransferPercentage:" + status.getTransferPercentage());
                           }
                       });
               // Refresh the download progress each time 1 MB data is downloaded.
               request.setProgressInterval(1024 * 1024L);
               ObsObject obsObject = obsClient.getObject(request);
               // Read the object content.
               System.out.println("Object content:");
               InputStream input = obsObject.getObjectContent();
               byte[] b = new byte[1024];
               ByteArrayOutputStream bos = new ByteArrayOutputStream();
               int len;
               while ((len = input.read(b)) != -1) {
                   bos.write(b, 0, len);
               }
               System.out.println("getObjectContent successfully");
               System.out.println(new String(bos.toByteArray()));
               bos.close();
               input.close();
           } catch (ObsException e) {
               System.out.println("getObjectContent failed");
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
               System.out.println("getObjectContent failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
