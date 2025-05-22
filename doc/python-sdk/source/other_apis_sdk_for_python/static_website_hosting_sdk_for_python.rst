:original_name: obs_22_1304.html

.. _obs_22_1304:

Static Website Hosting (SDK for Python)
=======================================

Function
--------

This API uploads the files of the static website to your bucket in OBS as objects and configures the **public-read** permission on the files, and then configures the static website hosting mode for your bucket to host your static websites in OBS. After this, when third-party users access your websites, they actually access the objects in your bucket in OBS. When using static website hosting, you can configure request redirection to redirect specific or all requests.

Restrictions
------------

-  To upload an object, you must have the **obs:object:PutObject** permission.

Uploading a Website File to a Bucket
------------------------------------

1. Upload the website files to your bucket in OBS as objects and set the MIME type for the objects.

2. Set the ACL for the objects to **public-read**.

3. Access the objects using a browser.

This example uploads an HTML website file to a bucket and grants the public read permission for the object to implement static website hosting.

::

   from obs import ObsClient
   import os
   from obs import PutObjectHeader
   from obs import HeadPermission
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
       bucketName = 'bucketname'
       # Specify a website file name.
       objectKey = 'test.html'
   # Specify the path of a local HTML website file.
       file_path = 'localfile.html'
       headers = PutObjectHeader()
       # Specify the MIME type for the object.
       headers.contentType = 'text/html'

       # Upload the object.
       resp = obsClient.putFile(bucketName, objectKey, file_path, headers=headers)

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Put File Succeeded')
           print('requestId:', resp.requestId)
          # Set the object ACL to public-read.
           resp2 = obsClient.setObjectAcl(bucketName, objectKey, aclControl=HeadPermission.PUBLIC_READ)
           if resp2.status < 300:
               print('Set Object Acl Succeeded')
               print('requestId:', resp2.requestId)
           else:
               print('Set Object Acl Failed')
               print('requestId:', resp2.requestId)
               print('errorCode:', resp2.errorCode)
               print('errorMessage:', resp2.errorMessage)
       else:
           print('Put File Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Put File Failed')
       print(traceback.format_exc())

.. note::

   You can use **https://**\ *bucketname*\ **.**\ *your-endpoint*\ **/test.html** in a browser to access files hosted using the sample code.

Configuring Static Website Hosting
----------------------------------

This example configures static website hosting for bucket **examplebucket**.

::

   from obs import ObsClient
   from obs import WebsiteConfiguration
   from obs import IndexDocument
   from obs import ErrorDocument
   from obs import RoutingRule
   from obs import Condition
   from obs import Redirect
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
       # Specify an error page when a 4XX error occurs.
       errorDocument = ErrorDocument(key='error.html')
       # Specify a default page.
       indexDocument = IndexDocument(suffix='index.html')
       # Specify a rule for redirecting requests to NotFound.html if the status code is 404.
       routingRule1 = RoutingRule(condition=Condition(httpErrorCodeReturnedEquals=404),
                                  redirect=Redirect(protocol='http', replaceKeyWith='NotFound.html'))
       # Configure the redirection rules in list format. Multiple rules can be configured.
       routingRules = [routingRule1]
       bucketName = "examplebucket"
       # Configure static website hosting for the bucket.
       resp = obsClient.setBucketWebsite(bucketName,
                                         WebsiteConfiguration(errorDocument=errorDocument, indexDocument=indexDocument,
                                                              routingRules=routingRules))

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Set Bucket Website Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Set Bucket Website Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Set Bucket Website Failed')
       print(traceback.format_exc())

This example configures redirection for all requests.

::

   from obs import ObsClient
   import os
   import traceback
   from obs import WebsiteConfiguration
   from obs import RedirectAllRequestTo

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
       bucketName = 'bucketname'
       # Configure redirection for all requests.
       resp = obsClient.setBucketWebsite(bucketName,
                                          WebsiteConfiguration(
                                              redirectAllRequestTo=RedirectAllRequestTo(hostName='www.example.com',
                                                                                        protocol='http')))
       if resp.status < 300:
           print('Set Bucket Website Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Set Bucket Website Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Set Bucket Website Failed')
       print(traceback.format_exc())

Viewing Static Website Hosting
------------------------------

This example returns the static website hosting configuration of bucket **examplebucket**.

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
       bucketName="examplebucket"
       # Obtain the static website configuration of the bucket.
       resp = obsClient.getBucketWebsite(bucketName)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Get Bucket Website Succeeded')
           print('requestId:', resp.requestId)
           if resp.body.redirectAllRequestTo:
               print('redirectAllRequestTo.hostName:', resp.body.redirectAllRequestTo.hostName,
                     ',redirectAllRequestTo.protocol:', resp.body.redirectAllRequestTo.protocol)
           if resp.body.indexDocument:
               print('indexDocument.suffix:', resp.body.indexDocument.suffix)
           if resp.body.errorDocument:
               print('errorDocument.key:', resp.body.errorDocument.key)
           if resp.body.routingRules:
               index = 1
               for rout in resp.body.routingRules:
                   print('routingRule[', index, ']:')
                   index += 1
                   print('condition.keyPrefixEquals:', rout.condition.keyPrefixEquals,
                         ',condition.httpErrorCodeReturnedEquals:', rout.condition.httpErrorCodeReturnedEquals)
                   print('redirect.protocol:', rout.redirect.protocol, ',redirect.hostName:', rout.redirect.hostName,
                         ',redirect.replaceKeyPrefixWith:', rout.redirect.replaceKeyPrefixWith,
                         ',redirect.replaceKeyWith:', rout.redirect.replaceKeyWith, ',redirect.httpRedirectCode:',
                         rout.redirect.httpRedirectCode)
       else:
           print('Get Bucket Website Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Get Bucket Website Failed')
       print(traceback.format_exc())

Deleting Static Website Hosting
-------------------------------

This example deletes the static website hosting configuration of bucket **examplebucket**.

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
       # Delete the static website hosting configuration of the bucket.
       resp = obsClient.deleteBucketWebsite(bucketName)

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Delete Bucket Website Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Delete Bucket Website Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Delete Bucket Website Failed')
       print(traceback.format_exc())
