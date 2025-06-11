:original_name: obs_22_0913.html

.. _obs_22_0913:

Downloading an Object - Obtaining the Download Progress
=======================================================

You can obtain the download progress when downloading an object in binary, streaming, file-based, or resumable mode.

This example returns the object download progress.

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

   # Obtain the download progress.
   def callback(transferredAmount, totalAmount, totalSeconds):
       # Obtain the average download rate (KB/s).
       print(transferredAmount * 1.0 / totalSeconds / 1024)
       # Obtain the download progress in percentage.
       print(transferredAmount * 100.0 / totalAmount)

   try:
       bucketName="examplebucket"
       objectKey="objectname"
       # Download an object.
       resp = obsClient.getObject(bucketName=bucketName,objectKey=objectKey, progressCallback=callback)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Get Object Succeeded')
           print('requestId:', resp.requestId)
           # Read the object content.
           while True:
               chunk = resp.body.response.read(65536)
               if not chunk:
                   break
               print(chunk)
           resp.body.response.close()
       else:
           print('Get Object Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Get Object Failed')
       print(traceback.format_exc())
