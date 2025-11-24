:original_name: obs_29_0412.html

.. _obs_29_0412:

Uploading an Object - Browser-Based
===================================

Function
--------

Performing a browser-based upload is to upload objects to a specified bucket in HTML form. The maximum size of an object is 5 GB.

You can call **ObsClient.createPostSignatureSync** to generate request parameters for a browser-based upload. The procedure is as follows:

#. Call **ObsClient.createPostSignatureSync** to generate request parameters for authentication.
#. Prepare an HTML form page.
#. Enter the request parameters in the HTML page.
#. Select a local file and upload it in browser-based mode.

Method
------

.. code-block::

   ObsClient.createPostSignatureSync(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                          |
   +=================+=================+====================+======================================================================================================================================================================================+
   | Bucket          | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Bucket name.                                                                                                                                                                         |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                     |
   |                 |                 |                    | -  A bucket name:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                         |
   |                 |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                          |
   |                 |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                           |
   |                 |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                      |
   |                 |                 |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                            |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request. |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | The value can contain 3 to 63 characters.                                                                                                                                            |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key             | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Object name An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name.                   |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | The value can contain 1 to 1,024 characters.                                                                                                                                         |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Expires         | Number          | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Validity period of authentication for a browser-based upload                                                                                                                         |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | A positive integer, in seconds                                                                                                                                                       |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | 300                                                                                                                                                                                  |
   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | FormParams      | Object          | No                 | **Explanation:**                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | Parameters used for browser-based uploads, excluding **key**, **policy**, and **signature**.                                                                                         |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Value range**:                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | -  acl                                                                                                                                                                               |
   |                 |                 |                    | -  cache-control                                                                                                                                                                     |
   |                 |                 |                    | -  content-type                                                                                                                                                                      |
   |                 |                 |                    | -  content-disposition                                                                                                                                                               |
   |                 |                 |                    | -  content-encoding                                                                                                                                                                  |
   |                 |                 |                    | -  expires                                                                                                                                                                           |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | **Default value**:                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                      |
   |                 |                 |                    | None                                                                                                                                                                                 |
   +-----------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 2** Responses

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                            |
   +=======================+=======================+========================================================================================+
   | OriginPolicy          | String                | **Explanation:**                                                                       |
   |                       |                       |                                                                                        |
   |                       |                       | **policy** not encoded using Base64. This parameter can only be used for verification. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+
   | Policy                | String                | **Explanation:**                                                                       |
   |                       |                       |                                                                                        |
   |                       |                       | **policy** in the form.                                                                |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+
   | Signature             | String                | **Explanation:**                                                                       |
   |                       |                       |                                                                                        |
   |                       |                       | **signature** in the form.                                                             |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------+

Code Examples
-------------

The following sample code shows how to generate the parameters in a browser-based upload request.

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

   function createSignedUrlSync() {
     const params = {
       // Specify the bucket name.
       Bucket: "examplebucket",
       // Specify an object (example/objectname in this example).
       Key: "example/objectname",
       // Specify the validity period of the signed URL, in seconds (3600 in this example).
       Expires: 3600,
       // Specify the headers that must be carried in the request.
       FormParams: {
         'x-obs-acl': 'public-read',
         'content-type': 'text/plain'
       }
     };
     // Create a signed URL for uploading an object.
     const res = obsClient.createPostSignatureSync(params);
     console.log("OriginPolicy : %s", res.OriginPolicy);
     console.log("Policy: %s", res.Policy);
     console.log("Signature: %v", res.Signature);
   };

   createSignedUrlSync()

Code of an HTML form example is as follows:

.. code-block::

   <html>
   <head>
   <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
   </head>
   <body>

   <form action="http://bucketname.your-endpoint/" method="post" enctype="multipart/form-data">
   Object key
   <!-- Object name -->
   <input type="text" name="key" value="objectname" />
   <p>
   ACL
   <!-- Object ACL -->
   <input type="text" name="x-obs-acl" value="public-read" />
   <p>
   Content-Type
   <!-- Object MIME type -->
   <input type="text" name="content-type" value="text/plain" />
   <p>
   <!-- Base64 code of the policy -->
   <input type="hidden" name="policy" value="*** Provide your policy ***" />
   <!-- AK -->
   <input type="hidden" name="AccessKeyId" value="*** Provide your access key ***"/>
   <!-- Signature information -->
   <input type="hidden" name="signature" value="*** Provide your signature ***"/>

   <input name="file" type="file" />
   <input name="submit" value="Upload" type="submit" />
   </form>
   </body>
   </html>
