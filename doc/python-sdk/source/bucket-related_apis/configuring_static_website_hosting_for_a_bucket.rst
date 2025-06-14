:original_name: obs_22_0824.html

.. _obs_22_0824:

Configuring Static Website Hosting for a Bucket
===============================================

Function
--------

You can host static website resources such as HTML web pages, flash files, or audio and video files in an OBS bucket, so that you can provide these hosted resources using the bucket's website endpoint to end users. Typical use cases include:

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

ObsClient.setBucketWebsite(bucketName, website, extensionHeaders)

Request Parameters
------------------

+------------------+---------------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter        | Type                                                                            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
+==================+=================================================================================+====================+===================================================================================================================================================================================+
| bucketName       | str                                                                             | Yes                | **Explanation:**                                                                                                                                                                  |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | Bucket name                                                                                                                                                                       |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | **Restrictions:**                                                                                                                                                                 |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
|                  |                                                                                 |                    | -  A bucket name:                                                                                                                                                                 |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
|                  |                                                                                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
|                  |                                                                                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
|                  |                                                                                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
|                  |                                                                                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket properties comply with those set in the first creation request. |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | **Default value**:                                                                                                                                                                |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | None                                                                                                                                                                              |
+------------------+---------------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| website          | :ref:`WebsiteConfiguration <obs_22_0824__en-us_topic_0142814686_table14455523>` | Yes                | **Explanation:**                                                                                                                                                                  |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | Input parameters for configuring static website hosting. For details, see :ref:`Table 1 <obs_22_0824__en-us_topic_0142814686_table14455523>`.                                     |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | **Default value**:                                                                                                                                                                |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | None                                                                                                                                                                              |
+------------------+---------------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| extensionHeaders | dict                                                                            | No                 | **Explanation:**                                                                                                                                                                  |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | Extension headers.                                                                                                                                                                |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | **Value range**:                                                                                                                                                                  |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | See :ref:`User-defined Headers <obs_22_1305>`.                                                                                                                                    |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | **Default value**:                                                                                                                                                                |
|                  |                                                                                 |                    |                                                                                                                                                                                   |
|                  |                                                                                 |                    | None                                                                                                                                                                              |
+------------------+---------------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_22_0824__en-us_topic_0142814686_table14455523:

.. table:: **Table 1** WebsiteConfiguration

   +----------------------+--------------------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter            | Type                                                                           | Mandatory (Yes/No)                | Description                                                                                                 |
   +======================+================================================================================+===================================+=============================================================================================================+
   | redirectAllRequestTo | :ref:`RedirectAllRequestTo <obs_22_0824__table1255418118393>`                  | No if used as a request parameter | **Explanation:**                                                                                            |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | Redirection rules for all requests. For details, see :ref:`Table 2 <obs_22_0824__table1255418118393>`.      |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | **Default value**:                                                                                          |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | None                                                                                                        |
   +----------------------+--------------------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------+
   | indexDocument        | :ref:`IndexDocument <obs_22_0824__table033975403914>`                          | No if used as a request parameter | **Explanation:**                                                                                            |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | Default page configuration. For details, see :ref:`Table 3 <obs_22_0824__table033975403914>`.               |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | **Default value**:                                                                                          |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | None                                                                                                        |
   +----------------------+--------------------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------+
   | errorDocument        | :ref:`ErrorDocument <obs_22_0824__table99251319174017>`                        | No if used as a request parameter | **Explanation:**                                                                                            |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | Error page configuration. For details, see :ref:`Table 4 <obs_22_0824__table99251319174017>`.               |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | **Default value**:                                                                                          |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | None                                                                                                        |
   +----------------------+--------------------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------+
   | routingRules         | list of :ref:`RoutingRule <obs_22_0824__en-us_topic_0142814587_table14455523>` | No if used as a request parameter | **Explanation:**                                                                                            |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | List of routing rules. For details, see :ref:`Table 5 <obs_22_0824__en-us_topic_0142814587_table14455523>`. |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | **Default value**:                                                                                          |
   |                      |                                                                                |                                   |                                                                                                             |
   |                      |                                                                                |                                   | None                                                                                                        |
   +----------------------+--------------------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------------------------------------------+

