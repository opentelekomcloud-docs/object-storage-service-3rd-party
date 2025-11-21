:original_name: obs_29_1905.html

.. _obs_29_1905:

Listing Uploaded Parts
======================

Function
--------

This API lists the uploaded parts in a specified bucket. This request must contain the multipart upload ID.

You can list the uploaded parts of a specified multipart upload or of all ongoing multipart uploads. For each listing request, OBS can list a maximum of 1,000 uploaded parts. If more than 1,000 parts were uploaded for a multipart upload, you need to send more than one request to list all uploaded parts. Assembled parts will not be listed.

Restrictions
------------

-  To list uploaded parts, you must be the bucket owner or have the required permission (**obs:object:ListMultipartUploadParts** in IAM or **ListMultipartUploadParts** in a bucket policy).
-  A maximum of 1,000 parts can be listed each time. If the upload of a specified ID contains more than 1,000 parts, **InterfaceResult.IsTruncated** in the response is **true**, indicating not all parts were listed. In such case, you can use **InterfaceResult.NextPartNumberMarker** to obtain the start position for the next listing.

Method
------

.. code-block::

   ObsClient.listParts(params)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Type            | Mandatory (Yes/No) | Description                                                                                                                                                                          |
   +==================+=================+====================+======================================================================================================================================================================================+
   | Bucket           | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | Bucket name                                                                                                                                                                          |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                     |
   |                  |                 |                    | -  A bucket name:                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                         |
   |                  |                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                          |
   |                  |                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                           |
   |                  |                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                      |
   |                  |                 |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                            |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | -  If you repeatedly create buckets with the same name in the same region, no error will be reported, and the bucket attributes comply with those set in the first creation request. |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Value range**:                                                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | The value can contain 3 to 63 characters.                                                                                                                                            |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Default value**:                                                                                                                                                                   |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | None                                                                                                                                                                                 |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key              | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name.                  |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | None                                                                                                                                                                                 |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Value range**:                                                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | The value can contain 1 to 1,024 characters.                                                                                                                                         |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Default value**:                                                                                                                                                                   |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | None                                                                                                                                                                                 |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | UploadId         | string          | Yes                | **Explanation:**                                                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | Multipart upload ID, which is generated by :ref:`initiating a multipart upload <obs_29_1902>`.                                                                                       |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | None                                                                                                                                                                                 |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Value range**:                                                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | The value must contain 32 characters, for example, **000001648453845DBB78F2340DD460D8**.                                                                                             |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Default value**:                                                                                                                                                                   |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | None                                                                                                                                                                                 |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PartNumberMarker | number          | No                 | **Explanation:**                                                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | Part number the listing starts from.                                                                                                                                                 |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | None                                                                                                                                                                                 |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | OBS only lists parts with greater numbers than that specified by this parameter.                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Default value**:                                                                                                                                                                   |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | None                                                                                                                                                                                 |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MaxParts         | number          | No                 | **Explanation:**                                                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | Maximum number of parts that can be listed per page.                                                                                                                                 |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Restrictions**:                                                                                                                                                                    |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | If the specified value is greater than **1000**, only 1,000 parts are returned.                                                                                                      |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Value range**:                                                                                                                                                                     |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | The value ranges from **1** to **1000**.                                                                                                                                             |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | **Default value**:                                                                                                                                                                   |
   |                  |                 |                    |                                                                                                                                                                                      |
   |                  |                 |                    | 1000                                                                                                                                                                                 |
   +------------------+-----------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 2** Responses

   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Type                                                                                      | Description                                                                          |
   +===========================================================================================+======================================================================================+
   | :ref:`Table 3 <obs_29_1905__table1722625714202>`                                          | **Explanation:**                                                                     |
   |                                                                                           |                                                                                      |
   | .. note::                                                                                 | Returned results. For details, see :ref:`Table 3 <obs_29_1905__table1722625714202>`. |
   |                                                                                           |                                                                                      |
   |    This API returns a Promise response, which requires the Promise or async/await syntax. |                                                                                      |
   +-------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_29_1905__table1722625714202:

.. table:: **Table 3** Response

   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                   |
   +=======================+=====================================================+===============================================================================================================================================================================+
   | CommonMsg             | :ref:`ICommonMsg <obs_29_1905__table6176201212273>` | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Common information generated after an API call is complete, including the HTTP status code and error code. For details, see :ref:`Table 4 <obs_29_1905__table6176201212273>`. |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | InterfaceResult       | :ref:`Table 5 <obs_29_1905__table33959011>`         | **Explanation:**                                                                                                                                                              |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | Results outputted for a successful call. For details, see :ref:`Table 5 <obs_29_1905__table33959011>`.                                                                        |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | **Restrictions:**                                                                                                                                                             |
   |                       |                                                     |                                                                                                                                                                               |
   |                       |                                                     | This parameter is not included if the value of **Status** is greater than 300.                                                                                                |
   +-----------------------+-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1905__table6176201212273:

.. table:: **Table 4** ICommonMsg

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Parameter**         | **Type**              | **Description**                                                                                                                                                  |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                | number                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | HTTP status code returned by the OBS server.                                                                                                                     |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | **Value range**:                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | A status code is a group of digits indicating the status of a response. It ranges from 2\ *xx* (indicating successes) to 4\ *xx* or 5\ *xx* (indicating errors). |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Code                  | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Error code returned by the OBS server.                                                                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Message               | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Error description returned by the OBS server.                                                                                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HostId                | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Request server ID returned by the OBS server.                                                                                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Request ID returned by the OBS server.                                                                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Id2                   | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Request ID2 returned by the OBS server.                                                                                                                          |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Indicator             | string                | **Explanation:**                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                  |
   |                       |                       | Error code details returned by the OBS server.                                                                                                                   |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1905__table33959011:

.. table:: **Table 5** ListMultipartUploadsOutput

   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                        | Description                                                                                                                                                                                                            |
   +=======================+=============================================================+========================================================================================================================================================================================================================+
   | RequestId             | string                                                      | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Request ID returned by the OBS server                                                                                                                                                                                  |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Bucket                | string                                                      | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Bucket name                                                                                                                                                                                                            |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key                   | string                                                      | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path of the object that does not contain the bucket name.                                                    |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | UploadId              | string                                                      | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Multipart upload ID, for example, **000001648453845DBB78F2340DD460D8**.                                                                                                                                                |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Initiator             | :ref:`Initiator <obs_29_1905__table1789825565819>`          | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Initiator of the multipart upload. For details, see :ref:`Table 6 <obs_29_1905__table1789825565819>`.                                                                                                                  |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner                 | :ref:`Owner <obs_29_1905__table14427161515578>`             | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Owner of the multipart upload, which is consistent with an initiator. For details, see :ref:`Table 7 <obs_29_1905__table14427161515578>`.                                                                              |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | StorageClass          | :ref:`StorageClassType <obs_29_1905__table127731936165615>` | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Storage class of the object obtained from assembling parts. For details about storage classes, see :ref:`Table 8 <obs_29_1905__table127731936165615>`.                                                                 |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PartNumberMarker      | number                                                      | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Part number the listing begins from, which is consistent with that specified in the request.                                                                                                                           |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | NextPartNumberMarker  | number                                                      | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Part number to start with for the next part listing request. This parameter is returned if some parts were not listed. You can set **PartNumberMarker** to this value in the next request to list the remaining parts. |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MaxParts              | number                                                      | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Maximum number of parts that can be listed per page, which is consistent with that specified in the request.                                                                                                           |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | IsTruncated           | boolean                                                     | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | Whether all results are returned in the response.                                                                                                                                                                      |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | **Value range**:                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | -  **true**: Not all results are returned.                                                                                                                                                                             |
   |                       |                                                             | -  **false**: All results are returned.                                                                                                                                                                                |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parts                 | :ref:`Part <obs_29_1905__table10704184772010>`\ []          | **Explanation:**                                                                                                                                                                                                       |
   |                       |                                                             |                                                                                                                                                                                                                        |
   |                       |                                                             | List of uploaded parts. For details, see :ref:`Table 9 <obs_29_1905__table10704184772010>`.                                                                                                                            |
   +-----------------------+-------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1905__table1789825565819:

.. table:: **Table 6** Initiator

   +-----------------+-----------------+------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                 | Description                                                                                                                                       |
   +=================+=================+====================================+===================================================================================================================================================+
   | ID              | string          | Yes if used as a request parameter | **Explanation:**                                                                                                                                  |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | Account (domain) ID of the initiator                                                                                                              |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | **Value range**:                                                                                                                                  |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_29_1715>`.                                                       |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | **Default value**:                                                                                                                                |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | None                                                                                                                                              |
   +-----------------+-----------------+------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | DisplayName     | string          | No                                 | **Explanation:**                                                                                                                                  |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | Account name of the initiator                                                                                                                     |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | **Restrictions**:                                                                                                                                 |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | The account name can contain 6 to 32 characters and must start with a letter. Only letters, digits, hyphens (-), and underscores (_) are allowed. |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | **Default value**:                                                                                                                                |
   |                 |                 |                                    |                                                                                                                                                   |
   |                 |                 |                                    | None                                                                                                                                              |
   +-----------------+-----------------+------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1905__table14427161515578:

.. table:: **Table 7** Owner

   +-----------------+-----------------+------------------------------------+---------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                 | Description                                                                                 |
   +=================+=================+====================================+=============================================================================================+
   | ID              | string          | Yes if used as a request parameter | **Explanation:**                                                                            |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | Account (domain) ID of the owner                                                            |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | **Value range**:                                                                            |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_29_1715>`. |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | **Default value**:                                                                          |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | None                                                                                        |
   +-----------------+-----------------+------------------------------------+---------------------------------------------------------------------------------------------+
   | DisplayName     | string          | No                                 | **Explanation:**                                                                            |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | Account name of the owner                                                                   |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | **Default value**:                                                                          |
   |                 |                 |                                    |                                                                                             |
   |                 |                 |                                    | None                                                                                        |
   +-----------------+-----------------+------------------------------------+---------------------------------------------------------------------------------------------+

