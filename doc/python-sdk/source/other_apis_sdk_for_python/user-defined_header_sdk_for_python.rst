:original_name: obs_22_1305.html

.. _obs_22_1305:

User-defined Header (SDK for Python)
====================================

Function
--------

When calling an API, you can configure user-defined headers to meet specific needs. The SDK will automatically calculate the signature for the specified headers if needed.

Method:

You can add the specified headers in **extensionHeaders** in the dictionary format.

Code Examples
-------------

This example configures user-defined headers to use the single-connection bandwidth throttling function for downloading object **objectname** from bucket **examplebucket** at a limited rate.

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
       # Configure the download rate limit by specifying x-obs-traffic-limit, in bits. The value range is from 819200 (100 KB) to 838860800 (100 MB). 819200 is used as an example.
       extensionHeaders = {'x-obs-traffic-limit': 819200}
       # Specify the full path (localfile as an example) to which objects are downloaded. The full path contains the local file name.
       downloadPath = 'localfile'
       # Download the object at a limited rate.
       resp = obsClient.getObject(bucketName, objectKey, downloadPath, extensionHeaders=extensionHeaders)

       # If status code 2xx is returned, the API was called successfully. Otherwise, the call failed.
       if resp.status < 300:
           print('Get Object Succeeded')
           print('requestId:', resp.requestId)
           print('url:', resp.body.url)
       else:
           print('Get Object Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Get Object Failed')
       print(traceback.format_exc())

This example configures a user-defined header to implement the upload callback.

::

   from obs import ObsClient
   import os
   import traceback
   from urllib.parse import quote
   import base64
   import json

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
       # Specify a protocol.
       protocol = 'http://'

       # Specify the callback address. If the URL contains any special characters or full-width characters, they must be URL-encoded using quote(str).
       callbackUrl1 = protocol + quote("www.example.com/callback1")
       callbackUrl2 = protocol + quote ("www.example.com/full-width-characters?key=object-name-in-full-width-characters")
       # (Optional) Specify the value of the host header carried in the callback request. If this parameter is not specified, the value of host parsed from callbackUrl is used.
       callbackHost = 'www.example.com'
       # Specify the body of the callback request.
       callbackBody = 'key=$(key)&override=$(override)&size=$(size)&bucket=$(bucket)&etag=$(etag)'
       # Configure the upload callback.
       callBackPolicy = {"callbackBody": callbackBody, "callbackUrl": callbackUrl1 + ';' + callbackUrl2,
                         "callbackHost": callbackHost}

       # Configure the custom headers by specifying extensionHeaders. The input parameters are in the dictionary format.
       # Convert callBackPolicy to a JSON string and then to  binary using json.dumps().encode(). Then, encode the results using Base64 (base64.b64encode()) and convert the encoded data which is in binary mode to a string using str(b'str', "utf-8").
       extensionHeaders = {'x-obs-callback': str(base64.b64encode(json.dumps(callBackPolicy).encode()), "utf-8")}

       bucketName = 'your-bucketName'
       objectKey = 'example.txt'
       content = 'Hello OBS'
       # Upload the text and perform the upload callback.
       resp = obsClient.putContent(bucketName, objectKey, content, extensionHeaders=extensionHeaders)

       # If status code 2xx is returned, the API was called successfully. Otherwise, the call failed.
       if resp.status < 300:
           print('Put Content Succeeded')
           print('requestId:', resp.requestId)
           print('etag:', resp.body.etag)
       else:
           print('Put Content Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Put Content Failed')
       print(traceback.format_exc())

This example changes the expiration time of an object using a user-defined header.

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
       # x-obs-expires indicates how many days after the last modification the object expires. This example configures 3 days.
       extensionHeaders = {'x-obs-expires': 3}
       # Configure the object metadata.
       resp = obsClient.setObjectMetadata(bucketName, objectKey, extensionHeaders=extensionHeaders)

       # If status code 2xx is returned, the API was called successfully. Otherwise, the call failed.
       if resp.status < 300:
           print('Set Object Metadata Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Set Object Metadata Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Set Object Metadata Failed')
       print(traceback.format_exc())
