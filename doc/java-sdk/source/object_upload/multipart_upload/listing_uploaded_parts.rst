:original_name: obs_21_0620.html

.. _obs_21_0620:

Listing Uploaded Parts
======================

Function
--------

This API lists the uploaded parts in a specified bucket. This request must contain the multipart upload ID.

You can list the uploaded parts of a specified multipart upload or of all ongoing multipart uploads. A maximum of 1,000 uploaded parts can be returned in a response. If your multipart upload has more than 1,000 parts, you need to send multiple requests to list all uploaded parts. Assembled parts will not be listed.

Restrictions
------------

-  To list uploaded parts, you must be the bucket owner or have the required permission (**obs:object:ListMultipartUploadParts** in IAM or **ListMultipartUploadParts** in a bucket policy).

Method
------

obsClient.listParts(:ref:`ListPartsRequest <obs_21_0620__table9747247160>` :ref:`request <obs_21_0620__table97462410166>`)

Request Parameters
------------------

.. _obs_21_0620__table97462410166:

.. table:: **Table 1** List of request parameters

   +-----------------+--------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                   | Mandatory (Yes/No) | Description                                                                                                    |
   +=================+========================================================+====================+================================================================================================================+
   | request         | :ref:`ListPartsRequest <obs_21_0620__table9747247160>` | Yes                | **Explanation:**                                                                                               |
   |                 |                                                        |                    |                                                                                                                |
   |                 |                                                        |                    | Request parameters for listing uploaded parts. For details, see :ref:`Table 2 <obs_21_0620__table9747247160>`. |
   +-----------------+--------------------------------------------------------+--------------------+----------------------------------------------------------------------------------------------------------------+

.. _obs_21_0620__table9747247160:

.. table:: **Table 2** ListPartsRequest

   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                                         |
   +==================+=================+====================+=====================================================================================================================================================================================================+
   | bucketName       | String          | Yes                | **Explanation:**                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | Bucket name.                                                                                                                                                                                        |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Restrictions:**                                                                                                                                                                                   |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                                    |
   |                  |                 |                    | -  A bucket name:                                                                                                                                                                                   |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                        |
   |                  |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                                         |
   |                  |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                          |
   |                  |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                     |
   |                  |                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                             |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.                   |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Default value**:                                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | None                                                                                                                                                                                                |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectKey        | String          | Yes                | **Explanation:**                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                                               |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Value range**:                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | The value must contain 1 to 1,024 characters.                                                                                                                                                       |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Default value**:                                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | None                                                                                                                                                                                                |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | uploadId         | String          | Yes                | **Explanation:**                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | Multipart upload ID, for example, **000001648453845DBB78F2340DD460D8**.                                                                                                                             |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Value range**:                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | The value must contain 1 to 32 characters.                                                                                                                                                          |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Default value**:                                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | None                                                                                                                                                                                                |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maxParts         | Integer         | No                 | **Explanation:**                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | Maximum number of parts that can be listed per page.                                                                                                                                                |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Restrictions:**                                                                                                                                                                                   |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | If the specified value is greater than **1000**, only 1,000 parts are returned.                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Value range**:                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | The value ranges from **1** to **1000**.                                                                                                                                                            |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Default value**:                                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **1000**                                                                                                                                                                                            |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | partNumberMarker | Integer         | No                 | **Explanation:**                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | Part number the listing starts from.                                                                                                                                                                |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Restrictions:**                                                                                                                                                                                   |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | OBS lists only parts with greater numbers than that specified by this parameter.                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Default value**:                                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | None                                                                                                                                                                                                |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | encodingType     | String          | No                 | **Explanation:**                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | Encoding type for **key** in the response. If **key** in the response contains control characters that are not supported by the XML 1.0 standard, you can specify this parameter to encode **key**. |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Value range**:                                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **url**                                                                                                                                                                                             |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | **Default value**:                                                                                                                                                                                  |
   |                  |                 |                    |                                                                                                                                                                                                     |
   |                  |                 |                    | None. If you leave this parameter blank, encoding is not applied.                                                                                                                                   |
   +------------------+-----------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** ListPartsResult

   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                     | Description                                                                                                                                                                                                                                  |
   +=======================+==========================================================+==============================================================================================================================================================================================================================================+
   | statusCode            | int                                                      | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | HTTP status code.                                                                                                                                                                                                                            |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Value range**:                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response.                                                                  |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | responseHeaders       | Map<String, Object>                                      | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | HTTP response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header.                                                                  |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bucket                | String                                                   | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Bucket name.                                                                                                                                                                                                                                 |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Restrictions:**                                                                                                                                                                                                                            |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                             |
   |                       |                                                          | -  A bucket name:                                                                                                                                                                                                                            |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                 |
   |                       |                                                          |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                  |
   |                       |                                                          |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                   |
   |                       |                                                          |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                              |
   |                       |                                                          |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                      |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.                                                            |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | key                   | String                                                   | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                                                                                        |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Value range**:                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | The value must contain 1 to 1,024 characters.                                                                                                                                                                                                |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | uploadId              | String                                                   | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Multipart upload ID, for example, **000001648453845DBB78F2340DD460D8**.                                                                                                                                                                      |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Value range**:                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | The value must contain 32 characters.                                                                                                                                                                                                        |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | initiator             | :ref:`Owner <obs_21_0620__table195631852884>`            | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Initiator of the multipart upload. For details, see :ref:`Table 6 <obs_21_0620__table195631852884>`.                                                                                                                                         |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | owner                 | :ref:`Owner <obs_21_0620__table195631852884>`            | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Owner of the multipart upload, which is consistent with **initiator**. For details, see :ref:`Table 6 <obs_21_0620__table195631852884>`.                                                                                                     |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | storageClass          | :ref:`StorageClassEnum <obs_21_0620__table877317471375>` | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Storage class of the object to be uploaded.                                                                                                                                                                                                  |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Value range**:                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | See :ref:`Table 5 <obs_21_0620__table877317471375>`.                                                                                                                                                                                         |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | multipartList         | List<:ref:`Multipart <obs_21_0620__table796713360494>`>  | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | List of uploaded parts. For details, see :ref:`Table 4 <obs_21_0620__table796713360494>`.                                                                                                                                                    |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maxParts              | Integer                                                  | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Maximum number of parts that can be listed per page, which is consistent with that set in the request.                                                                                                                                       |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Restrictions:**                                                                                                                                                                                                                            |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | If the specified value is greater than 1000, only 1,000 parts are returned.                                                                                                                                                                  |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Value range**:                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | The value ranges from 1 to 1000.                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | 1000                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | isTruncated           | boolean                                                  | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Whether all parts are returned in the response.                                                                                                                                                                                              |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Value range**:                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | -  **true**: Not all parts are returned.                                                                                                                                                                                                     |
   |                       |                                                          | -  **false**: All parts are returned.                                                                                                                                                                                                        |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | partNumberMarker      | String                                                   | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Part number after which part listing begins, which is consistent with that set in the request.                                                                                                                                               |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | nextPartNumberMarker  | String                                                   | **Explanation:**                                                                                                                                                                                                                             |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | Part number to start with for the next part listing request. If only part of the uploaded parts are returned for the current request, this parameter is included in the response for setting **partNumberMarker** in the subsequent request. |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | **Default value**:                                                                                                                                                                                                                           |
   |                       |                                                          |                                                                                                                                                                                                                                              |
   |                       |                                                          | None                                                                                                                                                                                                                                         |
   +-----------------------+----------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0620__table796713360494:

