:original_name: obs_22_0907.html

.. _obs_22_0907:

Uploading an Object - Browser-Based
===================================

Function
--------

This API uploads an object up to 5 GB to a specified bucket in HTML form. You can call **ObsClient.createPostSignature** to generate parameters for requesting a browser-based upload. For details, see the following:

#. Call **ObsClient.createPostSignature** to generate request parameters for authentication.
#. Prepare an HTML form.
#. Enter the request parameters in the page.
#. Select a local file and upload it in browser-based mode.

.. note::

   There are two request parameters generated for authentication:

   -  **policy**, which corresponds to the **policy** parameter in the form.
   -  **signature**, which corresponds to the **signature** parameter in the form.

Restrictions
------------

-  To upload an object, you must be the bucket owner or have the required permission (**obs:object:PutObject** in IAM or **PutObject** in a bucket policy).

-  Values of **policy** and **signature** in the HTML form are obtained from the returned results of **ObsClient.createPostSignature**.

Method
------

.. code-block::

   ObsClient.createPostSignature(bucketName, objectKey, expires, formParams)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                                                     |
   +=================+=================+====================+=================================================================================================================================================================================================================================================================================+
   | bucketName      | str             | No                 | **Explanation:**                                                                                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | Bucket name                                                                                                                                                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Restrictions:**                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                                                                |
   |                 |                 |                    | -  A bucket name:                                                                                                                                                                                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                                                    |
   |                 |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                                                     |
   |                 |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                                                      |
   |                 |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                                                                 |
   |                 |                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                                                         |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket properties comply with those set in the first creation request.                                                                                               |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                            |
   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey       | str             | No                 | **Explanation:**                                                                                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                                                                                                                           |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                            |
   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | expires         | int             | No                 | **Explanation:**                                                                                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | Expiration time of authentication for a browser-based upload                                                                                                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | A positive integer, in seconds                                                                                                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | 300                                                                                                                                                                                                                                                                             |
   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | formParams      | dict            | No                 | **Explanation:**                                                                                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | Parameters of browser-based uploads, not including **key**, **policy**, and **signature**.                                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Value range**:                                                                                                                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | (When you use the following parameters, you must add the **x-obs** prefix to them. Taking **acl** as an example, it should be configured as **formParams['x-obs-acl']='public-read'**. To obtain the values of these parameters, see the response header descriptions in APIs.) |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | -  acl                                                                                                                                                                                                                                                                          |
   |                 |                 |                    | -  cache-control                                                                                                                                                                                                                                                                |
   |                 |                 |                    | -  content-type                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | -  content-disposition                                                                                                                                                                                                                                                          |
   |                 |                 |                    | -  content-encoding                                                                                                                                                                                                                                                             |
   |                 |                 |                    | -  expires                                                                                                                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | **Default value**:                                                                                                                                                                                                                                                              |
   |                 |                 |                    |                                                                                                                                                                                                                                                                                 |
   |                 |                 |                    | None                                                                                                                                                                                                                                                                            |
   +-----------------+-----------------+--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 2** List of returned results

   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                      |
   +=======================+=======================+==================================================================================================================================================================================================+
   | originPolicy          | str                   | **Explanation:**                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | Value of **Policy** that is not encoded by Base64. This parameter can only be used for verification. For example:                                                                                |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **{"expiration":"2023-09-12T12:52:59Z","conditions":[{"content-type":"text/plain"},{"bucket":"examplebucket"},{"key":"example/objectname"},]}"**                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | policy                | str                   | **Explanation:**                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | Value of **Policy** that is encoded by Base64. For example:                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **eyJleHBpcmF0aW9uIjoiMjAyMy0wOS0xMlQxMjo1Mjo1OVoiLCJjb25kaXRpb25zIjpbeyJjb250ZW50LXR5cGUiOiJ0ZXh0L3BsYWluIn0seyJidWNrZXQiOiJleGFtcGxlYnVja2V0In0seyJrZXkiOiJleGFtcGxlL29iamVjdG5hbWUifSxdfQ==** |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | signature             | str                   | **Explanation:**                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **signature** in the form For example:                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **g0jQr4v9VWd1Q2FOFDG6LGfV9Cw=**                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | **Default value**:                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                  |
   |                       |                       | None                                                                                                                                                                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example generates authentication parameters **policy** and **signature** for a browser-based upload.

::

   from obs import ObsClient
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
       bucketName = "examplebucket"
       objectKey = "objectname"
       # Configure the validity period (in seconds) for a browser-based upload request. 3600 is used as an example.
       expires = 3600
       # Specify parameters for a browser-based upload except key, policy, and signature. In this example, x-obs-acl is set to private and content-type is set to text/plain.
       formParams = {'x-obs-acl': 'private', 'content-type': 'text/plain'}
       # Create parameters for a browser-based upload.
       resp = obsClient.createPostSignature(bucketName, objectKey, expires, formParams)

       print('originPolicy:', resp.originPolicy)
       print('policy:', resp.policy)
       print('signature:', resp.signature)
   except:
       print(traceback.format_exc())

Code of an HTML form example is as follows:

::

   <html>
       <head>
           <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
       </head>
       <body>
           <form action="http://bucketname.your-endpoint/" method="post" enctype="multipart/form-data">
               <p>
                   Object key
               </p>
               <!-- Object name  -->
               <input type="text" name="key" value="objectname" />
               <p>
                   ACL
               </p>
               <!-- Object ACL -->
               <input type="text" name="x-obs-acl" value="private" />
               <p>
                   Content-Type
               </p>
               <!-- Object MIME type -->
               <input type="text" name="content-type" value="text/plain" />
               <p>
                   <!-- Base64-encoded policy -->
                   <input type="hidden" name="policy" value="*** Provide your policy ***" />
                   <!-- AK -->
                   <input type="hidden" name="AccessKeyId" value="*** Provide your access key ***"/>
                   <!-- Signature string information -->
                   <input type="hidden" name="signature" value="*** Provide your signature ***"/>
                   <input name="file" type="file" />
                   <input name="submit" value="Upload" type="submit" />
               </p>
           </form>
       </body>
   </html>

.. note::

   -  Values of **policy** and **signature** in the HTML form are obtained from the returned results of **ObsClient.createPostSignature**.
