:original_name: obs_29_1203.html

.. _obs_29_1203:

Configuring Static Website Hosting
==================================

Function
--------

You can host static website resources such as HTML web pages, flash files, or audio and video files in an OBS bucket, so that you can provide these hosted resources using the bucket's website endpoint to end users. Typical use cases include:

-  Redirecting all requests to another website
-  Redirecting specific requests

This API configures static website hosting for a bucket.

Restrictions
------------

-  Periods (.) should be avoided in the target bucket name, or there may be certificate verification failures on the client when using HTTPS for access.
-  The request body of the website configuration cannot exceed 10 KB.
-  To configure static website hosting for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketWebsite** in IAM or **PutBucketWebsite** in a bucket policy).

Method
------

.. code-block::

   ObsClient.setBucketWebsite(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                          | Mandatory (Yes/No) | Description                                                                                                                                                                          |
   +=======================+===============================================================+====================+======================================================================================================================================================================================+
   | Bucket                | string                                                        | Yes                | **Explanation:**                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | Bucket name                                                                                                                                                                          |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Restrictions**:                                                                                                                                                                    |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                     |
   |                       |                                                               |                    | -  A bucket name:                                                                                                                                                                    |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                         |
   |                       |                                                               |                    |    -  Cannot be formatted as an IP address.                                                                                                                                          |
   |                       |                                                               |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                           |
   |                       |                                                               |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                      |
   |                       |                                                               |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                            |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request. |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Value range**:                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | The value can contain 3 to 63 characters.                                                                                                                                            |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Default value**:                                                                                                                                                                   |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | None                                                                                                                                                                                 |
   +-----------------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RedirectAllRequestsTo | :ref:`RedirectAllRequestTo <obs_29_1203__table1630621572518>` | No                 | **Explanation:**                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | Redirection rule for all requests                                                                                                                                                    |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Restrictions**:                                                                                                                                                                    |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | None                                                                                                                                                                                 |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Value range**:                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | See :ref:`Table 2 <obs_29_1203__table1630621572518>`.                                                                                                                                |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Default value**:                                                                                                                                                                   |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | None                                                                                                                                                                                 |
   +-----------------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IndexDocument         | :ref:`IndexDocument <obs_29_1203__table179962100303>`         | No                 | **Explanation:**                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | Default page configuration.                                                                                                                                                          |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Restrictions**:                                                                                                                                                                    |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | None                                                                                                                                                                                 |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Value range**:                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | See :ref:`Table 3 <obs_29_1203__table179962100303>`.                                                                                                                                 |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Default value**:                                                                                                                                                                   |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | None                                                                                                                                                                                 |
   +-----------------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ErrorDocument         | :ref:`ErrorDocument <obs_29_1203__table1292634533216>`        | No                 | **Explanation:**                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | Error page configuration.                                                                                                                                                            |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Restrictions**:                                                                                                                                                                    |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | None                                                                                                                                                                                 |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Value range**:                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | See :ref:`Table 4 <obs_29_1203__table1292634533216>`.                                                                                                                                |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Default value**:                                                                                                                                                                   |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | None                                                                                                                                                                                 |
   +-----------------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RoutingRules          | :ref:`RoutingRule <obs_29_1203__table4262125213320>`\ []      | No                 | **Explanation:**                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | Redirection rule list                                                                                                                                                                |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Restrictions**:                                                                                                                                                                    |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | None                                                                                                                                                                                 |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Value range**:                                                                                                                                                                     |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | See :ref:`Table 5 <obs_29_1203__table4262125213320>`.                                                                                                                                |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | **Default value**:                                                                                                                                                                   |
   |                       |                                                               |                    |                                                                                                                                                                                      |
   |                       |                                                               |                    | None                                                                                                                                                                                 |
   +-----------------------+---------------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   -  **ErrorDocument**, **IndexDocument**, and **RoutingRules** must be used together and must not be used with **RedirectAllRequestsTo**.
   -  When **ErrorDocument**, **IndexDocument**, and **RoutingRules** are used together, **RoutingRules** can be left blank.
   -  You must set either these three parameters (**ErrorDocument**, **IndexDocument**, and **RoutingRules**) or **RedirectAllRequestsTo**.

.. _obs_29_1203__table1630621572518:

.. table:: **Table 2** RedirectAllRequestsTo

   +-----------------+-----------------+-----------------------------------------------+--------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                            | Description                                                        |
   +=================+=================+===============================================+====================================================================+
   | HostName        | string          | Yes if **RedirectAllRequestsTo** is specified | **Explanation:**                                                   |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | Domain name used for redirection, for example, **www.example.com** |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | **Restrictions**:                                                  |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | The domain name must comply with the domain name standards.        |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | **Value range**:                                                   |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | None                                                               |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | **Default value**:                                                 |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | None                                                               |
   +-----------------+-----------------+-----------------------------------------------+--------------------------------------------------------------------+
   | Protocol        | string          | No                                            | **Explanation:**                                                   |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | Protocol used for redirection                                      |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | **Restrictions**:                                                  |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | None                                                               |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | **Value range**:                                                   |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | http or https                                                      |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | **Default value**:                                                 |
   |                 |                 |                                               |                                                                    |
   |                 |                 |                                               | None                                                               |
   +-----------------+-----------------+-----------------------------------------------+--------------------------------------------------------------------+

.. _obs_29_1203__table179962100303:

.. table:: **Table 3** IndexDocument

   +-----------------+-----------------+---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                    | Description                                                                                                                                                                                                                                         |
   +=================+=================+=======================================+=====================================================================================================================================================================================================================================================+
   | Suffix          | string          | Yes if **IndexDocument** is specified | **Explanation:**                                                                                                                                                                                                                                    |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | Suffix that is appended to the request for a directory. For example, if the suffix is **index.html** and you request **samplebucket/images/**, the returned data will be for the object named **images/index.html** in the bucket **samplebucket**. |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | **Restrictions**:                                                                                                                                                                                                                                   |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | This parameter can neither be left blank nor contain slashes (/).                                                                                                                                                                                   |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | **Value range**:                                                                                                                                                                                                                                    |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | None                                                                                                                                                                                                                                                |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | **Default value**:                                                                                                                                                                                                                                  |
   |                 |                 |                                       |                                                                                                                                                                                                                                                     |
   |                 |                 |                                       | None                                                                                                                                                                                                                                                |
   +-----------------+-----------------+---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1203__table1292634533216:

.. table:: **Table 4** ErrorDocument

   +-----------------+-----------------+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                   | Description                                                                                                                      |
   +=================+=================+======================================+==================================================================================================================================+
   | Key             | string          | No if **ErrorDocument** is specified | **Explanation:**                                                                                                                 |
   |                 |                 |                                      |                                                                                                                                  |
   |                 |                 |                                      | The object name that is used when a 4\ *XX* error occurs. This element specifies the page that is returned when an error occurs. |
   |                 |                 |                                      |                                                                                                                                  |
   |                 |                 |                                      | **Restrictions**:                                                                                                                |
   |                 |                 |                                      |                                                                                                                                  |
   |                 |                 |                                      | None                                                                                                                             |
   |                 |                 |                                      |                                                                                                                                  |
   |                 |                 |                                      | **Value range**:                                                                                                                 |
   |                 |                 |                                      |                                                                                                                                  |
   |                 |                 |                                      | The key can contain 1 to 1,024 characters.                                                                                       |
   |                 |                 |                                      |                                                                                                                                  |
   |                 |                 |                                      | **Default value**:                                                                                                               |
   |                 |                 |                                      |                                                                                                                                  |
   |                 |                 |                                      | None                                                                                                                             |
   +-----------------+-----------------+--------------------------------------+----------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1203__table4262125213320:

.. table:: **Table 5** RoutingRule

   +-----------------+----------------------------------------------------+-------------------------------------+-------------------------------------------------------------------+
   | Parameter       | Type                                               | Mandatory (Yes/No)                  | Description                                                       |
   +=================+====================================================+=====================================+===================================================================+
   | Condition       | :ref:`Condition <obs_29_1203__table336864313514>`  | No                                  | **Explanation:**                                                  |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | Conditions that must be met for the specified rule to take effect |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | **Restrictions**:                                                 |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | None                                                              |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | **Value range**:                                                  |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | See :ref:`Table 6 <obs_29_1203__table336864313514>`.              |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | **Default value**:                                                |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | None                                                              |
   +-----------------+----------------------------------------------------+-------------------------------------+-------------------------------------------------------------------+
   | Redirect        | :ref:`Redirect <obs_29_1203__table12397124916367>` | Yes if **RoutingRule** is specified | **Explanation:**                                                  |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | Details about the redirection                                     |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | **Restrictions**:                                                 |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | None                                                              |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | **Value range**:                                                  |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | See :ref:`Table 7 <obs_29_1203__table12397124916367>`.            |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | **Default value**:                                                |
   |                 |                                                    |                                     |                                                                   |
   |                 |                                                    |                                     | None                                                              |
   +-----------------+----------------------------------------------------+-------------------------------------+-------------------------------------------------------------------+

.. _obs_29_1203__table336864313514:

.. table:: **Table 6** Condition

   +-----------------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                   | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                   |
   +=============================+=================+====================+===============================================================================================================================================================================================================================================+
   | KeyPrefixEquals             | string          | No                 | **Explanation:**                                                                                                                                                                                                                              |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | Object name prefix for the redirection to take effect. If the name prefix of the requested object is the same as the value specified for this parameter, the redirection rule takes effect.                                                   |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | For example, to redirect the requests for the object **ExamplePage.html**, set **KeyPrefixEquals** to **ExamplePage.html**.                                                                                                                   |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | **Restrictions**:                                                                                                                                                                                                                             |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | This parameter cannot be used together with **HttpErrorCodeReturnedEquals**.                                                                                                                                                                  |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | **Value range**:                                                                                                                                                                                                                              |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | The value can contain 1 to 1,024 characters.                                                                                                                                                                                                  |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | **Default value**:                                                                                                                                                                                                                            |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | None                                                                                                                                                                                                                                          |
   +-----------------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HttpErrorCodeReturnedEquals | string          | No                 | **Explanation:**                                                                                                                                                                                                                              |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | HTTP error code for the redirection to take effect. If an error code returned is the same as the value specified for this parameter, the redirection rule takes effect.                                                                       |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | For example, if you want to redirect requests to **NotFound.html** when HTTP error code **404** is returned, set **HttpErrorCodeReturnedEquals** to **404** in **Condition** and set **ReplaceKeyWith** to **NotFound.html** in **Redirect**. |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | **Restrictions**:                                                                                                                                                                                                                             |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | This parameter cannot be used together with **KeyPrefixEquals**.                                                                                                                                                                              |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | **Default value**:                                                                                                                                                                                                                            |
   |                             |                 |                    |                                                                                                                                                                                                                                               |
   |                             |                 |                    | None                                                                                                                                                                                                                                          |
   +-----------------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1203__table12397124916367:

.. table:: **Table 7** Redirect

   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | Parameter            | Type            | Mandatory (Yes/No)                | Description                                                           |
   +======================+=================+===================================+=======================================================================+
   | Protocol             | string          | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | Protocol used for redirection                                         |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Restrictions**:                                                     |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Value range**:                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | http or https                                                         |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | HostName             | string          | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | Domain name used for redirection                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Restrictions**:                                                     |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | The domain name must comply with the domain name standards.           |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Value range**:                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | ReplaceKeyPrefixWith | string          | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | Object name prefix used in the redirection request                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Restrictions**:                                                     |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Value range**:                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | The value can contain 1 to 1,024 characters.                          |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | ReplaceKeyWith       | string          | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | Object name used in the redirection request                           |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Restrictions**:                                                     |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | This parameter cannot be used together with **replaceKeyPrefixWith**. |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Value range**:                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | The value can contain 1 to 1,024 characters.                          |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+
   | HttpRedirectCode     | string          | No if used as a request parameter | **Explanation:**                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | HTTP status code in the response to the redirection request           |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Restrictions**:                                                     |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Value range**:                                                      |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | **Default value**:                                                    |
   |                      |                 |                                   |                                                                       |
   |                      |                 |                                   | None                                                                  |
   +----------------------+-----------------+-----------------------------------+-----------------------------------------------------------------------+

Responses
---------

.. table:: **Table 8** Responses

   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------+
   | Type                                                                                      | Description                                                        |
   +===========================================================================================+====================================================================+
   | :ref:`Table 9 <obs_29_1203__table1722625714202>`                                          | **Explanation:**                                                   |
   |                                                                                           |                                                                    |
   | .. note::                                                                                 | Returned results.                                                  |
   |                                                                                           |                                                                    |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. | For details, see :ref:`Table 9 <obs_29_1203__table1722625714202>`. |
   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------+

.. _obs_29_1203__table1722625714202:

.. table:: **Table 9** Response

   +-----------------------+-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                    |
   +=======================+=====================================================+================================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_1203__table6176201212273>` | **Explanation:**                                                                                                                                                               |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 10 <obs_29_1203__table6176201212273>`. |
   +-----------------------+-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`Table 11 <obs_29_1203__table33959011>`        | **Explanation:**                                                                                                                                                               |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | Results outputted for a successful call. For details, see :ref:`Table 11 <obs_29_1203__table33959011>`.                                                                        |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | **Restrictions:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                                |
   |                       |                                                     | This parameter is not included if the value of **Status** is greater than 300.                                                                                                 |
   +-----------------------+-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1203__table6176201212273:

.. table:: **Table 10** ICommonMsg

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Parameter**         | **Type**              | **Description**                                                                                                                                                  |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                | number                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | HTTP status code returned by the OBS server.                                                                                                                     |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | **Value range**:                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | A status code is a group of digits indicating the status of a response. It ranges from 2\ *xx* (indicating successes) to 4\ *xx* or 5\ *xx* (indicating errors). |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Code                  | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Error code returned by the OBS server.                                                                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Message               | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Error description returned by the OBS server.                                                                                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HostId                | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Request server ID returned by the OBS server.                                                                                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Request ID returned by the OBS server.                                                                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Id2                   | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Request ID2 returned by the OBS server.                                                                                                                          |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Indicator             | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Error code details returned by the OBS server.                                                                                                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1203__table33959011:

.. table:: **Table 11** BaseResponseOutput

   +-----------------------+-----------------------+---------------------------------------+
   | Parameter             | Type                  | Description                           |
   +=======================+=======================+=======================================+
   | RequestId             | string                | **Explanation:**                      |
   |                       |                       |                                       |
   |                       |                       | Request ID returned by the OBS server |
   +-----------------------+-----------------------+---------------------------------------+

Code Examples
-------------

This example configures website hosting for bucket **examplebucket**.

::

   // Import the OBS library.
   // Use npm to install the client.
   const ObsClient = require("esdk-obs-nodejs");
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');

   // Create an instance of ObsClient.
   const obsClient = new ObsClient({
     // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
     // Obtain an AK/SK pair on the management console.
     access_key_id: process.env.ACCESS_KEY_ID,
     secret_access_key: process.env.SECRET_ACCESS_KEY,
     // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
     // security_token: process.env.SECURITY_TOKEN,
     // Enter the endpoint of the region where the bucket is located.
     server: "https://your-endpoint"
   });

   async function setBucketWebsite() {
     try {
       const params = {
         // Specify the bucket name.
         Bucket: "examplebucket",
         // Specify a default page (index.html in this example).
         IndexDocument: { Suffix: 'index.html' },
         // Specify an error page (error.html in this example).
         ErrorDocument: { Key: 'error.html' },
         // Configure redirection for all requests.
         RedirectAllRequestsTo : {HostName : 'www.example.com', Protocol : 'http'}
         // Specify redirect rules for requests.
         RoutingRules: [
           { Redirect: { HostName: "www.a.com", Protocol: obs.ProtocolHttp, ReplaceKeyPrefixWith: "prefix", HttpRedirectCode: "304" } },
           { Redirect: { HostName: "www.b.com", Protocol: obs.ProtocolHttps, ReplaceKeyWith: "replaceKey", HttpRedirectCode: "304" } },
         ]
       };
       // Configure the website settings for the bucket.
       const result = await obsClient.setBucketWebsite(params);
       if (result.CommonMsg.Status <= 300) {
         console.log("Set bucket(%s)'s website configuration successful!", params.Bucket);
         console.log("RequestId: %s", result.CommonMsg.RequestId);
         return;
       };
       console.log("An ObsError was found, which means your request sent to OBS was rejected with an error response.");
       console.log("Status: %d", result.CommonMsg.Status);
       console.log("Code: %s", result.CommonMsg.Code);
       console.log("Message: %s", result.CommonMsg.Message);
       console.log("RequestId: %s", result.CommonMsg.RequestId);
     } catch (error) {
       console.log("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.");
       console.log(error);
     };
   };

   setBucketWebsite();