.. table:: **Table 4** Multipart

   +-----------------------+-----------------------+-----------------------------------------------------------+
   | Parameter             | Type                  | Description                                               |
   +=======================+=======================+===========================================================+
   | partNumber            | Integer               | **Explanation:**                                          |
   |                       |                       |                                                           |
   |                       |                       | Part number.                                              |
   |                       |                       |                                                           |
   |                       |                       | **Value range**:                                          |
   |                       |                       |                                                           |
   |                       |                       | An integer ranging from 1 to 10000.                       |
   |                       |                       |                                                           |
   |                       |                       | **Default value**:                                        |
   |                       |                       |                                                           |
   |                       |                       | None                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------+
   | lastModified          | Date                  | **Explanation:**                                          |
   |                       |                       |                                                           |
   |                       |                       | Last time the part was uploaded.                          |
   |                       |                       |                                                           |
   |                       |                       | **Default value**:                                        |
   |                       |                       |                                                           |
   |                       |                       | None                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------+
   | etag                  | String                | **Explanation:**                                          |
   |                       |                       |                                                           |
   |                       |                       | Part ETag. Base64-encoded, 128-bit MD5 value of the part. |
   |                       |                       |                                                           |
   |                       |                       | **Value range**:                                          |
   |                       |                       |                                                           |
   |                       |                       | The value must contain 32 characters.                     |
   |                       |                       |                                                           |
   |                       |                       | **Default value**:                                        |
   |                       |                       |                                                           |
   |                       |                       | None                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------+
   | size                  | Long                  | **Explanation:**                                          |
   |                       |                       |                                                           |
   |                       |                       | Part size.                                                |
   |                       |                       |                                                           |
   |                       |                       | **Default value**:                                        |
   |                       |                       |                                                           |
   |                       |                       | None                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------+

