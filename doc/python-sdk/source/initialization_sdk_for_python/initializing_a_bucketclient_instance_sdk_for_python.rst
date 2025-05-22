:original_name: obs_22_0602.html

.. _obs_22_0602:

Initializing a BucketClient Instance (SDK for Python)
=====================================================

Function
--------

BucketClient functions as the Python client for accessing an OBS bucket. It offers users a series of APIs for interaction with OBS. These APIs are used for managing resources, such as buckets and objects, stored in OBS.

Except for **ObsClient.listBuckets**, **ObsClient.downloadFile**, **Obsclient.uploadFile**, **ObsClient.createPostSignature**, and **ObsClient.createSignedUrl**, **BucketClient** implements the same APIs as **ObsClient**, including the same functions and parameters, with the **bucketName** parameter omitted.

Method
------

.. code-block::

   obsClient.bucketClient(
       bucketName='*** Your Bucket Name ***'
   )

Constructor Parameter Description
---------------------------------

+-------------+------+--------------------+-----------------------------------------+
| Parameter   | Type | Mandatory (Yes/No) | Description                             |
+=============+======+====================+=========================================+
| bucket_name | str  | Yes                | Name of the bucket client to be created |
+-------------+------+--------------------+-----------------------------------------+

Code Examples
-------------

.. code-block::

   # Import the module.
   from obs import ObsClient

   # Obtain an AK and SK pair using environment variables or import the AK and SK pair in other ways. Using hard coding may result in leakage.
   # Obtain an AK and SK pair on the management console.
   ak = os.getenv("AccessKeyID")
   sk = os.getenv("SecretAccessKey")
   # (Optional) If you use a temporary AK and SK pair and a security token to access OBS, obtain them from environment variables.
   security_token = os.getenv("SecurityToken")
   # Set server to the endpoint of the region where the bucket is located.
   server = "https://your-endpoint"

   # Create an obsClient instance.
   # If you use a temporary AK and SK pair and a security token to access OBS, you must specify security_token when creating an instance.
   obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)

   # Create an instance of BucketClient.
   bucketClient = obsClient.bucketClient('bucketname')
   # Create a Bucket.
   resp = bucketClient.createBucket()
   if resp.status < 300:
       print('requestId:', resp.requestId)
   else:
       print('errorCode:', resp.errorCode)
       print('errorMessage:', resp.errorMessage)

.. note::

   Except for **ObsClient.listBuckets**, **ObsClient.downloadFile**, **Obsclient.uploadFile**, **ObsClient.createPostSignature**, and **ObsClient.createSignedUrl**, **BucketClient** can implement the same APIs as **ObsClient**, including the same functions and parameters, with the **bucketName** parameter omitted.
