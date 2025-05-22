:original_name: obs_22_0919.html

.. _obs_22_0919:

Batch Deleting Objects (SDK for Python)
=======================================

Function
--------

This API deletes objects in a batch from a specific bucket. Deleted objects cannot be restored.

OBS does not involve folders like in a file system. All elements stored in OBS buckets are objects. A folder you see on the console or other tools in OBS is essentially an object whose size is 0 and whose name ends with a slash (/). To delete a folder, you need to list all objects whose names are prefixed with the folder name and then call the batch deletion API.

In a batch delete operation, OBS concurrently deletes the specified objects and returns the deletion result of each object.

Restrictions
------------

-  To delete objects in a batch, you must be the bucket owner or have the required permission (**obs:object:DeleteObject** in IAM or **DeleteObject** in a bucket policy).
-  If versioning is not enabled for a bucket, deleted objects cannot be recovered.
-  A maximum of 1,000 objects can be deleted at a time. If you send a request for deleting more than 1,000 objects, OBS returns an error message.
-  After concurrent tasks are assigned, if an internal error occurs during cyclic deletion of multiple objects, an object may be deleted in the index data but still exist in the metadata.

Method
------

.. code-block::

   ObsClient.deleteObjects(bucketName, deleteObjectsRequest, extensionHeaders)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +----------------------+---------------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter            | Type                                                                            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +======================+=================================================================================+====================+===================================================================================================================================================================================+
   | bucketName           | str                                                                             | Yes                | **Explanation:**                                                                                                                                                                  |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | Bucket name                                                                                                                                                                       |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | **Restrictions:**                                                                                                                                                                 |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                      |                                                                                 |                    | -  A bucket name:                                                                                                                                                                 |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                      |                                                                                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                      |                                                                                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                      |                                                                                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                      |                                                                                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket properties comply with those set in the first creation request. |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | **Default value**:                                                                                                                                                                |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | None                                                                                                                                                                              |
   +----------------------+---------------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | deleteObjectsRequest | :ref:`DeleteObjectsRequest <obs_22_0919__en-us_topic_0142814657_table14455523>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | Request parameters of deleting objects in a batch For details, see :ref:`Table 2 <obs_22_0919__en-us_topic_0142814657_table14455523>`.                                            |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | **Default value**:                                                                                                                                                                |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | None                                                                                                                                                                              |
   +----------------------+---------------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | extensionHeaders     | dict                                                                            | No                 | **Explanation:**                                                                                                                                                                  |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | Extension headers.                                                                                                                                                                |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | **Value range**:                                                                                                                                                                  |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | See :ref:`User-defined Header (SDK for Python) <obs_22_1305>`.                                                                                                                    |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | **Default value**:                                                                                                                                                                |
   |                      |                                                                                 |                    |                                                                                                                                                                                   |
   |                      |                                                                                 |                    | None                                                                                                                                                                              |
   +----------------------+---------------------------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_22_0919__en-us_topic_0142814657_table14455523:

.. table:: **Table 2** DeleteObjectsRequest

   +-----------------+----------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                     | Mandatory (Yes/No) | Description                                                                                        |
   +=================+==========================================================+====================+====================================================================================================+
   | quiet           | bool                                                     | No                 | **Explanation:**                                                                                   |
   |                 |                                                          |                    |                                                                                                    |
   |                 |                                                          |                    | Response mode to the request for deleting objects in a batch                                       |
   |                 |                                                          |                    |                                                                                                    |
   |                 |                                                          |                    | **Value range**:                                                                                   |
   |                 |                                                          |                    |                                                                                                    |
   |                 |                                                          |                    | -  **False**: The detailed mode. Results of both successful and failed deletions are returned.     |
   |                 |                                                          |                    | -  **True**: The quiet mode. Only results of failed deletions are returned.                        |
   |                 |                                                          |                    |                                                                                                    |
   |                 |                                                          |                    | **Default value**:                                                                                 |
   |                 |                                                          |                    |                                                                                                    |
   |                 |                                                          |                    | False                                                                                              |
   +-----------------+----------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------+
   | objects         | list of :ref:`Object <obs_22_0919__table17374640193513>` | Yes                | **Explanation:**                                                                                   |
   |                 |                                                          |                    |                                                                                                    |
   |                 |                                                          |                    | List of objects to be deleted. For details, see :ref:`Table 3 <obs_22_0919__table17374640193513>`. |
   |                 |                                                          |                    |                                                                                                    |
   |                 |                                                          |                    | **Default value**:                                                                                 |
   |                 |                                                          |                    |                                                                                                    |
   |                 |                                                          |                    | None                                                                                               |
   +-----------------+----------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------+

.. _obs_22_0919__table17374640193513:

.. table:: **Table 3** Object

   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                                                                           |
   +=================+=================+====================+=======================================================================================================================================================+
   | key             | str             | Yes                | **Explanation:**                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name. |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | **Value range**:                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                         |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | **Default value**:                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | None                                                                                                                                                  |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | versionId       | str             | No                 | **Explanation:**                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | Object version ID, for example, **G001117FCE89978B0000401205D5DC9**                                                                                   |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | **Value range**:                                                                                                                                      |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | The value must contain 32 characters.                                                                                                                 |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | **Default value**:                                                                                                                                    |
   |                 |                 |                    |                                                                                                                                                       |
   |                 |                 |                    | None. If this parameter is left blank, the latest version of the object is deleted.                                                                   |
   +-----------------+-----------------+--------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 4** List of returned results

   +---------------------------------------------------+-----------------------------------+
   | Type                                              | Description                       |
   +===================================================+===================================+
   | :ref:`GetResult <obs_22_0919__table133284282414>` | **Explanation:**                  |
   |                                                   |                                   |
   |                                                   | SDK common results                |
   +---------------------------------------------------+-----------------------------------+

.. _obs_22_0919__table133284282414:

.. table:: **Table 5** GetResult

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                                                        |
   +=======================+=======================+====================================================================================================================================================================================================================================================================================================================================+
   | status                | int                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | HTTP status code                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Value range**:                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | A status code is a group of digits ranging from 2\ *xx* (indicating successes) to 4\ *xx* or 5\ *xx* (indicating errors). It indicates the status of a response.                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | reason                | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Reason description.                                                                                                                                                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | errorCode             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Error code returned by the OBS server. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | errorMessage          | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Error message returned by the OBS server. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | requestId             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Request ID returned by the OBS server                                                                                                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | indicator             | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Error indicator returned by the OBS server.                                                                                                                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hostId                | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Requested server ID. If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource              | str                   | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Error source (a bucket or an object). If the value of **status** is less than **300**, this parameter is left blank.                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | header                | list                  | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Response header list, composed of tuples. Each tuple consists of two elements, respectively corresponding to the key and value of a response header.                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | body                  | object                | **Explanation:**                                                                                                                                                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | Result content returned after the operation is successful. If the value of **status** is larger than **300**, the value of **body** is null. The value varies with the API being called. For details, see :ref:`Bucket-Related APIs (SDK for Python) <obs_22_0800>` and :ref:`Object-Related APIs (SDK for Python) <obs_22_0900>`. |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 6** GetResult.body

   +--------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | GetResult.body Type                                          | Description                                                                                                                       |
   +==============================================================+===================================================================================================================================+
   | :ref:`DeleteObjectResponse <obs_22_0919__table127195379360>` | **Explanation:**                                                                                                                  |
   |                                                              |                                                                                                                                   |
   |                                                              | Response results of the request for deleting objects in a batch For details, see :ref:`Table 7 <obs_22_0919__table127195379360>`. |
   +--------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+

.. _obs_22_0919__table127195379360:

.. table:: **Table 7** DeleteObjectResponse

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                         |
   +=======================+=======================+=====================================================================================+
   | deleteMarker          | bool                  | **Explanation:**                                                                    |
   |                       |                       |                                                                                     |
   |                       |                       | Whether the deleted object is a delete marker                                       |
   |                       |                       |                                                                                     |
   |                       |                       | **Value range**:                                                                    |
   |                       |                       |                                                                                     |
   |                       |                       | -  **true**: The deleted object is a delete marker.                                 |
   |                       |                       | -  **false**: The deleted object is not a delete marker.                            |
   |                       |                       |                                                                                     |
   |                       |                       | **Default value**:                                                                  |
   |                       |                       |                                                                                     |
   |                       |                       | false                                                                               |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------+
   | versionId             | str                   | **Explanation:**                                                                    |
   |                       |                       |                                                                                     |
   |                       |                       | Object version ID, for example, **G001117FCE89978B0000401205D5DC9**                 |
   |                       |                       |                                                                                     |
   |                       |                       | **Value range**:                                                                    |
   |                       |                       |                                                                                     |
   |                       |                       | The value must contain 32 characters.                                               |
   |                       |                       |                                                                                     |
   |                       |                       | **Default value**:                                                                  |
   |                       |                       |                                                                                     |
   |                       |                       | None. If this parameter is left blank, the latest version of the object is deleted. |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------+

Code Examples
-------------

This example deletes objects **objectkey1** and **objectkey2** from bucket **examplebucket** in a batch.

::

   from obs import ObsClient
   import os
   from obs import DeleteObjectsRequest
   from obs import Object
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
       # Specify the objects to be deleted in a batch.
       object1 = Object(key='objectkey1', versionId=None)
       object2 = Object(key='objectkey2', versionId=None)

   # Specify encoding_type when the object name contains special characters.
       encoding_type = 'url'
       bucketName = "examplebucket"
       # Batch delete the objects.
       resp = obsClient.deleteObjects(bucketName, DeleteObjectsRequest(quiet=False, objects=[object1, object2],
                                                                       encoding_type=encoding_type))

       # If status code 2xx is returned, the API is called successfully. Otherwise, the API call fails.
       if resp.status < 300:
           print('Delete Objects Succeeded')
           print('requestId:', resp.requestId)
           if resp.body.deleted:
               index = 1
               for delete in resp.body.deleted:
                   print('delete[' + str(index) + ']')
                   print('key:', delete.key, ',deleteMarker:', delete.deleteMarker, ',deleteMarkerVersionId:',
                         delete.deleteMarkerVersionId)
                   print('versionId:', delete.versionId)
                   index += 1
           if resp.body.error:
               index = 1
               for err in resp.body.error:
                   print('err[' + str(index) + ']')
                   print('key:', err.key, ',code:', err.code, ',message:', err.message)
                   print('versionId:', err.versionId)
                   index += 1
       else:
           print('Delete Objects Failed')
           print('requestId:', resp.requestId)
           print('errorCode:', resp.errorCode)
           print('errorMessage:', resp.errorMessage)
   except:
       print('Delete Objects Failed')
       print(traceback.format_exc())

This example deletes all objects prefixed with **test/** in bucket **examplebucket**.

.. warning::

   In the example below, if the value of **prefix** is an empty string or NULL, all files in the bucket will be deleted.

.. code-block::

   from obs import ObsClient
   import os
   from obs import DeleteObjectsRequest
   from obs import Object
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
       # Specify the folder to be deleted.
       prefix = 'test/'
       # Specify the maximum number of objects to be listed at a time. 1000 is used in this example.
       max_num = 1000
       mark = None
       index = 1
       failed_list = []
       while True:
           resp = obsClient.listObjects(bucketName=bucketName, prefix=prefix, marker=mark, max_keys=max_num,
                                        encoding_type='url')
           if resp.status < 300:
               need_to_delete_objects = [Object(key=i["key"], versionId=None) for i in resp.body["contents"]]
               del_resp = obsClient.deleteObjects(bucketName,
                                                  DeleteObjectsRequest(False, need_to_delete_objects, encoding_type="url"))
               for delete in del_resp.body.deleted:
                   print("Successfully deleted %s " % delete.key)
                   index += 1
               if del_resp.body.error:
                   for err in del_resp.body.error:
                       print("Failed to delete %s" % err.key)
                       failed_list.append(err.key)
               if resp.body.is_truncated is True:
                   mark = resp.body.next_marker
               else:
                   break
           else:
               print('errorCode:', resp.errorCode)
               print('errorMessage:', resp.errorMessage)
               break
       print("Total deleted %s objects" % index)
       for i in failed_list:
           print("Failed to delete %s, please try again" % i)
   except:
       print('Delete Objects Failed')
       print(traceback.format_exc())
