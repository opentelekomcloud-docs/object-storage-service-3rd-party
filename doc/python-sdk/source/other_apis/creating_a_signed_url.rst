:original_name: obs_22_1301.html

.. _obs_22_1301:

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

.. code-block::

   ObsClient.createSignedUrl(method, bucketName, objectKey, specialParam, expires, headers, queryParams)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +=================+=================+====================+===================================================================================================================================================================================+
   | method          | str             | Yes                | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | HTTP methods                                                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  GET                                                                                                                                                                            |
   |                 |                 |                    | -  POST                                                                                                                                                                           |
   |                 |                 |                    | -  PUT                                                                                                                                                                            |
   |                 |                 |                    | -  DELETE                                                                                                                                                                         |
   |                 |                 |                    | -  HEAD                                                                                                                                                                           |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bucketName      | str             | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Bucket name                                                                                                                                                                       |
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
   | objectKey       | str             | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                             |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                                                     |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | specialParam    | str             | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Special operator, which indicates the sub-resource to be operated                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  versions                                                                                                                                                                       |
   |                 |                 |                    | -  uploads                                                                                                                                                                        |
   |                 |                 |                    | -  location                                                                                                                                                                       |
   |                 |                 |                    | -  storageinfo                                                                                                                                                                    |
   |                 |                 |                    | -  quota                                                                                                                                                                          |
   |                 |                 |                    | -  storagePolicy                                                                                                                                                                  |
   |                 |                 |                    | -  acl                                                                                                                                                                            |
   |                 |                 |                    | -  append                                                                                                                                                                         |
   |                 |                 |                    | -  logging                                                                                                                                                                        |
   |                 |                 |                    | -  policy                                                                                                                                                                         |
   |                 |                 |                    | -  lifecycle                                                                                                                                                                      |
   |                 |                 |                    | -  website                                                                                                                                                                        |
   |                 |                 |                    | -  versioning                                                                                                                                                                     |
   |                 |                 |                    | -  cors                                                                                                                                                                           |
   |                 |                 |                    | -  notification                                                                                                                                                                   |
   |                 |                 |                    | -  tagging                                                                                                                                                                        |
   |                 |                 |                    | -  delete                                                                                                                                                                         |
   |                 |                 |                    | -  restore                                                                                                                                                                        |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | expires         | int             | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Expiration time of the signed URL                                                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Value range**:                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | -  The value of this parameter for temporary credentials ranges from **0** to **86400**, in seconds.                                                                              |
   |                 |                 |                    | -  The value of this parameter for permanent keys ranges from **0** to **630720000**, in seconds.                                                                                 |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | 300                                                                                                                                                                               |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | headers         | dict            | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Headers in the request                                                                                                                                                            |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | queryParams     | dict            | No                 | **Explanation:**                                                                                                                                                                  |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | Query parameters in the request                                                                                                                                                   |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | **Default value**:                                                                                                                                                                |
   |                 |                 |                    |                                                                                                                                                                                   |
   |                 |                 |                    | None                                                                                                                                                                              |
   +-----------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. caution::

   If a CORS or signature mismatch error occurs, refer to the following steps to troubleshoot the issue:

   #. If CORS is not configured, you need to configure CORS rules on OBS Console.
   #. If the signatures do not match, check whether signature parameters are correct. For example, during an object upload, the backend uses **Content-Type** to calculate the signature and generate an authorized URL, but if **Content-Type** is not set or is set to an incorrect value when the frontend uses the authorized URL, a CORS error occurs. To avoid this issue, ensure that **Content-Type** fields at both the frontend and backend are kept consistent.

Responses
---------

.. table:: **Table 2** List of returned results

   +----------------------------+-----------------------+-----------------------------------------------------------------+
   | Parameter                  | Type                  | Description                                                     |
   +============================+=======================+=================================================================+
   | signedUrl                  | str                   | **Explanation:**                                                |
   |                            |                       |                                                                 |
   |                            |                       | Signed URL                                                      |
   |                            |                       |                                                                 |
   |                            |                       | **Default value**:                                              |
   |                            |                       |                                                                 |
   |                            |                       | None                                                            |
   +----------------------------+-----------------------+-----------------------------------------------------------------+
   | actualSignedRequestHeaders | dict                  | **Explanation:**                                                |
   |                            |                       |                                                                 |
   |                            |                       | Actual headers in the request initiated by using the signed URL |
   |                            |                       |                                                                 |
   |                            |                       | **Default value**:                                              |
   |                            |                       |                                                                 |
   |                            |                       | None                                                            |
   +----------------------------+-----------------------+-----------------------------------------------------------------+

