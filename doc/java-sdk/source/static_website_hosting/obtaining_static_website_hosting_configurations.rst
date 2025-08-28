:original_name: obs_21_1604.html

.. _obs_21_1604:

Obtaining Static Website Hosting Configurations
===============================================

Function
--------

You can host static website resources such as HTML web pages, flash files, or audio and video files in an OBS bucket, so that you can provide these hosted resources using the bucket's website endpoint to end users. Typical use cases include:

-  Redirecting all requests to another website
-  Redirecting specific requests to another website

This API returns the static website hosting configurations of the bucket.

Restrictions
------------

-  To obtain the static website hosting configurations of a bucket, you must be the bucket owner or have the required permission (**obs:bucket:GetBucketWebsite** in IAM or **GetBucketWebsite** in a bucket policy).

Method
------

obsClient.getBucketWebsite(final :ref:`BaseBucketRequest <obs_21_1604__table43960571>` :ref:`request <obs_21_1604__table72121329103020>`)

Request Parameters
------------------

.. _obs_21_1604__table72121329103020:

.. table:: **Table 1** List of request parameters

   +-----------------+-------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                  | Mandatory (Yes/No) | Description                                                                                                           |
   +=================+=======================================================+====================+=======================================================================================================================+
   | request         | :ref:`BaseBucketRequest <obs_21_1604__table43960571>` | Yes                | **Explanation:**                                                                                                      |
   |                 |                                                       |                    |                                                                                                                       |
   |                 |                                                       |                    | Request parameters related to basic bucket information. For details, see :ref:`Table 2 <obs_21_1604__table43960571>`. |
   +-----------------+-------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1604__table43960571:

.. table:: **Table 2** BaseBucketRequest

   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=================+====================+===================================================================================================================================================================================+
   | bucketName      | String          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Bucket name.                                                                                                                                                                      |
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
   |                 |                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** WebsiteConfiguration

   +-----------------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                        | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                         |
   +=======================+=============================================================+====================+=====================================================================================================================================================================================================================================================+
   | suffix                | String                                                      | No                 | **Explanation:**                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | Suffix that is appended to the request for a directory. For example, if the suffix is **index.html** and you request **samplebucket/images/**, the returned data will be for the object named **images/index.html** in the bucket **samplebucket**. |
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
   |                       |                                                             |                    | **Value range**:                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                       |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | **Default value**:                                                                                                                                                                                                                                  |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | None                                                                                                                                                                                                                                                |
   +-----------------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | redirectAllRequestsTo | :ref:`RedirectAllRequest <obs_21_1604__table1630621572518>` | No                 | **Explanation:**                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | Redirection rules for all requests. For details, see :ref:`Table 4 <obs_21_1604__table1630621572518>`.                                                                                                                                              |
   +-----------------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | routeRules            | List<:ref:`RouteRule <obs_21_1604__table4262125213320>`>    | No                 | **Explanation:**                                                                                                                                                                                                                                    |
   |                       |                                                             |                    |                                                                                                                                                                                                                                                     |
   |                       |                                                             |                    | List of routing rules. For details, see :ref:`Table 6 <obs_21_1604__table4262125213320>`.                                                                                                                                                           |
   +-----------------------+-------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_1604__table1630621572518:

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
   | protocol        | :ref:`ProtocolEnum <obs_21_1604__table155207227288>` | No                 | **Explanation:**                                                  |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | Protocol used for redirection.                                    |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | **Value range**:                                                  |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | See :ref:`Table 5 <obs_21_1604__table155207227288>`.              |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | **Default value**:                                                |
   |                 |                                                      |                    |                                                                   |
   |                 |                                                      |                    | None                                                              |
   +-----------------+------------------------------------------------------+--------------------+-------------------------------------------------------------------+

.. _obs_21_1604__table155207227288:

.. table:: **Table 5** ProtocolEnum

   ======== ============= ====================================
   Constant Default Value Description
   ======== ============= ====================================
   HTTP     http          HTTP protocol used for redirection.
   HTTPS    https         HTTPS protocol used for redirection.
   ======== ============= ====================================

.. _obs_21_1604__table4262125213320:

.. table:: **Table 6** RouteRule

   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                       | Mandatory (Yes/No) | Description                                                                                         |
   +=================+============================================================+====================+=====================================================================================================+
   | condition       | :ref:`RouteRuleCondition <obs_21_1604__table336864313514>` | No                 | **Explanation:**                                                                                    |
   |                 |                                                            |                    |                                                                                                     |
   |                 |                                                            |                    | Conditions of a redirection rule. For details, see :ref:`Table 7 <obs_21_1604__table336864313514>`. |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+
   | redirect        | :ref:`Redirect <obs_21_1604__table12397124916367>`         | Yes                | **Explanation:**                                                                                    |
   |                 |                                                            |                    |                                                                                                     |
   |                 |                                                            |                    | Details about the redirection. For details, see :ref:`Table 8 <obs_21_1604__table12397124916367>`.  |
   +-----------------+------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------+

.. _obs_21_1604__table336864313514:

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

.. _obs_21_1604__table12397124916367:

.. table:: **Table 8** Redirect

   +----------------------+------------------------------------------------------+--------------------+-----------------------------------------------------------------------+
   | Parameter            | Type                                                 | Mandatory (Yes/No) | Description                                                           |
   +======================+======================================================+====================+=======================================================================+
   | Protocol             | :ref:`ProtocolEnum <obs_21_1604__table155207227288>` | No                 | **Explanation:**                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | Protocol used for redirection.                                        |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | **Value range**:                                                      |
   |                      |                                                      |                    |                                                                       |
   |                      |                                                      |                    | See :ref:`Table 5 <obs_21_1604__table155207227288>`.                  |
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

Code Examples
-------------

This example returns the website configuration of bucket **examplebucket** using **obsClient.getBucketWebsite**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.RouteRule;
   import com.obs.services.model.WebsiteConfiguration;
   public class GetBucketWebsite001
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
               // View the website configuration of the bucket.
               WebsiteConfiguration config = obsClient.getBucketWebsite("examplebucket");
               System.out.println("Key:" + config.getKey());
               System.out.println("Suffix:" + config.getSuffix());
               for(RouteRule rule : config.getRouteRules()){
                   System.out.println("rule:" +rule);
               }
               System.out.println("getBucketWebsite successfully");
           } catch (ObsException e) {
               System.out.println("getBucketWebsite failed");
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
               System.out.println("getBucketWebsite failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
