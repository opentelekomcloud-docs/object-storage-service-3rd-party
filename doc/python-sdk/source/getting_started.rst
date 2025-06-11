:original_name: obs_22_0500.html

.. _obs_22_0500:

Getting Started
===============

Creating an AK and SK
---------------------

OBS employs access keys (AK and SK) for signature verification to ensure that only authorized accounts can access specified OBS resources. Detailed explanations of access keys are as follows:

-  AK is short for Access Key ID. One AK maps to only one user but one user can have multiple AKs. OBS authenticates users by their AKs.
-  SK is short for Secret Access Key, which is used to access OBS. You can generate authentication information based on SKs and request headers. An SK maps to an AK, and they group into a pair.

Access keys are permanent. There are also temporary security credentials (consisting of an AK/SK pair and a security token). Each user can create a maximum of two valid AK/SK pairs. Temporary security credentials can only be used to access OBS within the specified validity period. Once they expire, they must be requested again. For security purposes, you are advised to use temporary security credentials to access OBS. If you want to use permanent access keys, periodically update them.

-  To get permanent access keys, do as follows:

   #. Log in to the management console.
   #. In the upper right corner, hover your cursor over the username and choose **My Credentials**.
   #. On the **My Credentials** page, click **Access Keys** in the navigation pane.
   #. On the **Access Keys** page, click **Create Access Key**.
   #. In the **Create Access Key** dialog box, enter a description (recommended), and click **OK**.
   #. In the displayed dialog box, click **Download** to save the access keys to your browser's default download path.
   #. Open the downloaded **credentials.csv** file to obtain the access keys (AK and SK).

   .. note::

      -  In the **credentials.csv** file, the AK is the value in the **Access Key ID** column, and the SK is the one in the **Secret Access Key** column.
      -  Keep the access keys properly to prevent information leakage. If you click **Cancel** in the download dialog box, the access keys will not be downloaded and cannot be downloaded later. You can create new access keys if required.

-  To get temporary security credentials, refer to the following:

   Temporary security credentials are issued by the system and are only valid for 15 minutes to 24 hours. They follow the principle of least privilege. When using temporary security credentials, you must use an AK/SK pair and a security token together.

Obtaining Endpoints
-------------------

-  You can click `here <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__ to view the endpoints and regions enabled for OBS.

.. important::

   The SDK allows you to pass endpoints with or without the protocol name. Suppose the endpoint you obtained is **your-endpoint**. The endpoint passed when initializing an instance of **ObsClient** can be **http://your-endpoint**, **https://your-endpoint**, or **your-endpoint**.

Initializing an Instance of ObsClient
-------------------------------------

Each time you want to send an HTTP/HTTPS request to OBS, you must create an ObsClient instance. Sample code is as follows:

::

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
   # Use the instance to access OBS.

   # Close ObsClient.
   obsClient.close()

.. note::

   For more information, see chapter :ref:`Initialization <obs_22_0600>`.

   For details about log configuration, see :ref:`Log Initialization <obs_22_0603>`.

Creating a Bucket
-----------------

A bucket is a global namespace of OBS and is a data container. It functions as a root directory of a file system and can store objects.

This example creates a bucket named **examplebucket** and specifies its location, ACL, storage class, and redundancy type.

::

   from obs import CreateBucketHeader, HeadPermission
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
       # Add additional headers to specify a private bucket in the Standard storage class that supports multi-AZ storage.
       header = CreateBucketHeader(aclControl=HeadPermission.PRIVATE, storageClass="STANDARD", availableZone="3az")
       # Specify the region where the bucket is to be created. The region must be the same as that in the endpoint passed.
       location = "region"
       bucketName = "examplebucket"
       # Create a bucket.
       resp = obsClient.createBucket(bucketName, header, location)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Create Bucket Succeeded')
           print('requestId:', resp.requestId)
       else:
           print('Create Bucket Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Create Bucket Failed')
       print(traceback.format_exc())

.. note::

   -  Bucket names are globally unique. Ensure that the bucket you create is named differently from any other bucket.
   -  A bucket name:

      -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.
      -  Cannot be formatted as an IP address.
      -  Cannot start or end with a hyphen (-) or period (.).
      -  Cannot contain two consecutive periods (..), for example, **my..bucket**.
      -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.

   -  If you repeatedly create buckets of the same name, no error will be reported and the bucket attributes comply with those specified in the first creation request.
   -  For more information, see :ref:`Creating a Bucket <obs_22_0801>`.

Uploading an Object
-------------------

This example uploads a text.

::

   from obs import ObsClient
   import os
   import traceback

   # Obtain an AK and SK pair using environment variables or import the AK and SK pair in other ways. Using hard coding may result in leakage.
   # Obtain an AK and SK pair on the management console.
   # Before running the sample code, ensure that the environment variables AccessKeyID and SecretAccessKey have been configured.
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
       # Specify the text to be uploaded.
       content = 'Hello OBS'
       # Upload the text.
       resp = obsClient.putContent(bucketName, objectKey, content)
       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
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

.. note::

   For more information, see :ref:`Object Upload Overview <obs_22_0501>`.
