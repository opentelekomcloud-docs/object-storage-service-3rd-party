:original_name: obs_22_1613.html

.. _obs_22_1613:

How Do I Obtain an Object URL? (Python SDK)
===========================================

:ref:`After setting an ACL to grant anonymous users the read permission for an object in a bucket <obs_22_1607>`, you can download this object using its URL. Methods to obtain the object URL are as follows:

Method 1: Query by calling the API. After an object is uploaded by calling **ObsClient.putContent** or **ObsClient.putFile**, **PutContentResponse** is returned. You can call **objectUrl** to obtain the URL of the uploaded object. Sample code is as follows:

.. code-block::

   # Import the module.
   from obs import ObsClient

   # Create an instance of ObsClient.
   obsClient = ObsClient(
       access_key_id=os.getenv("AccessKeyID"),
       secret_access_key=os.getenv("SecretAccessKey"),
       server='https://your-endpoint'
   )
   resp = obsClient.putContent('bucketname', 'objectname', content='Hello OBS')

   if resp.status < 300:
       print('requestId:', resp.requestId)
       print('objectUrl:', resp.body.objectUrl)
   else:
       print('requestId:', resp.requestId)
       print('errorCode:', resp.errorCode)

Method 2: Compose the URL in the format of **https://**\ *Bucket name*.\ *Domain name*/*Directory level*/*Object name*.

.. note::

   -  If the object resides in the root directory of a bucket, its URL does not contain a directory level.
