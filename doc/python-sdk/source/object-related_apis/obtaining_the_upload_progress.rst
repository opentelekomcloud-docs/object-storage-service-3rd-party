:original_name: obs_22_0906.html

.. _obs_22_0906:

Obtaining the Upload Progress
=============================

You can query the upload progress when uploading an object in streaming, file-based, multipart, appendable, or resumable mode.

This example configures a callback function to obtain the object upload progress.

Sample code is as follows:

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

   # Obtain the upload progress.
   def callback(transferredAmount, totalAmount, totalSeconds):
       # Obtain the average upload rate (KB/s).
       print(transferredAmount * 1.0 / totalSeconds / 1024)
       # Obtain the upload progress in percentage.
       print(transferredAmount * 100.0 / totalAmount)

   try:
       bucketName = "examplebucket"
       # Specify an object name (the name displayed after the file is uploaded to the bucket).
       objectKey = "objectname"
       # Specify the full path of the file to be uploaded, for example, aa/bb.txt.
       file_path = 'localfile'
       # Perform the file-based upload.
       resp = obsClient.putFile(bucketName, objectKey, file_path, progressCallback=callback)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Put File Succeeded')
           print('requestId:', resp.requestId)
           print('etag:', resp.body.etag)
           print('versionId:', resp.body.versionId)
           print('storageClass:', resp.body.storageClass)
       else:
           print('Put File Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Put File Failed')
       print(traceback.format_exc())
