:original_name: obs_21_0604.html

.. _obs_21_0604:

Obtaining the Upload Progress
=============================

Function
--------

This API returns the upload progress of a specified object.

You can call **PutObjectRequest.setProgressListener** to obtain the upload progress.

Restrictions
------------

-  To obtain the upload progress, you must have the **obs:object:PutObject** permission.
-  You can query the upload progress when uploading an object in streaming, file-based, multipart, appendable, or resumable mode.
-  If the value of **ProgressStatus.getTransferPercentage()** is **-1**, the content is uploaded in streaming mode. In this case, you must configure the **Content-Length** parameter.

Method
------

PutObjectRequest.setProgressListener(:ref:`ProgressListener <obs_21_0604__table134092034114420>` :ref:`progressListener <obs_21_0604__table06508445110>`)

Request parameters
------------------

.. _obs_21_0604__table06508445110:

.. table:: **Table 1** List of request parameters

   +------------------+-------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Type                                                        | Mandatory (Yes/No) | Description                                                                                                                        |
   +==================+=============================================================+====================+====================================================================================================================================+
   | progressListener | :ref:`ProgressListener <obs_21_0604__table134092034114420>` | Yes                | **Explanation:**                                                                                                                   |
   |                  |                                                             |                    |                                                                                                                                    |
   |                  |                                                             |                    | Data transmission listener for obtaining the upload progress. For details, see :ref:`Table 2 <obs_21_0604__table134092034114420>`. |
   +------------------+-------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0604__table134092034114420:

.. table:: **Table 2** ProgressListener

   +-----------------------------------------------------+-------------------+--------------------+-------------------------------------------------------------------------------------------------------+
   | Method                                              | Return Value Type | Mandatory (Yes/No) | Description                                                                                           |
   +=====================================================+===================+====================+=======================================================================================================+
   | :ref:`progressChanged <obs_21_0604__table14455523>` | void              | Yes                | **Explanation:**                                                                                      |
   |                                                     |                   |                    |                                                                                                       |
   |                                                     |                   |                    | Used for obtaining the upload progress. For details, see :ref:`Table 3 <obs_21_0604__table14455523>`. |
   +-----------------------------------------------------+-------------------+--------------------+-------------------------------------------------------------------------------------------------------+

.. _obs_21_0604__table14455523:

.. table:: **Table 3** progressChanged

   +-----------------+------------------------------------------------------+--------------------+--------------------------------------------------------------------------------+
   | Parameter       | Type                                                 | Mandatory (Yes/No) | Description                                                                    |
   +=================+======================================================+====================+================================================================================+
   | status          | :ref:`ProgressStatus <obs_21_0604__table8474713764>` | Yes                | **Explanation:**                                                               |
   |                 |                                                      |                    |                                                                                |
   |                 |                                                      |                    | Progress data. For details, see :ref:`Table 4 <obs_21_0604__table8474713764>`. |
   +-----------------+------------------------------------------------------+--------------------+--------------------------------------------------------------------------------+

.. _obs_21_0604__table8474713764:

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

This example returns the progress of uploading local file **exampleLocalFilePath** to bucket **examplebucket** as object **objectname**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.ProgressListener;
   import com.obs.services.model.ProgressStatus;
   import com.obs.services.model.PutObjectRequest;
   import java.io.File;
   public class PutObject005 {
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
               // Upload a file.
               PutObjectRequest request = new PutObjectRequest("examplebucket", "exampleobject");
               request.setFile(new File("exampleLocalFilePath"));
               request.setProgressListener(
                       new ProgressListener() {
                           @Override
                           public void progressChanged(ProgressStatus status) {
                               // Obtain the average upload rate.
                               System.out.println("AverageSpeed:" + status.getAverageSpeed());
                                // Obtain the upload progress in percentage.
                               System.out.println("TransferPercentage:" + status.getTransferPercentage());
                           }
                       });
               // Refresh the upload progress each time 1 MB data is uploaded.
               request.setProgressInterval(1024 * 1024L);
               obsClient.putObject(request);
               System.out.println("putObject successfully");
           } catch (ObsException e) {
               System.out.println("putObject failed");
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
               System.out.println("putObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

This example returns the progress of uploading local file **exampleFileName** in a stream to bucket **examplebucket** as object **objectname**.

.. code-block::

   import com.obs.services.ObsClient;
   import com.obs.services.ObsConfiguration;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.ObjectMetadata;
   import com.obs.services.model.ProgressListener;
   import com.obs.services.model.ProgressStatus;
   import com.obs.services.model.PutObjectRequest;
   import java.io.File;
   import java.io.FileInputStream;
   public class PutObjectByInputStreamWithProgress {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           String securityToken = System.getenv("SECURITY_TOKEN");
           // Enter the endpoint corresponding to the bucket.
           // Obtain an endpoint using environment variables or import it in other ways.
           // String endPoint = System.getenv("ENDPOINT");
           String endPoint = "https://obs.region.example.com";
           ObsConfiguration obsConfiguration = new ObsConfiguration();
           obsConfiguration.setEndPoint(endPoint);
           // Create an ObsClient instance.
           try (ObsClient obsClient = new ObsClient(ak, sk, securityToken, obsConfiguration)) {
               String exampleBucket = "examplebucket";
               String exampleObject = "objectname";
               String fileToUpload = "exampleFileName";
               long contentLength = new File(fileToUpload).length();
               PutObjectRequest request = new PutObjectRequest(exampleBucket, exampleObject, new FileInputStream(fileToUpload));
               ObjectMetadata objectMetadata = new ObjectMetadata();
               // Streaming uploads require the object attribute Content-Length must be configured.
               // Otherwise, ProgressStatus.getTransferPercentage () returns -1.
               objectMetadata.setContentLength(contentLength);
               request.setMetadata(objectMetadata);
               request.setProgressListener(
                   new ProgressListener() {
                       @Override
                       public void progressChanged(ProgressStatus status) {
                               // Obtain the average upload rate.
                           System.out.println("AverageSpeed:" + status.getAverageSpeed());
                                // Obtain the upload progress in percentage.
                           System.out.println("TransferPercentage:" + status.getTransferPercentage());
                       }
                   });
               // Refresh the upload progress each time 1 MB data is uploaded.
               request.setProgressInterval(1024 * 1024L);
               obsClient.putObject(request);
               System.out.println("putObject successfully");
           } catch (ObsException e) {
               System.out.println("putObject failed");
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
               System.out.println("putObject failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
