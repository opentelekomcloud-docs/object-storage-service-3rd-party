:original_name: obs_21_1603.html

.. _obs_21_1603:

Configuring Static Website Hosting
==================================

Function
--------

You can host static website resources such as HTML web pages, flash files, or audio and video files in an OBS bucket, so that you can provide these hosted resources using the bucket's website endpoint to end users. Typical use cases include:

-  Redirecting all requests to another website
-  Redirecting specific requests to another website

This API configures static website hosting for a bucket.

Restrictions
------------

-  Periods (.) should be avoided in the target bucket name, or there may be certificate verification failures on the client when you use HTTPS for access.
-  The request body of the website configuration cannot exceed 10 KB.
-  To configure static website hosting for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketWebsite** in IAM or **PutBucketWebsite** in a bucket policy).

Method
------

obsClient.setBucketWebsite(final :ref:`SetBucketWebsiteRequest <obs_21_1603__table14455523>` :ref:`request <obs_21_1603__table1210700>`)

Request Parameters
------------------

.. _obs_21_1603__table1210700:

.. table:: **Table 1** List of request parameters

   +-----------------+-------------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                        | Mandatory (Yes/No) | Description                                                                                                       |
   +=================+=============================================================+====================+===================================================================================================================+
   | request         | :ref:`SetBucketWebsiteRequest <obs_21_1603__table14455523>` | Yes                | **Explanation:**                                                                                                  |
   |                 |                                                             |                    |                                                                                                                   |
   |                 |                                                             |                    | Request parameters for configuring website hosting. For details, see :ref:`Table 2 <obs_21_1603__table14455523>`. |
   +-----------------+-------------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1603__table14455523:

.. table:: **Table 2** SetBucketWebsiteRequest

   +-----------------+----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                           | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+================================================================+====================+===================================================================================================================================================================================+
   | bucketName      | String                                                         | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                                |                    |                                                                                                                                                                                   |
   |                 |                                                                |                    | Bucket name.                                                                                                                                                                      |
   |                 |                                                                |                    |                                                                                                                                                                                   |
   |                 |                                                                |                    | **Restrictions:**                                                                                                                                                                 |
   |                 |                                                                |                    |                                                                                                                                                                                   |
   |                 |                                                                |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                 |                                                                |                    | -  A bucket name:                                                                                                                                                                 |
   |                 |                                                                |                    |                                                                                                                                                                                   |
   |                 |                                                                |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                 |                                                                |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                 |                                                                |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                 |                                                                |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                 |                                                                |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                                                                |                    |                                                                                                                                                                                   |
   |                 |                                                                |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                                                                |                    |                                                                                                                                                                                   |
   |                 |                                                                |                    | **Value range**:                                                                                                                                                                  |
   |                 |                                                                |                    |                                                                                                                                                                                   |
   |                 |                                                                |                    | The value must contain 3 to 63 characters.                                                                                                                                        |
   +-----------------+----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | websiteConfig   | :ref:`WebsiteConfiguration <obs_21_1603__table18752173983114>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                                                                |                    |                                                                                                                                                                                   |
   |                 |                                                                |                    | Static website hosting configurations. For details, see :ref:`Table 3 <obs_21_1603__table18752173983114>`.                                                                        |
   +-----------------+----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1603__table18752173983114:

.. table:: **Table 3** WebsiteConfiguration

   +-----------------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                        | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                         |
   +=======================+=============================================================+====================+=====================================================================================================================================================================================================================================================+
   | suffix                | String                                                      | No                 | **Explanation:**                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | Suffix that is appended to the request for a directory. For example, if the suffix is **index.html** and you request **samplebucket/images/**, the returned data will be for the object named **images/index.html** in the bucket **samplebucket**. |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Restrictions:**                                                                                                                                                                                                                                   |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | -  **key**, **suffix**, and **routeRules** must be used together and they cannot be used with **redirectAllRequestsTo**.                                                                                                                            |
   |                       |                                                             |                    | -  When **key**, **suffix**, and **routeRules** are used together, **routeRules** can be left blank.                                                                                                                                                |
   |                       |                                                             |                    | -  If you configure **key**, **suffix**, and **routeRules**, they must not be all left blank.                                                                                                                                                       |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Value range**:                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | This parameter can neither be left blank nor contain slashes (/).                                                                                                                                                                                   |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Default value**:                                                                                                                                                                                                                                  |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | None                                                                                                                                                                                                                                                |
   +-----------------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | key                   | String                                                      | No                 | **Explanation:**                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | Object name to use when a **4**\ *XX* error occurs. This parameter specifies the web page to display when an error occurs.                                                                                                                          |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Restrictions:**                                                                                                                                                                                                                                   |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | -  **key**, **suffix**, and **routeRules** must be used together and they cannot be used with **redirectAllRequestsTo**.                                                                                                                            |
   |                       |                                                             |                    | -  When **key**, **suffix**, and **routeRules** are used together, **routeRules** can be left blank.                                                                                                                                                |
   |                       |                                                             |                    | -  If you configure **key**, **suffix**, and **routeRules**, they must not be all left blank.                                                                                                                                                       |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Value range**:                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                       |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Default value**:                                                                                                                                                                                                                                  |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | None                                                                                                                                                                                                                                                |
   +-----------------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | routeRules            | List<:ref:`RouteRule <obs_21_1603__table4262125213320>`>    | No                 | **Explanation:**                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | List of routing rules. For details, see :ref:`Table 6 <obs_21_1603__table4262125213320>`.                                                                                                                                                           |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Restrictions:**                                                                                                                                                                                                                                   |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | -  **key**, **suffix**, and **routeRules** must be used together and they cannot be used with **redirectAllRequestsTo**.                                                                                                                            |
   |                       |                                                             |                    | -  When **key**, **suffix**, and **routeRules** are used together, **routeRules** can be left blank.                                                                                                                                                |
   |                       |                                                             |                    | -  If you configure **key**, **suffix**, and **routeRules**, they must not be all left blank.                                                                                                                                                       |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Default value**:                                                                                                                                                                                                                                  |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | None                                                                                                                                                                                                                                                |
   +-----------------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | redirectAllRequestsTo | :ref:`RedirectAllRequest <obs_21_1603__table1630621572518>` | No                 | **Explanation:**                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | Redirection rules for all requests. For details, see :ref:`Table 4 <obs_21_1603__table1630621572518>`.                                                                                                                                              |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Restrictions:**                                                                                                                                                                                                                                   |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | -  **key**, **suffix**, and **routeRules** must be used together and they cannot be used with **redirectAllRequestsTo**.                                                                                                                            |
   |                       |                                                             |                    | -  If you configure **redirectAllRequestsTo**, it must not be left blank.                                                                                                                                                                           |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Default value**:                                                                                                                                                                                                                                  |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | None                                                                                                                                                                                                                                                |
   +-----------------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1603__table1630621572518:

.. table:: **Table 4** RedirectAllRequest

   +-----------------+------------------------------------------------------+--------------------+-------------------------------------------------------------------+
   | Parameter       | Type                                                 | Mandatory (Yes/No) | Description                                                       |
   +=================+======================================================+====================+===================================================================+
   | hostName        | String                                               | Yes                | **Explanation:**                                                  |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | Host name used for redirection, for example, **www.example.com**. |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | **Restrictions:**                                                 |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | The host name must comply with the host name rules.               |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | **Default value**:                                                |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | None                                                              |
   +-----------------+------------------------------------------------------+--------------------+-------------------------------------------------------------------+
   | protocol        | :ref:`ProtocolEnum <obs_21_1603__table155207227288>` | No                 | **Explanation:**                                                  |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | Protocol used for redirection.                                    |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | **Value range**:                                                  |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | See :ref:`Table 5 <obs_21_1603__table155207227288>`.              |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | **Default value**:                                                |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | None                                                              |
   +-----------------+------------------------------------------------------+--------------------+-------------------------------------------------------------------+

.. _obs_21_1603__table155207227288:

.. table:: **Table 5** ProtocolEnum

   ======== ============= ====================================
   Constant Default Value Description
   ======== ============= ====================================
   HTTP     http          HTTP protocol used for redirection.
   HTTPS    https         HTTPS protocol used for redirection.
   ======== ============= ====================================

.. _obs_21_1603__table4262125213320:

.. table:: **Table 6** RouteRule

   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                       | Mandatory (Yes/No) | Description                                                                                         |
   +=================+============================================================+====================+=====================================================================================================+
   | condition       | :ref:`RouteRuleCondition <obs_21_1603__table336864313514>` | No                 | **Explanation:**                                                                                    |
   |                 |                                                            |                    |                                                                                                     |
   |                 |                                                            |                    | Conditions of a redirection rule. For details, see :ref:`Table 7 <obs_21_1603__table336864313514>`. |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+
   | redirect        | :ref:`Redirect <obs_21_1603__table12397124916367>`         | Yes                | **Explanation:**                                                                                    |
   |                 |                                                            |                    |                                                                                                     |
   |                 |                                                            |                    | Details about the redirection. For details, see :ref:`Table 8 <obs_21_1603__table12397124916367>`.  |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+

.. _obs_21_1603__table336864313514:

.. table:: **Table 7** RouteRuleCondition

   +-----------------------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                   | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                             |
   +=============================+=================+====================+=========================================================================================================================================================================================================================================================+
   | keyPrefixEquals             | String          | No                 | **Explanation:**                                                                                                                                                                                                                                        |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | Object name prefix for the redirection to take effect. If the name prefix of the requested object is the same as the value specified for this parameter, the redirection rule takes effect.                                                             |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | For example, to redirect the requests for the object **ExamplePage.html**, set **keyPrefixEquals** to **ExamplePage.html**.                                                                                                                             |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | **Restrictions:**                                                                                                                                                                                                                                       |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | This parameter cannot be used together with **httpErrorCodeReturnedEquals**.                                                                                                                                                                            |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | **Value range**:                                                                                                                                                                                                                                        |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                           |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | **Default value**:                                                                                                                                                                                                                                      |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | None                                                                                                                                                                                                                                                    |
   +-----------------------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | httpErrorCodeReturnedEquals | String          | No                 | **Explanation:**                                                                                                                                                                                                                                        |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | HTTP error code for the redirection to take effect. If there is an error, and the error code returned is the same as the value specified for this parameter, the redirection rule takes effect.                                                         |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | For example, if you want to redirect requests to **NotFound.html** when HTTP error code **404** is returned, set **httpErrorCodeReturnedEquals** to **404** in **RouteRuleCondition**, and set **replaceKeyWith** to **NotFound.html** in **Redirect**. |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | **Restrictions:**                                                                                                                                                                                                                                       |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | This parameter cannot be used together with **keyPrefixEquals**.                                                                                                                                                                                        |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | **Default value**:                                                                                                                                                                                                                                      |
   |                             |                 |                    |                                                                                                                                                                                                                                                         |
   |                             |                 |                    | None                                                                                                                                                                                                                                                    |
   +-----------------------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1603__table12397124916367:

.. table:: **Table 8** Redirect

   +----------------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------+
   | Parameter            | Type                                                 | Mandatory (Yes/No) | Description                                                           |
   +======================+======================================================+====================+=======================================================================+
   | Protocol             | :ref:`ProtocolEnum <obs_21_1603__table155207227288>` | No                 | **Explanation:**                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | Protocol used for redirection.                                        |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Value range**:                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | See :ref:`Table 5 <obs_21_1603__table155207227288>`.                  |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Default value**:                                                    |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | None                                                                  |
   +----------------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------+
   | hostName             | String                                               | No                 | **Explanation:**                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | Host name used for redirection.                                       |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Default value**:                                                    |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | None                                                                  |
   +----------------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------+
   | replaceKeyPrefixWith | String                                               | No                 | **Explanation:**                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | Object name prefix used in the redirection request.                   |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Restrictions:**                                                     |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | This parameter cannot be used together with **replaceKeyWith**.       |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Value range**:                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | The value must contain 1 to 1,024 characters.                         |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Default value**:                                                    |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | None                                                                  |
   +----------------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------+
   | replaceKeyWith       | String                                               | No                 | **Explanation:**                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | Object name used in the redirection request.                          |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Restrictions:**                                                     |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | This parameter cannot be used together with **replaceKeyPrefixWith**. |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Value range**:                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | The value must contain 1 to 1,024 characters.                         |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Default value**:                                                    |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | None                                                                  |
   +----------------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------+
   | httpRedirectCode     | String                                               | No                 | **Explanation:**                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | HTTP status code in the response to the redirect request.             |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Default value**:                                                    |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | None                                                                  |
   +----------------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------+

Responses
---------

.. table:: **Table 9** Common response headers

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
   |                       |                       | HTTP response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Example: Configuring the Default Home Page and Error Pages
---------------------------------------------------------------

This example configures the default homepage and error pages for bucket **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.WebsiteConfiguration;
   public class SetBucketWebsite001
   {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           String securityToken = System.getenv("SECURITY_TOKEN");
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
               // Sample code is as follows:
               WebsiteConfiguration config = new WebsiteConfiguration();
               // Configure the default homepage.
               config.setSuffix("index.html");
               // Configure the error pages.
               config.setKey("error.html");
               obsClient.setBucketWebsite("examplebucket", config);
               System.out.println("setBucketWebsite successfully");
           } catch (ObsException e) {
               System.out.println("setBucketWebsite failed");
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
               System.out.println("setBucketWebsite failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Configuring a Redirection Rule
--------------------------------------------

This example configures a redirection rule for bucket **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.ProtocolEnum;
   import com.obs.services.model.Redirect;
   import com.obs.services.model.RouteRule;
   import com.obs.services.model.RouteRuleCondition;
   import com.obs.services.model.WebsiteConfiguration;
   public class SetBucketWebsite002
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
               // Sample code is as follows:
               WebsiteConfiguration config = new WebsiteConfiguration();
               // Configure the default homepage.
               config.setSuffix("index.html");
               // Configure the error pages.
               config.setKey("error.html");
               RouteRule rule = new RouteRule();
               Redirect r = new Redirect();
               r.setHostName("www.example.com");
               r.setHttpRedirectCode("305");
               r.setRedirectProtocol(ProtocolEnum.HTTP);
               r.setReplaceKeyPrefixWith("replacekeyprefix");
               rule.setRedirect(r);
               RouteRuleCondition condition = new RouteRuleCondition();
               condition.setHttpErrorCodeReturnedEquals("404");
               condition.setKeyPrefixEquals("keyprefix");
               rule.setCondition(condition);
               config.getRouteRules().add(rule);
               obsClient.setBucketWebsite("examplebucket", config);
               System.out.println("setBucketWebsite successfully");
           } catch (ObsException e) {
               System.out.println("setBucketWebsite failed");
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
               System.out.println("setBucketWebsite failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Configuring Redirection for All Requests
------------------------------------------------------

This example configures redirection of all requests for bucket **examplebucket**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.ProtocolEnum;
   import com.obs.services.model.RedirectAllRequest;
   import com.obs.services.model.WebsiteConfiguration;
   public class SetBucketWebsite003
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
               // Sample code is as follows:
               WebsiteConfiguration config = new WebsiteConfiguration();
               RedirectAllRequest redirectAll = new RedirectAllRequest();
               redirectAll.setHostName("www.example.com");
               redirectAll.setRedirectProtocol(ProtocolEnum.HTTP);
               config.setRedirectAllRequestsTo(redirectAll);
               obsClient.setBucketWebsite("examplebucket", config);
               System.out.println("setBucketWebsite successfully");
           } catch (ObsException e) {
               System.out.println("setBucketWebsite failed");
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
               System.out.println("setBucketWebsite failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
