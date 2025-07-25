:original_name: obs_33_0431.html

.. _obs_33_0431:

Configuring CORS for a Bucket
=============================

Function
--------

Cross-origin resource sharing (CORS) is a browser-standard mechanism defined by the World Wide Web Consortium (W3C). It allows a web client in one origin to interact with resources in another one. For general web page requests, website scripts and contents in one origin cannot interact with those in another because of Same Origin Policies (SOPs). OBS supports CORS rules that allow the resources in OBS to be requested from other origins.

This API configures CORS for a bucket.

Restrictions
------------

-  To configure CORS for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketCORS** in IAM or **PutBucketCORS** in a bucket policy).

Method
------

**func** (obsClient ObsClient) SetBucketCors(input \*\ :ref:`SetBucketCorsInput <obs_33_0431__table14455523>`) (output \*\ :ref:`BaseModel <obs_33_0431__table44411618181811>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+------------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                       | Mandatory (Yes/No) | Description                                                                                                       |
   +=================+============================================================+====================+===================================================================================================================+
   | input           | \*\ :ref:`SetBucketCorsInput <obs_33_0431__table14455523>` | Yes                | **Explanation:**                                                                                                  |
   |                 |                                                            |                    |                                                                                                                   |
   |                 |                                                            |                    | Input parameters for configuring CORS for a bucket. For details, see :ref:`Table 2 <obs_33_0431__table14455523>`. |
   +-----------------+------------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0431__table14455523:

.. table:: **Table 2** SetBucketCorsInput

   +-----------------+--------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                   | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+========================================================+====================+===================================================================================================================================================================================+
   | Bucket          | string                                                 | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    | Bucket name                                                                                                                                                                       |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                        |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                        |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                        |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                        |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                        |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    | **Default value**:                                                                                                                                                                |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    | None                                                                                                                                                                              |
   +-----------------+--------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CorsRules       | []\ :ref:`CorsRule <obs_33_0431__table17941121314177>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    | CORS rule list of the bucket. For details, see :ref:`Table 3 <obs_33_0431__table17941121314177>`.                                                                                 |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                        |                    |                                                                                                                                                                                   |
   |                 |                                                        |                    | A list can have a maximum of 100 CORS rules.                                                                                                                                      |
   +-----------------+--------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0431__table17941121314177:

.. table:: **Table 3** CorsRule

   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                 | Description                                                                                                                                                                                                                                                                                                  |
   +=================+=================+====================================+==============================================================================================================================================================================================================================================================================================================+
   | ID              | string          | No if used as a request parameter  | **Explanation:**                                                                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | CORS rule ID                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Value range**:                                                                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | The value must contain 1 to 255 characters.                                                                                                                                                                                                                                                                  |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Default value**:                                                                                                                                                                                                                                                                                           |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | None                                                                                                                                                                                                                                                                                                         |
   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AllowedMethod   | []string        | Yes if used as a request parameter | **Explanation:**                                                                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | The allowed HTTP methods cross-origin request, same as the operation types of buckets and objects.                                                                                                                                                                                                           |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Value range**:                                                                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | The following HTTP methods are supported:                                                                                                                                                                                                                                                                    |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | -  GET                                                                                                                                                                                                                                                                                                       |
   |                 |                 |                                    | -  PUT                                                                                                                                                                                                                                                                                                       |
   |                 |                 |                                    | -  HEAD                                                                                                                                                                                                                                                                                                      |
   |                 |                 |                                    | -  POST                                                                                                                                                                                                                                                                                                      |
   |                 |                 |                                    | -  DELETE                                                                                                                                                                                                                                                                                                    |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Default value**:                                                                                                                                                                                                                                                                                           |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | None                                                                                                                                                                                                                                                                                                         |
   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AllowedOrigin   | []string        | Yes if used as a request parameter | **Explanation:**                                                                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | The origin from which the requests can access the bucket.                                                                                                                                                                                                                                                    |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Restrictions:**                                                                                                                                                                                                                                                                                            |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | Domain name of the origin. Each origin can contain only one wildcard character (``*``), for example, **https://*.vbs.example.com**.                                                                                                                                                                          |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Default value**:                                                                                                                                                                                                                                                                                           |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | None                                                                                                                                                                                                                                                                                                         |
   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | AllowedHeader   | []string        | No if used as a request parameter  | **Explanation:**                                                                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | The allowed headers for cross-origin requests. Only CORS requests matching the allowed headers are valid.                                                                                                                                                                                                    |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Restrictions:**                                                                                                                                                                                                                                                                                            |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | Each header can contain only one wildcard character (``*``). Spaces, ampersands (&), colons (:), and less-than signs (<) are not allowed.                                                                                                                                                                    |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Default value**:                                                                                                                                                                                                                                                                                           |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | None                                                                                                                                                                                                                                                                                                         |
   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MaxAgeSeconds   | int             | No if used as a request parameter  | **Explanation:**                                                                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | Time your client can cache the response for a cross-origin request                                                                                                                                                                                                                                           |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Restrictions:**                                                                                                                                                                                                                                                                                            |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | Each CORS rule can specify only one value for **MaxAgeSeconds**.                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Value range**:                                                                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | 0 to (2\ :sup:`31` - 1), in seconds                                                                                                                                                                                                                                                                          |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Default value**:                                                                                                                                                                                                                                                                                           |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | 100                                                                                                                                                                                                                                                                                                          |
   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ExposeHeader    | []string        | No if used as a request parameter  | **Explanation:**                                                                                                                                                                                                                                                                                             |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | The CORS-allowed additional headers in the response. These headers provide additional information to clients. By default, your browser can only access headers **Content-Length** and **Content-Type**. If your browser needs to access other headers, add them to a list of the allowed additional headers. |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Restrictions:**                                                                                                                                                                                                                                                                                            |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | Spaces, wildcard characters (``*``), ampersands (&), colons (:), and less-than signs (<) are not allowed.                                                                                                                                                                                                    |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | **Default value**:                                                                                                                                                                                                                                                                                           |
   |                 |                 |                                    |                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                                    | None                                                                                                                                                                                                                                                                                                         |
   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 4** List of returned results

   +-----------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------+
   | Parameter             | Type                                                    | Description                                                                           |
   +=======================+=========================================================+=======================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0431__table44411618181811>` | **Explanation:**                                                                      |
   |                       |                                                         |                                                                                       |
   |                       |                                                         | Returned results. For details, see :ref:`Table 5 <obs_33_0431__table44411618181811>`. |
   +-----------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------+
   | err                   | error                                                   | **Explanation:**                                                                      |
   |                       |                                                         |                                                                                       |
   |                       |                                                         | Error messages returned by the API                                                    |
   +-----------------------+---------------------------------------------------------+---------------------------------------------------------------------------------------+

.. _obs_33_0431__table44411618181811:

.. table:: **Table 5** BaseModel

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

Code Examples
-------------

This example configures CORS rules for bucket **examplebucket**.

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
       securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint, obs.WithSecurityToken(securityToken))
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.SetBucketCorsInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify CORS rules.
       input.CorsRules = []obs.CorsRule{
           {
               ID:            "rule1",
               AllowedOrigin: []string{"http://www.a.com", "http://www.b.com"},
               AllowedMethod: []string{"GET", "PUT"},
               AllowedHeader: []string{"header1", "header2"},
               MaxAgeSeconds: 1000,
               ExposeHeader:  []string{"obs-1", "obs-2"},
           },
           {
               ID:            "rule2",
               AllowedOrigin: []string{"http://www.c.com", "http://www.d.com"},
               AllowedMethod: []string{"GET", "POST"},
               AllowedHeader: []string{"header3", "header4"},
               MaxAgeSeconds: 1000,
           },
       }
       // Configure CORS for the bucket.
       output, err := obsClient.SetBucketCors(input)
       if err == nil {
           fmt.Printf("Set bucket(%s) CORS configuration successful!\n", input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Set bucket(%s) CORS configuration fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
