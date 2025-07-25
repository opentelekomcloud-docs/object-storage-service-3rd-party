:original_name: obs_33_0601.html

.. _obs_33_0601:

Creating a Signed URL
=====================

Function
--------

This API creates a URL whose **Query** parameters are carried with authentication information by specifying the AK and SK, HTTP method, and request parameters. You can provide other users with this URL for temporary access. When generating a URL, you need to specify the validity period of the URL to restrict the access duration of visitors.

If you want to grant other users the permission to perform other operations on buckets or objects (for example, upload or download objects), generate a URL with the corresponding request (for example, to upload an object using the URL that generates the PUT request) and provide the URL for other users.

Restrictions
------------

-  If a CORS or signature mismatch error occurs, refer to the following steps to troubleshoot the issue:

   #. If CORS is not configured, you need to configure CORS rules on OBS Console.
   #. If the signatures do not match, check whether signature parameters are correct. For example, during an object upload, the backend uses **Content-Type** to calculate the signature and generate an authorized URL, but if **Content-Type** is not set or is set to an incorrect value when the frontend uses the authorized URL, a CORS error occurs. To avoid this issue, ensure that **Content-Type** fields at both the frontend and backend are kept consistent.

Method
------

**func** (obsClient ObsClient) CreateSignedUrl(input \*\ :ref:`CreateSignedUrlInput <obs_33_0601__table206638398315>`) (output \*\ :ref:`CreateSignedUrlOutput <obs_33_0601__table15448153632220>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                             | Mandatory (Yes/No) | Description                                                                                                   |
   +=================+==================================================================+====================+===============================================================================================================+
   | input           | \*\ :ref:`CreateSignedUrlInput <obs_33_0601__table206638398315>` | Yes                | **Explanation:**                                                                                              |
   |                 |                                                                  |                    |                                                                                                               |
   |                 |                                                                  |                    | Input parameters for creating a signed URL. For details, see :ref:`Table 2 <obs_33_0601__table206638398315>`. |
   +-----------------+------------------------------------------------------------------+--------------------+---------------------------------------------------------------------------------------------------------------+

.. _obs_33_0601__table206638398315:

.. table:: **Table 2** CreateSignedUrlInput

   +-----------------+---------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                    | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=========================================================+====================+===================================================================================================================================================================================+
   | Method          | :ref:`HttpMethodType <obs_33_0601__table12153312211>`   | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | HTTP method. For details, see :ref:`Table 3 <obs_33_0601__table12153312211>`.                                                                                                     |
   +-----------------+---------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Bucket          | string                                                  | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | Bucket name                                                                                                                                                                       |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                         |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                         |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                         |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                         |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                         |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | None                                                                                                                                                                              |
   +-----------------+---------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key             | string                                                  | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                             |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | None                                                                                                                                                                              |
   +-----------------+---------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SubResource     | :ref:`SubResourceType <obs_33_0601__table593654162113>` | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | Type of the subresource to access. For details, see :ref:`Table 4 <obs_33_0601__table593654162113>`.                                                                              |
   +-----------------+---------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Expires         | int                                                     | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | Expiration time of the signed URL                                                                                                                                                 |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | -  The value of this parameter for temporary credentials ranges from **0** to **86400**, in seconds.                                                                              |
   |                 |                                                         |                    | -  The value of this parameter for permanent keys ranges from **0** to **630720000**, in seconds.                                                                                 |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | 300                                                                                                                                                                               |
   +-----------------+---------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Headers         | map[string]string                                       | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | Headers in the request                                                                                                                                                            |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | None                                                                                                                                                                              |
   +-----------------+---------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | QueryParams     | map[string]string                                       | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | Query parameters in the request                                                                                                                                                   |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                         |                    |                                                                                                                                                                                   |
   |                 |                                                         |                    | None                                                                                                                                                                              |
   +-----------------+---------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0601__table12153312211:

.. table:: **Table 3** HttpMethodType

   ================= ============= ====================
   Constant          Default Value Description
   ================= ============= ====================
   HttpMethodGet     GET           HTTP GET request
   HttpMethodPut     POST          HTTP POST request
   HttpMethodPost    PUT           HTTP PUT request
   HttpMethodDelete  DELETE        HTTP DELETE request
   HttpMethodHead    HEAD          HTTP HEAD request
   HttpMethodOptions OPTIONS       HTTP OPTIONS request
   ================= ============= ====================

.. _obs_33_0601__table593654162113:

.. table:: **Table 4** SubResourceType

   +--------------------------+---------------+------------------------------------------------------------+
   | Constant                 | Default Value | Applicable API                                             |
   +==========================+===============+============================================================+
   | SubResourceStoragePolicy | storagePolicy | Sets or obtains bucket storage classes.                    |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceQuota         | quota         | Sets or obtains bucket quotas.                             |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceStorageInfo   | storageinfo   | Obtains bucket storage information.                        |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceLocation      | location      | Obtains bucket locations.                                  |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceAcl           | acl           | Sets or obtains bucket ACLs or object ACLs.                |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourcePolicy        | policy        | Sets, obtains, or deletes bucket policies.                 |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceCors          | cors          | Sets, obtains, or deletes bucket CORS configurations.      |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceVersioning    | versioning    | Sets or obtains bucket version statuses.                   |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceWebsite       | website       | Sets, obtains, or deletes bucket website configurations.   |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceLogging       | logging       | Sets or obtains bucket logging settings.                   |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceLifecycle     | lifecycle     | Sets, obtains, or deletes lifecycle rules of buckets.      |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceNotification  | notification  | Sets or obtains the notification configuration of buckets. |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceTagging       | tagging       | Sets, obtains, or deletes bucket tags.                     |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceDelete        | delete        | Batch deletes objects.                                     |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceVersions      | versions      | Lists versioning objects in buckets.                       |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceUploads       | uploads       | Lists or initializes multipart uploads in buckets.         |
   +--------------------------+---------------+------------------------------------------------------------+
   | SubResourceRestore       | restore       | Restores Cold objects.                                     |
   +--------------------------+---------------+------------------------------------------------------------+

Responses
---------

.. table:: **Table 5** List of returned results

   +-----------------------+---------------------------------------------------------------------+---------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                | Description                                                                           |
   +=======================+=====================================================================+=======================================================================================+
   | output                | \*\ :ref:`CreateSignedUrlOutput <obs_33_0601__table15448153632220>` | **Explanation:**                                                                      |
   |                       |                                                                     |                                                                                       |
   |                       |                                                                     | Returned results. For details, see :ref:`Table 6 <obs_33_0601__table15448153632220>`. |
   +-----------------------+---------------------------------------------------------------------+---------------------------------------------------------------------------------------+
   | err                   | error                                                               | **Explanation:**                                                                      |
   |                       |                                                                     |                                                                                       |
   |                       |                                                                     | Error messages returned by the API                                                    |
   +-----------------------+---------------------------------------------------------------------+---------------------------------------------------------------------------------------+

.. _obs_33_0601__table15448153632220:

.. table:: **Table 6** CreateSignedUrlOutput

   +----------------------------+-----------------------+-----------------------------------------------------------------+
   | Parameter                  | Type                  | Description                                                     |
   +============================+=======================+=================================================================+
   | SignedUrl                  | string                | **Explanation:**                                                |
   |                            |                       |                                                                 |
   |                            |                       | Signed URL                                                      |
   |                            |                       |                                                                 |
   |                            |                       | **Default value**:                                              |
   |                            |                       |                                                                 |
   |                            |                       | None                                                            |
   +----------------------------+-----------------------+-----------------------------------------------------------------+
   | ActualSignedRequestHeaders | http.Header           | **Explanation:**                                                |
   |                            |                       |                                                                 |
   |                            |                       | Actual headers in the request initiated by using the signed URL |
   |                            |                       |                                                                 |
   |                            |                       | **Default value**:                                              |
   |                            |                       |                                                                 |
   |                            |                       | None                                                            |
   +----------------------------+-----------------------+-----------------------------------------------------------------+

Code Example
------------

This example creates a signed URL for uploading an object.

::

   package main
   import (
       "fmt"
       "net/http"
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
       putObjectInput := &obs.CreateSignedUrlInput{}
       putObjectInput.Method = obs.HttpMethodPut
       putObjectInput.Bucket = "examplebucket"
       putObjectInput.Key = "example/objectname"
       putObjectInput.Expires = 3600
       // Create a signed URL for uploading an object.
       putObjectOutput, err := obsClient.CreateSignedUrl(putObjectInput)
       if err != nil {
           fmt.Println(err)
           return
       }
       fmt.Printf("SignedUrl:%s\n", putObjectOutput.SignedUrl)
       fmt.Printf("ActualSignedRequestHeaders:%v\n", putObjectOutput.ActualSignedRequestHeaders)
       // Call the signed URL.
       payload := strings.NewReader("hello OBS!")
       req, err := http.NewRequest("PUT", putObjectOutput.SignedUrl, payload)
       req.Header = putObjectOutput.ActualSignedRequestHeaders
       if err != nil {
           fmt.Printf("Create request error, errMsg: %s", err.Error())
           return
       }
       response, err := http.DefaultClient.Do(req)
       if err == nil {
           fmt.Printf("Use signed-url successful!\n")
           fmt.Printf("Status:%s,Etag:%s\n", response.Status, response.Header.Get("Etag"))
           return
       }
       fmt.Printf("Use signed-url successful!\n")
       fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
       fmt.Println(err)
   }

This example creates a signed URL for downloading an object.

::

   package main
   import (
       "fmt"
       "net/http"
       "os"
       "obs-sdk-go/obs"
   )
   func main() {
       // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
       // Obtain an AK/SK pair on the management console.
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
       getObjectInput := &obs.CreateSignedUrlInput{}
       getObjectInput.Method = obs.HttpMethodGet
       getObjectInput.Bucket = "examplebucket"
       getObjectInput.Key = "example/objectname"
       getObjectInput.Expires = 3600
       // Create a signed URL for downloading an object.
       getObjectOutput, err := obsClient.CreateSignedUrl(getObjectInput)
       if err != nil {
           fmt.Println(err)
           return
       }
       fmt.Printf("SignedUrl:%s\n", getObjectOutput.SignedUrl)
       fmt.Printf("ActualSignedRequestHeaders:%v\n", getObjectOutput.ActualSignedRequestHeaders)
       // Call the signed URL.
       req, err := http.NewRequest("GET", getObjectOutput.SignedUrl, nil)
       req.Header = getObjectOutput.ActualSignedRequestHeaders
       if err != nil {
           fmt.Printf("Create request error, errMsg: %s", err.Error())
           return
       }
       response, err := http.DefaultClient.Do(req)
       if err == nil {
           fmt.Printf("Use signed-url successful!\n")
           fmt.Printf("Status:%s,Etag:%s\n", response.Status, response.Header.Get("Etag"))
           p := make([]byte, 1024)
           var readErr error
           var readCount int
           // Read the object content.
           for {
               readCount, readErr = response.Body.Read(p)
               if readCount > 0 {
                   fmt.Printf("%s", p[:readCount])
               }
               if readErr != nil {
                   break
               }
           }
           return
       }
       fmt.Printf("Use signed-url successful!\n")
       fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
       fmt.Println(err)
   }

This example creates a signed URL for deleting an object.

::

   package main
   import (
       "fmt"
       "net/http"
       "os"
       "obs-sdk-go/obs"
   )
   func main() {
       // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
       // Obtain an AK/SK pair on the management console.
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
       // Create a signed URL for deleting an object.
       deleteObjectInput := &obs.CreateSignedUrlInput{}
       deleteObjectInput.Method = obs.HttpMethodDelete
       deleteObjectInput.Bucket = "examplebucket"
       deleteObjectInput.Key = "example/objectname"
       deleteObjectInput.Expires = 3600
       deleteObjectOutput, err := obsClient.CreateSignedUrl(deleteObjectInput)
       if err != nil {
           fmt.Println(err)
           return
       }
       fmt.Printf("SignedUrl:%s\n", deleteObjectOutput.SignedUrl)
       fmt.Printf("ActualSignedRequestHeaders:%v\n", deleteObjectOutput.ActualSignedRequestHeaders)
       // Call the signed URL.
       req, err := http.NewRequest("DELETE", deleteObjectOutput.SignedUrl, nil)
       req.Header = deleteObjectOutput.ActualSignedRequestHeaders
       if err != nil {
           fmt.Printf("Create request error, errMsg: %s", err.Error())
           return
       }
       response, err := http.DefaultClient.Do(req)
       if err == nil {
           fmt.Printf("Use signed-url successful!\n")
           fmt.Printf("Status:%s\n", response.Status)
           return
       }
       fmt.Printf("Use signed-url successful!\n")
       fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
       fmt.Println(err)
   }