.. _obs_21_0620__table877317471375:

.. table:: **Table 5** StorageClassEnum

   ======== ============= ======================
   Constant Default Value Description
   ======== ============= ======================
   STANDARD STANDARD      Standard storage class
   WARM     WARM          Warm storage class.
   COLD     COLD          Cold storage class.
   ======== ============= ======================

.. _obs_21_0620__table195631852884:

.. table:: **Table 6** Owner

   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                                                                  |
   +=================+=================+====================+==============================================================================================+
   | id              | String          | Yes                | **Explanation:**                                                                             |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | Account (domain) ID of the bucket owner.                                                     |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | **Value range**:                                                                             |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>`   |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | **Default value**:                                                                           |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | None                                                                                         |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------+
   | displayName     | String          | No                 | **Explanation:**                                                                             |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | Account name of the owner.                                                                   |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | **Value range**:                                                                             |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | To obtain the account name, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>` |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | **Default value**:                                                                           |
   |                 |                 |                    |                                                                                              |
   |                 |                 |                    | None                                                                                         |
   +-----------------+-----------------+--------------------+----------------------------------------------------------------------------------------------+

Code Example: Listing Up to 1,000 Uploaded Parts
------------------------------------------------

This example lists up to 1,000 parts uploaded to object **objectname** in bucket **examplebucket** based on the upload ID obtained through **initiateMultipartUpload**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.ListPartsRequest;
   import com.obs.services.model.ListPartsResult;
   import com.obs.services.model.Multipart;
   public class ListParts001 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           String securityToken = System.getenv("SECURITY_TOKEN");
           // Enter the endpoint corresponding to the region where the bucket is to be created.
           String endPoint = "https://your-endpoint";
           // Obtain an endpoint using environment variables or import it in other ways.
           //String endPoint = System.getenv("ENDPOINT");

           // Create an ObsClient instance.
           // Use the permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use the temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               String uploadId = "upload id from initiateMultipartUpload";
               // List uploaded parts. uploadId is obtained from the initiateMultipartUpload API.
               ListPartsRequest request = new ListPartsRequest("examplebucket", "objectname");
               request.setUploadId(uploadId);
               ListPartsResult result = obsClient.listParts(request);
               for (Multipart part : result.getMultipartList()) {
                   // Part number, specified during the upload
                   System.out.println("PartNumber:" + part.getPartNumber());
                   // Part size
                   System.out.println("Size:" + part.getSize());
                   // Part ETag
                   System.out.println("Etag:" + part.getEtag());
                   // Time when the part was last uploaded
                   System.out.println("LastModified:" + part.getLastModified());
               }
               System.out.println("listParts successfully");
           } catch (ObsException e) {
               System.out.println("listParts failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code:" + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message:" + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
               e.printStackTrace();
           } catch (Exception e) {
               System.out.println("listParts failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }

Code Example: Listing All Uploaded Parts
----------------------------------------

This example lists over 1,000 parts using pagination.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.ListPartsRequest;
   import com.obs.services.model.ListPartsResult;
   import com.obs.services.model.Multipart;
   public class ListParts002 {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           String securityToken = System.getenv("SECURITY_TOKEN");
           // Enter the endpoint corresponding to the region where the bucket is to be created.
           String endPoint = "https://your-endpoint";
           // Obtain an endpoint using environment variables or import it in other ways.
           //String endPoint = System.getenv("ENDPOINT");

           // Create an ObsClient instance.
           // Use the permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use the temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               String uploadId = "upload id from initiateMultipartUpload";
               // List uploaded parts. uploadId is obtained from the initiateMultipartUpload API.
               ListPartsRequest request = new ListPartsRequest("examplebucket", "objectname");
               request.setUploadId(uploadId);
               ListPartsResult result;
               do {
                   result = obsClient.listParts(request);
                   for (Multipart part : result.getMultipartList()) {
                       // Part number, specified during the upload
                       System.out.println("PartNumber:" + part.getPartNumber());
                       // Part size
                       System.out.println("Size:" + part.getSize());
                       // Part ETag
                       System.out.println("Etag:" + part.getEtag());
                       // Time when the part was last uploaded
                       System.out.println("LastModified:" + part.getLastModified());
                   }
                   request.setPartNumberMarker(Integer.parseInt(result.getNextPartNumberMarker()));
               } while (result.isTruncated());
               System.out.println("listParts successfully");
           } catch (ObsException e) {
               System.out.println("listParts failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code:" + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message:" + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
               e.printStackTrace();
           } catch (Exception e) {
               System.out.println("listParts failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