.. _obs_29_1905__table127731936165615:

.. table:: **Table 8** StorageClassType

   +--------------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Constant                             | Default Value         | Description                                                                                                                                                                       |
   +======================================+=======================+===================================================================================================================================================================================+
   | ObsClient.enums.StorageClassStandard | STANDARD              | Standard storage class.                                                                                                                                                           |
   |                                      |                       |                                                                                                                                                                                   |
   |                                      |                       | Features low access latency and high throughput and is used for storing massive, frequently accessed (multiple times a month) or small objects (< 1 MB) requiring quick response. |
   +--------------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.StorageClassWarm     | WARM                  | Warm storage class.                                                                                                                                                               |
   |                                      |                       |                                                                                                                                                                                   |
   |                                      |                       | Used for storing data that is semi-frequently accessed (fewer than 12 times a year) but becomes instantly available when needed.                                                  |
   +--------------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.enums.StorageClassCold     | COLD                  | Cold storage class.                                                                                                                                                               |
   |                                      |                       |                                                                                                                                                                                   |
   |                                      |                       | Used for storing rarely accessed (once a year) data.                                                                                                                              |
   +--------------------------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_29_1905__table10704184772010:

.. table:: **Table 9** Part

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                  |
   +=======================+=======================+==============================================================================================+
   | PartNumber            | number                | **Explanation:**                                                                             |
   |                       |                       |                                                                                              |
   |                       |                       | Part number                                                                                  |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------+
   | LastModified          | string                | **Explanation:**                                                                             |
   |                       |                       |                                                                                              |
   |                       |                       | Time when a part was last modified, in UTC                                                   |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------+
   | ETag                  | string                | **Explanation:**                                                                             |
   |                       |                       |                                                                                              |
   |                       |                       | ETag of a part. It is calculated by encoding the 128-bit MD5 value of the part using Base64. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------+
   | Size                  | number                | **Explanation:**                                                                             |
   |                       |                       |                                                                                              |
   |                       |                       | Size of the space occupied by a part                                                         |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------+

Code Examples
-------------

This example lists the parts that have been uploaded for a multipart upload.

::

   // Import the OBS library.
   // Use npm to install the client.
   const ObsClient = require("esdk-obs-nodejs");
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');
   // Create an instance of ObsClient.
   const obsClient = new ObsClient({
     // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
     // Obtain an AK/SK pair on the management console.
     access_key_id: process.env.ACCESS_KEY_ID,
     secret_access_key: process.env.SECRET_ACCESS_KEY,
     // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
     // security_token: process.env.SECURITY_TOKEN,
     // Enter the endpoint of the region where the bucket is located.
     server: "https://your-endpoint"
   });

   async function listParts() {
       try {
           const params = {
               // Specify the bucket name.
               Bucket: "examplebucket",
               // Specify an object. example/objectname is used in this example.
               Key: "example/objectname",
               // Specify the multipart upload ID (00000188677110424014075CC4A77xxx in this example).
               UploadId: "00000188677110424014075CC4A77xxx",
               // Specify the maximum number of objects to be returned in alphabetic order. The default value is 1000. 100 is used in this example.
               MaxKeys: 100,
           };
           // List uploaded parts.
           const result = await obsClient.listParts(params);
           if (result.CommonMsg.Status <= 300) {
               console.log("List part successful with bucket(%s) and object(%s)!", params.Bucket, params.Key);
               console.log('RequestId: %s', result.CommonMsg.RequestId);
               console.log('Bucket: %s', result.InterfaceResult.Bucket);
               console.log('Key: %s', result.InterfaceResult.Key);
               console.log('UploadId: %s', result.InterfaceResult.UploadId);
               console.log('PartNumberMarker: %s', result.InterfaceResult.PartNumberMarker);
               console.log('NextPartNumberMarker: %s', result.InterfaceResult.NextPartNumberMarker);
               console.log('MaxParts: %s', result.InterfaceResult.MaxParts);
               console.log('IsTruncated: %s', result.InterfaceResult.IsTruncated);
               console.log('StorageClass: %s', result.InterfaceResult.StorageClass);
               console.log('Initiator[ID]: %s', result.InterfaceResult.Initiator['ID']);
               console.log('Owner[ID]: %s', result.InterfaceResult.Owner['ID']);
               for (let i = 0; i < result.InterfaceResult.Parts.length; i++) {
                   const part = result.InterfaceResult.Parts[i];
                   console.log("Part[%d]-ETag:%s, PartNumber:%d, LastModified:%s, Size:%d",
                       i, part.PartNumber, part.LastModified, part.ETag, part.Size);
               };
               return;
           };
           console.log("An ObsError was found, which means your request sent to OBS was rejected with an error response.");
           console.log("Status: %d", result.CommonMsg.Status);
           console.log("Code: %s", result.CommonMsg.Code);
           console.log("Message: %s", result.CommonMsg.Message);
           console.log("RequestId: %s", result.CommonMsg.RequestId);
       } catch (error) {
           console.log("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.");
           console.log(error);
       };
   };

   listParts();
