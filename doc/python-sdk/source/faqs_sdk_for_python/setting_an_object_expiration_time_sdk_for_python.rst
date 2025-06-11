:original_name: obs_22_1704.html

.. _obs_22_1704:

Setting an Object Expiration Time (SDK for Python)
==================================================

This example sets the object expiration time using a header when uploading a file stream.

.. code-block::

   obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)
   try:
       # Read a file stream.
       content = open('localfile', 'rb')
       bucketName = "examplebucket"
       objectKey = "objectname"
       header=PutObjectHeader()
       #Set the expiration time.
       header.expires=10
       # Upload the file stream.
       resp = obsClient.putContent(bucketName, objectkey, content,headers=header)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Put Content Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Put Content Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print(traceback.format_exc())

This example sets the object expiration time using a user-defined header when uploading a file stream.

.. code-block::

   obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)
   try:
       # Read a file stream.
       content = open('localfile', 'rb')
       bucketName = "examplebucket"
       objectKey = "objectname"
       header=PutObjectHeader()
       # Use a user-defined header to set the expiration time.
       extensionHeaders = {'x-obs-expires': 30}
       # Upload the file stream.
       resp = obsClient.putContent(bucketName, objectkey, content,extensionHeaders=extensionHeaders)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Put Content Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Put Content Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print(traceback.format_exc())

This example sets the expiration time for an uploaded object.

.. code-block::

   obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)
   try:
       bucketName = "examplebucket"
       objectKey = "objectname"
       # Use a user-defined header to set the expiration time.
       extensionHeaders = {'x-obs-expires': 30}
       # Configure metadata for the object.
       resp = obsClient.setObjectMetadata(bucketName, objectkey, extensionHeaders=extensionHeaders)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Set Object Metadata Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Set Object Metadata Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print(traceback.format_exc())
