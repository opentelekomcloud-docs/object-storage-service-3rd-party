:original_name: obs_33_0602.html

.. _obs_33_0602:

Creating Authentication Parameters for a Browser-based Upload
=============================================================

Function
--------

This API generates parameters for authentication. The parameters can be used to upload data through POST operations based on a browser.

.. note::

   There are two request parameters generated:

   -  **Policy**, which corresponds to the **policy** parameter in the form
   -  **Signature**, which corresponds to the **x-obs-signature** parameter in the form

Restrictions
------------

-  To upload an object, you must be the bucket owner or have the required permission (**obs:object:PutObject** in IAM or **PutObject** in a bucket policy).

Method
------

**func** (obsClient ObsClient) CreateBrowserBasedSignature(input \*\ :ref:`CreateBrowserBasedSignatureInput <obs_33_0602__table11587896166>`) (output \*\ :ref:`CreateBrowserBasedSignatureOutput <obs_33_0602__table102058592163>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                                        | Mandatory (Yes/No) | Description                                                                                                                                          |
   +=================+=============================================================================+====================+======================================================================================================================================================+
   | input           | \*\ :ref:`CreateBrowserBasedSignatureInput <obs_33_0602__table11587896166>` | Yes                | **Explanation:**                                                                                                                                     |
   |                 |                                                                             |                    |                                                                                                                                                      |
   |                 |                                                                             |                    | Input parameters for creating authentication parameters for a browser-based upload. For details, see :ref:`Table 2 <obs_33_0602__table11587896166>`. |
   +-----------------+-----------------------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0602__table11587896166:

.. table:: **Table 2** CreateBrowserBasedSignatureInput

   +-----------------+-------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type              | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+===================+====================+===================================================================================================================================================================================+
   | Bucket          | string            | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | Bucket name                                                                                                                                                                       |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                   |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                   |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                   |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                   |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                   |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | **Default value**:                                                                                                                                                                |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | None                                                                                                                                                                              |
   +-----------------+-------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key             | string            | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                             |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | **Value range**:                                                                                                                                                                  |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | **Default value**:                                                                                                                                                                |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | None                                                                                                                                                                              |
   +-----------------+-------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Expires         | int               | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | Expiration time of authentication for a browser-based upload                                                                                                                      |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | **Value range**:                                                                                                                                                                  |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | 0 to (2\ :sup:`63` - 1), in seconds                                                                                                                                               |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | **Default value**:                                                                                                                                                                |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | 300                                                                                                                                                                               |
   +-----------------+-------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | FormParams      | map[string]string | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | Parameters of a browser-based upload, not including **key**, **policy**, and **signature**.                                                                                       |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | **Value range**:                                                                                                                                                                  |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | **acl**, **cache-control**, **content-type**, **content-disposition**, **content-encoding**, and **expires**                                                                      |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | **Default value**:                                                                                                                                                                |
   |                 |                   |                    |                                                                                                                                                                                   |
   |                 |                   |                    | None                                                                                                                                                                              |
   +-----------------+-------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** List of returned results

   +-----------------------+-------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                          | Description                                                                         |
   +=======================+===============================================================================+=====================================================================================+
   | output                | \*\ :ref:`CreateBrowserBasedSignatureOutput <obs_33_0602__table102058592163>` | **Explanation:**                                                                    |
   |                       |                                                                               |                                                                                     |
   |                       |                                                                               | Returned results. For details, see :ref:`Table 4 <obs_33_0602__table102058592163>`. |
   +-----------------------+-------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+
   | err                   | error                                                                         | **Explanation:**                                                                    |
   |                       |                                                                               |                                                                                     |
   |                       |                                                                               | Error messages returned by the API                                                  |
   +-----------------------+-------------------------------------------------------------------------------+-------------------------------------------------------------------------------------+

.. _obs_33_0602__table102058592163:

.. table:: **Table 4** CreateBrowserBasedSignatureOutput

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                               |
   +=======================+=======================+===========================================================================================================================================================================================================+
   | OriginPolicy          | string                | **Explanation:**                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | **policy** not encoded by Base64. This parameter can only be used for verification.                                                                                                                       |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | Example: **{"expiration":"2023-09-12T12:52:59Z","conditions":[{"content-type":"text/plain"},{"bucket":"examplebucket"},{"key":"example/objectname"},]}"**                                                 |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | **Default value**:                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | None                                                                                                                                                                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Policy                | string                | **Explanation:**                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | Base64-encoded value of **policy** in the form                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | Example: **eyJleHBpcmF0aW9uIjoiMjAyMy0wOS0xMlQxMjo1Mjo1OVoiLCJjb25kaXRpb25zIjpbeyJjb250ZW50LXR5cGUiOiJ0ZXh0L3BsYWluIn0seyJidWNrZXQiOiJleGFtcGxlYnVja2V0In0seyJrZXkiOiJleGFtcGxlL29iamVjdG5hbWUifSxdfQ==** |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | **Default value**:                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | None                                                                                                                                                                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Signature             | string                | **Explanation:**                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | **signature** in the form                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | Example: **g0jQr4v9VWd1Q2FOFDG6LGfV9Cw=**                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | **Default value**:                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | None                                                                                                                                                                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Example
------------

This example creates a signed URL for uploading an object using POST.

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
       // Create a signed URL for uploading an object.
       input := &obs.CreateBrowserBasedSignatureInput{}
       input.Bucket = "examplebucket"
       input.Key = "example/objectname"
       input.FormParams = map[string]string{
           "content-type": "text/plain",
           "success_action_redirect": "https://www.example.com",
           "x-obs-acl": "public-read",
       }
       output, err := obsClient.CreateBrowserBasedSignature(input)
   if err == nil {
           fmt.Printf("Policy:%s\n", output.Policy)
           fmt.Printf("Signature:%s\n", output.Signature)
       } else {
           fmt.Println(err)
           return
       }
       requestBody := &bytes.Buffer{}
       writer := multipart.NewWriter(requestBody)
       writer.WriteField("key", input.Key)
       writer.WriteField("AccessKeyId", ak)
       writer.WriteField("policy", output.Policy)
       writer.WriteField("signature", output.Signature)
       writer.WriteField("success_action_redirect", "https://www.example.com")
       // writer.WriteField("token", obs.WithSecurityToken(securityToken))
       writer.WriteField("Content-Type", "text/plain")
       formFile, _ := writer.CreateFormFile("file", "filename")
       io.Copy(formFile, strings.NewReader("hello OBS!"))
       writer.Close()
       url := "https://" + input.Bucket + "." + strings.Replace(endPoint, "https://", "", 1)
       request, err := http.NewRequest("POST", url, requestBody)
       if err != nil {
           fmt.Println(err)
           return
       }
       request.Header.Set("Content-Type", writer.FormDataContentType())
       client := &http.Client{}
       response, err := client.Do(request)
       if err != nil {
           fmt.Println(err)
           return
       }
       defer response.Body.Close()
       if err == nil {
           fmt.Printf("Use signed-url successful!\n")
           fmt.Printf("Status:%s,Etag:%s\n", response.Status, response.Header.Get("Etag"))
           return
       }
       fmt.Printf("Use signed-url successful!\n")
       fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
       fmt.Println(err)
   }
