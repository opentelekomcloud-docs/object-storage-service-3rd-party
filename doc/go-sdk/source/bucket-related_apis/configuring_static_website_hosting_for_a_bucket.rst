:original_name: obs_33_0426.html

.. _obs_33_0426:

Configuring Static Website Hosting for a Bucket
===============================================

Function
--------

You can host static website resources such as HTML web pages, flash files, or audio and video files in an OBS bucket, so that you can access these hosted resources using the bucket's website endpoint. Typical use cases include:

-  Redirecting all requests to another website
-  Redirecting specific requests

This API configures static website hosting for a bucket.

Restrictions
------------

-  Periods (.) should be avoided in the target bucket name, or there may be certificate verification failures on the client when you use HTTPS for access.
-  The request body of the website configuration cannot exceed 10 KB.
-  To configure static website hosting for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketWebsite** in IAM or **PutBucketWebsite** in a bucket policy).

Method
------

**func** (obsClient ObsClient) SetBucketWebsiteConfiguration(input \*\ :ref:`SetBucketWebsiteConfigurationInput <obs_33_0426__table14455523>`) (output \*\ :ref:`BaseModel <obs_33_0426__table1201244276>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+----------------------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                                       | Mandatory (Yes/No) | Description                                                                                                            |
   +=================+============================================================================+====================+========================================================================================================================+
   | input           | \*\ :ref:`SetBucketWebsiteConfigurationInput <obs_33_0426__table14455523>` | Yes                | **Explanation:**                                                                                                       |
   |                 |                                                                            |                    |                                                                                                                        |
   |                 |                                                                            |                    | Input parameters for configuring static website hosting. For details, see :ref:`Table 2 <obs_33_0426__table14455523>`. |
   +-----------------+----------------------------------------------------------------------------+--------------------+------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0426__table14455523:

.. table:: **Table 2** SetBucketWebsiteConfigurationInput

   +-----------------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                          | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=======================+===============================================================+====================+===================================================================================================================================================================================+
   | Bucket                | string                                                        | Yes                | **Explanation:**                                                                                                                                                                  |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | Bucket name                                                                                                                                                                       |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | **Restrictions:**                                                                                                                                                                 |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                       |                                                               |                    | -  A bucket name:                                                                                                                                                                 |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                       |                                                               |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                       |                                                               |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                       |                                                               |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                       |                                                               |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                         |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | **Value range**:                                                                                                                                                                  |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | The value must contain 3 to 63 characters.                                                                                                                                        |
   +-----------------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RedirectAllRequestsTo | :ref:`RedirectAllRequestTo <obs_33_0426__table1630621572518>` | No                 | **Explanation:**                                                                                                                                                                  |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | Redirection rules for all requests. For details, see :ref:`Table 3 <obs_33_0426__table1630621572518>`.                                                                            |
   +-----------------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IndexDocument         | :ref:`IndexDocument <obs_33_0426__table179962100303>`         | No                 | **Explanation:**                                                                                                                                                                  |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | Default page configuration. For details, see :ref:`Table 4 <obs_33_0426__table179962100303>`.                                                                                     |
   +-----------------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ErrorDocument         | :ref:`ErrorDocument <obs_33_0426__table1292634533216>`        | No                 | **Explanation:**                                                                                                                                                                  |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | Error page configuration. For details, see :ref:`Table 5 <obs_33_0426__table1292634533216>`.                                                                                      |
   +-----------------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RoutingRules          | []\ :ref:`RoutingRule <obs_33_0426__table4262125213320>`      | No                 | **Explanation:**                                                                                                                                                                  |
   |                       |                                                               |                    |                                                                                                                                                                                   |
   |                       |                                                               |                    | List of routing rules. For details, see :ref:`Table 6 <obs_33_0426__table4262125213320>`.                                                                                         |
   +-----------------------+---------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   -  **ErrorDocument**, **IndexDocument**, and **RoutingRules** must be used together and they cannot be used with **RedirectAllRequestsTo**.
   -  When **ErrorDocument**, **IndexDocument**, and **RoutingRules** are used together, **RoutingRules** can be left blank.
   -  You must specify either the three parameters (**ErrorDocument**, **IndexDocument**, and **RoutingRules**), or **RedirectAllRequestsTo**.

.. _obs_33_0426__table1630621572518:

.. table:: **Table 3** RedirectAllRequestsTo

   +-----------------+-----------------------------------------------------+-----------------------------------------------+------------------------------------------------------------------+
   | Parameter       | Type                                                | Mandatory (Yes/No)                            | Description                                                      |
   +=================+=====================================================+===============================================+==================================================================+
   | HostName        | string                                              | Yes if **RedirectAllRequestsTo** is specified | **Explanation:**                                                 |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | Host name used for redirection, for example, **www.example.com** |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | **Restrictions:**                                                |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | The host name must comply with the host name rules.              |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | **Default value**:                                               |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | None                                                             |
   +-----------------+-----------------------------------------------------+-----------------------------------------------+------------------------------------------------------------------+
   | Protocol        | :ref:`ProtocolType <obs_33_0426__table39087286412>` | No                                            | **Explanation:**                                                 |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | Protocol used for redirection                                    |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | **Value range**:                                                 |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | See :ref:`Table 9 <obs_33_0426__table39087286412>`.              |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | **Default value**:                                               |
   |                 |                                                     |                                               |                                                                  |
   |                 |                                                     |                                               | None                                                             |
   +-----------------+-----------------------------------------------------+-----------------------------------------------+------------------------------------------------------------------+

.. _obs_33_0426__table179962100303:

.. table:: **Table 4** IndexDocument

   +-----------------+-----------------+---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                    | Description                                                                                                                                                                                                                                         |
   +=================+=================+=======================================+=====================================================================================================================================================================================================================================================+
   | Suffix          | string          | Yes if **IndexDocument** is specified | **Explanation:**                                                                                                                                                                                                                                    |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | Suffix that is appended to the request for a directory. For example, if the suffix is **index.html** and you request **samplebucket/images/**, the returned data will be for the object named **images/index.html** in the bucket **samplebucket**. |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | **Value range**:                                                                                                                                                                                                                                    |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | This parameter can neither be left blank nor contain slashes (/).                                                                                                                                                                                   |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | **Default value**:                                                                                                                                                                                                                                  |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | None                                                                                                                                                                                                                                                |
   +-----------------+-----------------+---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0426__table1292634533216:

.. table:: **Table 5** ErrorDocument

   +-----------------+-----------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                   | Description                                                                                                               |
   +=================+=================+======================================+===========================================================================================================================+
   | Key             | string          | No if **ErrorDocument** is specified | **Explanation:**                                                                                                          |
   |                 |                 |                                      |                                                                                                                           |
   |                 |                 |                                      | Object name to use when a **4**\ *XX* error occurs. This parameter specifies the webpage to display when an error occurs. |
   |                 |                 |                                      |                                                                                                                           |
   |                 |                 |                                      | **Value range**:                                                                                                          |
   |                 |                 |                                      |                                                                                                                           |
   |                 |                 |                                      | The value must contain 1 to 1,024 characters.                                                                             |
   |                 |                 |                                      |                                                                                                                           |
   |                 |                 |                                      | **Default value**:                                                                                                        |
   |                 |                 |                                      |                                                                                                                           |
   |                 |                 |                                      | None                                                                                                                      |
   +-----------------+-----------------+--------------------------------------+---------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0426__table4262125213320:

.. table:: **Table 6** RoutingRule

   +-----------------+----------------------------------------------------+-------------------------------------+----------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                               | Mandatory (Yes/No)                  | Description                                                                                        |
   +=================+====================================================+=====================================+====================================================================================================+
   | Condition       | :ref:`Condition <obs_33_0426__table336864313514>`  | No                                  | **Explanation:**                                                                                   |
   |                 |                                                    |                                     |                                                                                                    |
   |                 |                                                    |                                     | Conditions that must be met for the specified redirect to apply                                    |
   |                 |                                                    |                                     |                                                                                                    |
   |                 |                                                    |                                     | **Value range**:                                                                                   |
   |                 |                                                    |                                     |                                                                                                    |
   |                 |                                                    |                                     | See :ref:`Table 7 <obs_33_0426__table336864313514>`.                                               |
   |                 |                                                    |                                     |                                                                                                    |
   |                 |                                                    |                                     | **Default value**:                                                                                 |
   |                 |                                                    |                                     |                                                                                                    |
   |                 |                                                    |                                     | None                                                                                               |
   +-----------------+----------------------------------------------------+-------------------------------------+----------------------------------------------------------------------------------------------------+
   | Redirect        | :ref:`Redirect <obs_33_0426__table12397124916367>` | Yes if **RoutingRule** is specified | **Explanation:**                                                                                   |
   |                 |                                                    |                                     |                                                                                                    |
   |                 |                                                    |                                     | Details about the redirection. For details, see :ref:`Table 8 <obs_33_0426__table12397124916367>`. |
   +-----------------+----------------------------------------------------+-------------------------------------+----------------------------------------------------------------------------------------------------+

.. _obs_33_0426__table336864313514:

.. table:: **Table 7** Condition

   +-----------------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                   | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                |
   +=============================+=================+====================+============================================================================================================================================================================================================================================+
   | KeyPrefixEquals             | string          | No                 | **Explanation:**                                                                                                                                                                                                                           |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | Object name prefix when the redirection is applied. When a request is sent for accessing an object, the redirection rule takes effect if the object name prefix matches the value specified for this parameter.                            |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | For example, to redirect the request for object **ExamplePage.html**, set the **KeyPrefixEquals** to **ExamplePage.html**.                                                                                                                 |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | **Restrictions:**                                                                                                                                                                                                                          |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | This parameter cannot be used together with **HttpErrorCodeReturnedEquals**.                                                                                                                                                               |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | **Value range**:                                                                                                                                                                                                                           |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                              |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | **Default value**:                                                                                                                                                                                                                         |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | None                                                                                                                                                                                                                                       |
   +-----------------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HttpErrorCodeReturnedEquals | string          | No                 | **Explanation:**                                                                                                                                                                                                                           |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | HTTP error codes when the redirection takes effect. The specified redirection is applied only when the error code returned equals the value specified for this parameter.                                                                  |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | For example, if you want to redirect requests to **NotFound.html** when HTTP error code 404 is returned, set **HttpErrorCodeReturnedEquals** to **404** in **Condition**, and set **ReplaceKeyWith** to **NotFound.html** in **Redirect**. |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | **Restrictions:**                                                                                                                                                                                                                          |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | This parameter cannot be used together with **KeyPrefixEquals**.                                                                                                                                                                           |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | **Default value**:                                                                                                                                                                                                                         |
   |                             |                 |                    |                                                                                                                                                                                                                                            |
   |                             |                 |                    | None                                                                                                                                                                                                                                       |
   +-----------------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0426__table12397124916367:

.. table:: **Table 8** Redirect

   +----------------------+-----------------------------------------------------+-----------------------------------+-----------------------------------------------------------------------+
   | Parameter            | Type                                                | Mandatory (Yes/No)                | Description                                                           |
   +======================+=====================================================+===================================+=======================================================================+
   | Protocol             | :ref:`ProtocolType <obs_33_0426__table39087286412>` | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | Protocol used for redirection                                         |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | **Value range**:                                                      |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | See :ref:`Table 9 <obs_33_0426__table39087286412>`.                   |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | **Default value**:                                                    |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | None                                                                  |
   +----------------------+-----------------------------------------------------+-----------------------------------+-----------------------------------------------------------------------+
   | HostName             | string                                              | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | Host name used for redirection                                        |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | **Default value**:                                                    |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | None                                                                  |
   +----------------------+-----------------------------------------------------+-----------------------------------+-----------------------------------------------------------------------+
   | ReplaceKeyPrefixWith | string                                              | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | Object name prefix used for redirection                               |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | **Value range**:                                                      |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | The value must contain 1 to 1,024 characters.                         |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | **Default value**:                                                    |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | None                                                                  |
   +----------------------+-----------------------------------------------------+-----------------------------------+-----------------------------------------------------------------------+
   | ReplaceKeyWith       | string                                              | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | Object name used for redirection                                      |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | **Restrictions:**                                                     |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | This parameter cannot be used together with **replaceKeyPrefixWith**. |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | **Value range**:                                                      |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | The value must contain 1 to 1,024 characters.                         |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | **Default value**:                                                    |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | None                                                                  |
   +----------------------+-----------------------------------------------------+-----------------------------------+-----------------------------------------------------------------------+
   | HttpRedirectCode     | string                                              | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | HTTP status code in the response to the redirect request.             |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | **Default value**:                                                    |
   |                      |                                                     |                                   |                                                                       |
   |                      |                                                     |                                   | None                                                                  |
   +----------------------+-----------------------------------------------------+-----------------------------------+-----------------------------------------------------------------------+

.. _obs_33_0426__table39087286412:

.. table:: **Table 9** ProtocolType

   +---------------+---------------+-------------------------------------------------+
   | Constant      | Default Value | Description                                     |
   +===============+===============+=================================================+
   | ProtocolHttp  | http          | HTTP protocol used for redirection              |
   +---------------+---------------+-------------------------------------------------+
   | ProtocolHttps | https         | HTTPS protocol used for the redirection request |
   +---------------+---------------+-------------------------------------------------+

Responses
---------

.. table:: **Table 10** List of returned results

   +-----------------------+-----------------------------------------------------+------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                        |
   +=======================+=====================================================+====================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0426__table1201244276>` | **Explanation:**                                                                   |
   |                       |                                                     |                                                                                    |
   |                       |                                                     | Returned results. For details, see :ref:`Table 11 <obs_33_0426__table1201244276>`. |
   +-----------------------+-----------------------------------------------------+------------------------------------------------------------------------------------+
   | err                   | error                                               | **Explanation:**                                                                   |
   |                       |                                                     |                                                                                    |
   |                       |                                                     | Error messages returned by the API                                                 |
   +-----------------------+-----------------------------------------------------+------------------------------------------------------------------------------------+

.. _obs_33_0426__table1201244276:

.. table:: **Table 11** BaseModel

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

This example configures static website hosting for bucket **examplebucket**.

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
       input := &obs.SetBucketWebsiteConfigurationInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify a default page (index.html as an example). This configuration indicates that when examplebucket/images/ is requested, the content of object images/index.html in bucket samplebucket will be returned.
       input.IndexDocument.Suffix = "index.html"
       // Specify an error page (error.html as an example).
       input.ErrorDocument.Key = "error.html"
       // Specify the list of request redirect rules.
       input.RoutingRules = []obs.RoutingRule{
           {Redirect: obs.Redirect{HostName: "www.a.com", Protocol: obs.ProtocolHttp, ReplaceKeyPrefixWith: "prefix", HttpRedirectCode: "304"}},
           {Redirect: obs.Redirect{HostName: "www.b.com", Protocol: obs.ProtocolHttps, ReplaceKeyWith: "replaceKey", HttpRedirectCode: "304"}},
       }
       // Configure static website hosting for the bucket.
       output, err := obsClient.SetBucketWebsiteConfiguration(input)
       if err == nil {
           fmt.Printf("Set bucket(%s)'s website successful!\n", input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Set bucket(%s)'s website fail!\n", input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
