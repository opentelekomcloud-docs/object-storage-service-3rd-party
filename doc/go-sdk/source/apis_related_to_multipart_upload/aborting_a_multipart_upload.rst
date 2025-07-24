:original_name: obs_33_0516.html

.. _obs_33_0516:

Aborting a Multipart Upload
===========================

Function
--------

This API aborts a multipart upload using the multipart upload ID.

After a multipart upload is aborted, the upload ID cannot be used to upload any part. The storage occupied by any uploaded parts will be released. If any part uploads are in progress, aborting the multipart upload might or might not make the uploads successful. To release the storage occupied by all uploaded parts, abort the multipart upload only after all parts have been uploaded.

Restrictions
------------

-  To abort a multipart upload, you must be the bucket owner or have the required permission (**obs:object:AbortMultipartUpload** in IAM or **AbortMultipartUpload** in a bucket policy).

Method
------

**func** (obsClient ObsClient) AbortMultipartUpload(input \*\ :ref:`AbortMultipartUploadInput <obs_33_0516__table296025017509>`) (output \*\ :ref:`BaseModel <obs_33_0516__table1752539145118>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                                  | Mandatory (Yes/No) | Description                                                                                                         |
   +=================+=======================================================================+====================+=====================================================================================================================+
   | input           | \*\ :ref:`AbortMultipartUploadInput <obs_33_0516__table296025017509>` | Yes                | **Explanation:**                                                                                                    |
   |                 |                                                                       |                    |                                                                                                                     |
   |                 |                                                                       |                    | Input parameters for aborting a multipart upload. For details, see :ref:`Table 2 <obs_33_0516__table296025017509>`. |
   +-----------------+-----------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0516__table296025017509:

.. table:: **Table 2** AbortMultipartUploadInput

   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=================+====================+===================================================================================================================================================================================+
   | Bucket          | string          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Bucket name                                                                                                                                                                       |
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
   |                 |                 |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key             | string          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                             |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | UploadId        | string          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Multipart upload ID, for example, **000001648453845DBB78F2340DD460D8**                                                                                                            |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | The value must contain 32 characters.                                                                                                                                             |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** List of returned results

   +-----------------------+--------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Parameter             | Type                                                   | Description                                                                          |
   +=======================+========================================================+======================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0516__table1752539145118>` | **Explanation:**                                                                     |
   |                       |                                                        |                                                                                      |
   |                       |                                                        | Returned results. For details, see :ref:`Table 4 <obs_33_0516__table1752539145118>`. |
   +-----------------------+--------------------------------------------------------+--------------------------------------------------------------------------------------+
   | err                   | error                                                  | **Explanation:**                                                                     |
   |                       |                                                        |                                                                                      |
   |                       |                                                        | Error messages returned by the API                                                   |
   +-----------------------+--------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_33_0516__table1752539145118:

.. table:: **Table 4** BaseModel

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================+
   | StatusCode            | int                   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP status code                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Request ID returned by the OBS server                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ResponseHeaders       | map[string][]string   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP response headers                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Example
------------

This example aborts a multipart upload.

::

   package main

   import (
       "fmt"
       "os"
       "obs-sdk-go/obs"
   )
   func main() {
       //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
       //Obtain an AK/SK pair on the management console.
       ak := os.Getenv("AccessKeyID")
       sk := os.Getenv("SecretAccessKey")
       // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
       // securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint/*, obs.WithSecurityToken(securityToken)*/)
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.AbortMultipartUploadInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify the object (example/objectname as an example) to upload.
       input.Key = "example/objectname"
       // Specify the multipart upload ID (00000188677110424014075CC4A77xxx as an example).
       input.UploadId = "00000188677110424014075CC4A77xxx"
       // Abort the multipart upload.
       output, err := obsClient.AbortMultipartUpload(input)
       if err == nil {
           fmt.Printf("Abort multipart upload successful!\n")
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Abort multipart upload fail!\n")
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
