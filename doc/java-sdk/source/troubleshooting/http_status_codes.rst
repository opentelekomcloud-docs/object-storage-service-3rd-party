:original_name: obs_21_2001.html

.. _obs_21_2001:

HTTP Status Codes
=================

The OBS server complies with the HTTP standard. After an API is called, the OBS server returns a standard HTTP status code. The following tables list the categories of HTTP status codes and the common HTTP status codes in OBS.

-  Categories of HTTP status codes

   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Category | Description                                                                                                                                                                    |
   +==========+================================================================================================================================================================================+
   | 1XX      | Informational response. A request is received by the server and the server requires the requester to continue the operation. This category is usually invisible to the client. |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 2XX      | Success. The operation is received and processed successfully.                                                                                                                 |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 3XX      | Redirection. Further operations to complete the request are required. This category is usually invisible to the client.                                                        |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 4XX      | Client errors. The request contains a syntax error, or the request cannot be implemented.                                                                                      |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 5XX      | Server errors. There is an error when the server is processing a request.                                                                                                      |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Common HTTP status codes in OBS and their meanings

   +---------------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HTTP Status Code          | Description                                  | Possible Cause                                                                                                                                                              |
   +===========================+==============================================+=============================================================================================================================================================================+
   | 400 Bad Request           | The request parameter is incorrect.          | -  Invalid request parameter.                                                                                                                                               |
   |                           |                                              | -  The consistency check fails after the client request carries MD5.                                                                                                        |
   |                           |                                              | -  An invalid parameter is transferred when the SDK is used.                                                                                                                |
   |                           |                                              | -  An invalid bucket name is used.                                                                                                                                          |
   +---------------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 403 Forbidden             | The access is denied.                        | -  The signature carried in the request header does not match with the signature calculated by the OBS server. Generally, the error is caused by incorrect AK/SK.           |
   |                           |                                              | -  The account does not have the permission to access the requested resource.                                                                                               |
   |                           |                                              | -  The account is in arrears.                                                                                                                                               |
   |                           |                                              | -  The bucket space is insufficient when a quota is set for the bucket.                                                                                                     |
   |                           |                                              | -  Invalid AK                                                                                                                                                               |
   |                           |                                              | -  The time difference between the client and the server is too large (the time on the machine where the client is located is not in sync with the time on the NTP server). |
   +---------------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 404 Not Found             | The requested resource does not exist.       | -  The bucket does not exist.                                                                                                                                               |
   |                           |                                              | -  The object does not exist.                                                                                                                                               |
   |                           |                                              | -  The bucket policy configuration does not exist. For example, the bucket CORS configuration or bucket policy configuration does not exist.                                |
   |                           |                                              | -  The multipart upload does not exist.                                                                                                                                     |
   +---------------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 405 Method Not Allowed    | The request method is not supported.         | The request method or feature is not supported in the region where the bucket is located.                                                                                   |
   +---------------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 408 Request Timeout       | Request timed out.                           | The Socket connection between the server and client times out.                                                                                                              |
   +---------------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 409 Conflict              | Request conflicts occur.                     | -  Buckets of the same name are created in different regions.                                                                                                               |
   |                           |                                              | -  The bucket to delete is not empty.                                                                                                                                       |
   +---------------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 500 Internal Server Error | An internal error occurs on the server side. | An internal error occurs on the server side.                                                                                                                                |
   +---------------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 503 Service Unavailable   | The service is unavailable.                  | The server is inaccessible temporarily.                                                                                                                                     |
   +---------------------------+----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