.. note::

   -  **errorDocument**, **indexDocument**, and **routingRules** must be used together and they cannot be used with **redirectAllRequestsTo**.
   -  When **errorDocument**, **indexDocument**, and **routingRules** are used together, **routingRules** can be left blank.
   -  You must specify either the combo of fields **ErrorDocument**, **IndexDocument**, and **RoutingRules**, or the **RedirectAllRequestsTo** field.

.. _obs_22_0824__table1255418118393:

.. table:: **Table 2** RedirectAllRequestTo

   +-----------------+-----------------+------------------------------------+------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                 | Description                                                      |
   +=================+=================+====================================+==================================================================+
   | hostName        | str             | Yes if used as a request parameter | **Explanation:**                                                 |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | Host name used for redirection, for example, **www.example.com** |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | **Restrictions:**                                                |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | The host name must comply with the host name rules.              |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | **Default value**:                                               |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | None                                                             |
   +-----------------+-----------------+------------------------------------+------------------------------------------------------------------+
   | protocol        | str             | No if used as a request parameter  | **Explanation:**                                                 |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | Protocol used for redirection                                    |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | **Value range**:                                                 |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | -  http                                                          |
   |                 |                 |                                    | -  https                                                         |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | **Default value**:                                               |
   |                 |                 |                                    |                                                                  |
   |                 |                 |                                    | None                                                             |
   +-----------------+-----------------+------------------------------------+------------------------------------------------------------------+

.. _obs_22_0824__table033975403914:

.. table:: **Table 3** IndexDocument

   +-----------------+-----------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                 | Description                                                                                                                                                                                                                                         |
   +=================+=================+====================================+=====================================================================================================================================================================================================================================================+
   | suffix          | str             | Yes if used as a request parameter | **Explanation:**                                                                                                                                                                                                                                    |
   |                 |                 |                                    |                                                                                                                                                                                                                                                     |
   |                 |                 |                                    | Suffix that is appended to the request for a directory. For example, if the suffix is **index.html** and you request **samplebucket/images/**, the returned data will be for the object named **images/index.html** in the bucket **samplebucket**. |
   |                 |                 |                                    |                                                                                                                                                                                                                                                     |
   |                 |                 |                                    | **Value range**:                                                                                                                                                                                                                                    |
   |                 |                 |                                    |                                                                                                                                                                                                                                                     |
   |                 |                 |                                    | This parameter can neither be left blank nor contain slashes (/).                                                                                                                                                                                   |
   |                 |                 |                                    |                                                                                                                                                                                                                                                     |
   |                 |                 |                                    | **Default value**:                                                                                                                                                                                                                                  |
   |                 |                 |                                    |                                                                                                                                                                                                                                                     |
   |                 |                 |                                    | None                                                                                                                                                                                                                                                |
   +-----------------+-----------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_22_0824__table99251319174017:

.. table:: **Table 4** ErrorDocument

   +-----------------+-----------------+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                | Description                                                                                                               |
   +=================+=================+===================================+===========================================================================================================================+
   | key             | str             | No if used as a request parameter | **Explanation:**                                                                                                          |
   |                 |                 |                                   |                                                                                                                           |
   |                 |                 |                                   | Object name to use when a **4**\ *XX* error occurs. This parameter specifies the webpage to display when an error occurs. |
   |                 |                 |                                   |                                                                                                                           |
   |                 |                 |                                   | **Value range**:                                                                                                          |
   |                 |                 |                                   |                                                                                                                           |
   |                 |                 |                                   | The value must contain 1 to 1,024 characters.                                                                             |
   |                 |                 |                                   |                                                                                                                           |
   |                 |                 |                                   | **Default value**:                                                                                                        |
   |                 |                 |                                   |                                                                                                                           |
   |                 |                 |                                   | None                                                                                                                      |
   +-----------------+-----------------+-----------------------------------+---------------------------------------------------------------------------------------------------------------------------+

.. _obs_22_0824__en-us_topic_0142814587_table14455523:

.. table:: **Table 5** RoutingRule

   +-----------------+----------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                               | Mandatory (Yes/No)                 | Description                                                                                        |
   +=================+====================================================+====================================+====================================================================================================+
   | condition       | :ref:`Condition <obs_22_0824__table141092472404>`  | No if used as a request parameter  | **Explanation:**                                                                                   |
   |                 |                                                    |                                    |                                                                                                    |
   |                 |                                                    |                                    | Conditions that must be met for the specified redirect to apply                                    |
   |                 |                                                    |                                    |                                                                                                    |
   |                 |                                                    |                                    | **Value range**:                                                                                   |
   |                 |                                                    |                                    |                                                                                                    |
   |                 |                                                    |                                    | See :ref:`Table 6 <obs_22_0824__table141092472404>`.                                               |
   |                 |                                                    |                                    |                                                                                                    |
   |                 |                                                    |                                    | **Default value**:                                                                                 |
   |                 |                                                    |                                    |                                                                                                    |
   |                 |                                                    |                                    | None                                                                                               |
   +-----------------+----------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------------------+
   | redirect        | :ref:`Redirect <obs_22_0824__table19271235134119>` | Yes if used as a request parameter | **Explanation:**                                                                                   |
   |                 |                                                    |                                    |                                                                                                    |
   |                 |                                                    |                                    | Details about the redirection. For details, see :ref:`Table 7 <obs_22_0824__table19271235134119>`. |
   |                 |                                                    |                                    |                                                                                                    |
   |                 |                                                    |                                    | **Default value**:                                                                                 |
   |                 |                                                    |                                    |                                                                                                    |
   |                 |                                                    |                                    | None                                                                                               |
   +-----------------+----------------------------------------------------+------------------------------------+----------------------------------------------------------------------------------------------------+

.. _obs_22_0824__table141092472404:

.. table:: **Table 6** Condition

   +-----------------------------+-----------------+-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                   | Type            | Mandatory (Yes/No)                | Description                                                                                                                                                                                                                                    |
   +=============================+=================+===================================+================================================================================================================================================================================================================================================+
   | keyPrefixEquals             | str             | No if used as a request parameter | **Explanation:**                                                                                                                                                                                                                               |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | Object name prefix for the redirection to take effect. If the name prefix of the requested object is the same as the value specified for this parameter, the redirection rule takes effect.                                                    |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | For example, to redirect the requests for the object **ExamplePage.html**, set **KeyPrefixEquals** to **ExamplePage.html**.                                                                                                                    |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | **Restrictions:**                                                                                                                                                                                                                              |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | This parameter cannot be used together with **httpErrorCodeReturnedEquals**.                                                                                                                                                                   |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | **Value range**:                                                                                                                                                                                                                               |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                  |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | **Default value**:                                                                                                                                                                                                                             |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | None                                                                                                                                                                                                                                           |
   +-----------------------------+-----------------+-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | httpErrorCodeReturnedEquals | int             | No if used as a request parameter | **Explanation:**                                                                                                                                                                                                                               |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | HTTP error code for the redirection to take effect. If there is an error, and the error code returned is the same as the value specified for this parameter, the redirection rule takes effect.                                                |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | For example, if you want to redirect requests to **NotFound.html** when HTTP error code **404** is returned, set **httpErrorCodeReturnedEquals** to **404** in **Condition**, and set **ReplaceKeyWith** to **NotFound.html** in **Redirect**. |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | **Restrictions:**                                                                                                                                                                                                                              |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | This parameter cannot be used together with **keyPrefixEquals**.                                                                                                                                                                               |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | **Default value**:                                                                                                                                                                                                                             |
   |                             |                 |                                   |                                                                                                                                                                                                                                                |
   |                             |                 |                                   | None                                                                                                                                                                                                                                           |
   +-----------------------------+-----------------+-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_22_0824__table19271235134119:

.. table:: **Table 7** Redirect

   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | Parameter            | Type            | Mandatory (Yes/No)                | Description                                                           |
   +======================+=================+===================================+=======================================================================+
   | protocol             | str             | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | Protocol used for redirection                                         |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Value range**:                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | -  http                                                               |
   |                      |                 |                                   | -  https                                                              |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | hostName             | str             | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | Host name used for redirection                                        |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | replaceKeyPrefixWith | str             | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | Object name prefix used in the redirection request                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Value range**:                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | The value must contain 1 to 1,024 characters.                         |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | replaceKeyWith       | str             | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | Object name used in the redirection request                           |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Restrictions:**                                                     |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | This parameter cannot be used together with **replaceKeyPrefixWith**. |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Value range**:                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | The value must contain 1 to 1,024 characters.                         |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | httpRedirectCode     | int             | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | HTTP status code in the response to the redirect request.             |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+

Responses
---------

+-----------------------------------------------------+-----------------------------------+
| Type                                                | Description                       |
+=====================================================+===================================+
| :ref:`GetResult <obs_22_0824__table20121844173311>` | **Explanation:**                  |
|                                                     |                                   |
|                                                     | SDK common results                |
+-----------------------------------------------------+-----------------------------------+

.. _obs_22_0824__table20121844173311:

.. table:: **Table 8** GetResult

   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                      |
   +=======================+=======================+==================================================================================================================================================================================================================================================================================================+
   | status                | int                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | HTTP status code                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Value range**:                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | A status code is a group of digits ranging from 2\ *xx* (indicating successes) to 4\ *xx* or 5\ *xx* (indicating errors). It indicates the status of a response.                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | reason                | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Reason description.                                                                                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | errorCode             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Error code returned by the OBS server. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | errorMessage          | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Error message returned by the OBS server. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | requestId             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Request ID returned by the OBS server                                                                                                                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | indicator             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Error indicator returned by the OBS server.                                                                                                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hostId                | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Requested server ID. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource              | str                   | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Error source (a bucket or an object). If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                             |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | header                | list                  | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Response header list, composed of tuples. Each tuple consists of two elements, respectively corresponding to the key and value of a response header.                                                                                                                                             |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | body                  | object                | **Explanation:**                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | Result content returned after the operation is successful. If the value of **status** is larger than **300**, the value of **body** is null. The value varies with the API being called. For details, see :ref:`Bucket-Related APIs <obs_22_0800>` and :ref:`Object-Related APIs <obs_22_0900>`. |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example configures static website hosting for bucket **examplebucket**.

::

   from obs import ObsClient
   from obs import WebsiteConfiguration
   from obs import IndexDocument
   from obs import ErrorDocument
   from obs import RoutingRule
   from obs import Condition
   from obs import Redirect
   import os
   import traceback

   # Obtain an AK and SK pair using environment variables or import the AK and SK pair in other ways. Using hard coding may result in leakage.
   # Obtain an AK and SK pair on the management console.
   ak = os.getenv("AccessKeyID")
   sk = os.getenv("SecretAccessKey")
   # (Optional) If you use a temporary AK and SK pair and a security token to access OBS, obtain them from environment variables.
   # security_token = os.getenv("SecurityToken")
   # Set server to the endpoint of the region where the bucket is located.
   server = "https://your-endpoint"

   # Create an obsClient instance.
   # If you use a temporary AK and SK pair and a security token to access OBS, you must specify security_token when creating an instance.
   obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)
   try:
       # Specify an error page when a 4XX error occurs.
       errorDocument = ErrorDocument(key='error.html')
       # Specify a default page.
       indexDocument = IndexDocument(suffix='index.html')
       # Specify a rule for redirecting requests to NotFound.html if the status code is 404.
       routingRule1 = RoutingRule(condition=Condition(httpErrorCodeReturnedEquals=404),
                                  redirect=Redirect(protocol='http', replaceKeyWith='NotFound.html'))
       # Configure the redirection rules in list format. Multiple rules can be configured.
       routingRules = [routingRule1]
       bucketName = "examplebucket"
       # Configure static website hosting for the bucket.
       resp = obsClient.setBucketWebsite(bucketName,
                                         WebsiteConfiguration(errorDocument=errorDocument, indexDocument=indexDocument,
                                                              routingRules=routingRules))

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Set Bucket Website Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Set Bucket Website Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Set Bucket Website Failed')
       print(traceback.format_exc())