Code Examples
-------------

This example creates temporary signed URLs.

::

   from obs import ObsClient
   import os
   import traceback
   import base64

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
       # Create a signed URL for creating a bucket.
       res1 = obsClient.createSignedUrl(method='PUT', bucketName='bucketname', expires=3600)
       print('signedUrl:', res1.signedUrl)
       print('actualSignedRequestHeaders:', res1.actualSignedRequestHeaders)

       # Create a signed URL for uploading an object.
       res2 = obsClient.createSignedUrl(method='PUT', bucketName='bucketname', objectKey='objectkey', expires=3600,
                                        headers={'Content-Type': 'text/plain'})
       print('signedUrl:', res2.signedUrl)
       print('actualSignedRequestHeaders:', res2.actualSignedRequestHeaders)

       # Create a signed URL for setting an object ACL.
       res3 = obsClient.createSignedUrl(method='PUT', bucketName='bucketname', objectKey='objectkey', specialParam='acl',
                                        expires=3600, headers={'x-obs-acl': 'private'})
       print('signedUrl:', res3.signedUrl)
       print('actualSignedRequestHeaders:', res3.actualSignedRequestHeaders)

       # Create a signed URL for downloading an object.
       res4 = obsClient.createSignedUrl(method='GET', bucketName='bucketname', objectKey='objectkey', expires=3600)
       print('signedUrl:', res4.signedUrl)
       print('actualSignedRequestHeaders:', res4.actualSignedRequestHeaders)

       # Create a signed URL for deleting an object.
       res5 = obsClient.createSignedUrl(method='DELETE', bucketName='bucketname', objectKey='objectkey', expires=3600)
       print('signedUrl:', res5.signedUrl)
       print('actualSignedRequestHeaders:', res5.actualSignedRequestHeaders)

       # Create a signed URL for deleting a bucket.
       res6 = obsClient.createSignedUrl(method='DELETE', bucketName='bucketname', expires=3600)
       print('signedUrl:', res6.signedUrl)
       print('actualSignedRequestHeaders:', res6.actualSignedRequestHeaders)

       # Create a signed URL for initiating a multipart task.
       res7 = obsClient.createSignedUrl(method='POST', bucketName='bucketname', objectKey='objectkey',
                                        specialParam='uploads', expires=3600)
       print('signedUrl:', res7.signedUrl)
       print('actualSignedRequestHeaders:', res7.actualSignedRequestHeaders)

       # Create a signed URL for uploading a part.
       res8 = obsClient.createSignedUrl(method='PUT', bucketName='bucketname', objectKey='objectkey', expires=3600,
                                        queryParams={'partNumber': '1', 'uploadId': '00000*****'})
       print('signedUrl:', res8.signedUrl)
       print('actualSignedRequestHeaders:', res8.actualSignedRequestHeaders)

       # Create a signed URL for assembling parts.
       res9 = obsClient.createSignedUrl(method='POST', bucketName='bucketname', objectKey='objectkey', expires=3600,
                                        queryParams={'uploadId': '00000*****'})
       print('signedUrl:', res9.signedUrl)
       print('actualSignedRequestHeaders:', res9.actualSignedRequestHeaders)

       # Create a signed URL for image persistency.
       # Name of the bucket that stores the source object
       bucketName = 'originBucketName';
       # Source object name before the processing
       objectKey = 'test.png';

       # Name of the object after processing
       targetObjectName ="save.png"
       # (Optional) Name of the bucket that stores the new object
       targetBucketName ="saveBucketName"
       queryParams={}
       queryParams["x-image-process"]="image/resize,w_100"
       queryParams["x-image-save-object"]=base64.b64encode(targetObjectName .encode("utf-8")).decode()
       # Optional parameter
       queryParams["x-image-save-bucket"]=base64.b64encode(targetBucketName .encode("utf-8")).decode()

       res10 = obsClient.createSignedUrl(method='GET', bucketName=bucketName, objectKey=objectKey, queryParams=queryParams, expires=3600)
       print('signedUrl:', res10.signedUrl)
       print('actualSignedRequestHeaders:', res10.actualSignedRequestHeaders)
   except:
       print(traceback.format_exc())
