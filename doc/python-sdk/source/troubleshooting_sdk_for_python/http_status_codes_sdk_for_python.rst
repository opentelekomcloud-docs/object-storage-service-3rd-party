:original_name: obs_22_1501.html

.. _obs_22_1501:

HTTP Status Codes (SDK for Python)
==================================

The OBS server complies with the HTTP standard. After an API is called, the OBS server returns a standard HTTP status code. The following tables list the categories of HTTP status codes and the common HTTP status codes in OBS.

-  Categories of HTTP status codes

   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Category | Description                                                                                                                                                                    |
   +==========+================================================================================================================================================================================+
   | 1XX      | Informational response. A request is received by the server and the server requires the requester to continue the operation. This category is usually invisible to the client. |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 2XX      | Success. The operation is received and processed successfully.                                                                                                                 |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 3XX      | Redirection. Further operations to complete the request are required.                                                                                                          |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 4XX      | Client errors. The request contains a syntax error, or the request cannot be implemented.                                                                                      |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 5XX      | Server errors. An error occurs when the server is processing the request.                                                                                                      |
   +----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Common HTTP status codes in OBS and their meanings

   +---------------------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | HTTP Status Code          | Description                            | Possible Cause                                                                                                                                                                           |
   +===========================+========================================+==========================================================================================================================================================================================+
   | 400 Bad Request           | Incorrect request parameter.           | -  Invalid request parameter.                                                                                                                                                            |
   |                           |                                        | -  The consistency check fails after the client request carries MD5.                                                                                                                     |
   |                           |                                        | -  An invalid parameter is transferred when the SDK is used.                                                                                                                             |
   |                           |                                        | -  An invalid bucket name is used.                                                                                                                                                       |
   +---------------------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 403 Forbidden             | Access denied.                         | -  The signature of the request does not match. Generally, the error is caused by incorrect AK/SK.                                                                                       |
   |                           |                                        | -  The account does not have the permission to access the requested resource.                                                                                                            |
   |                           |                                        | -  The account is in arrears.                                                                                                                                                            |
   |                           |                                        | -  The bucket space is insufficient when a quota is set for the bucket.                                                                                                                  |
   |                           |                                        | -  Invalid AK                                                                                                                                                                            |
   |                           |                                        | -  The time difference between the client and the server is too large. That is, the time of the server where the client is located is not synchronized with the time of the NTP service. |
   +---------------------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 404 Not Found             | The requested resource does not exist. | -  The bucket does not exist.                                                                                                                                                            |
   |                           |                                        | -  The object does not exist.                                                                                                                                                            |
   |                           |                                        | -  The bucket policy configuration does not exist. For example, the bucket CORS configuration or bucket policy configuration does not exist.                                             |
   |                           |                                        | -  The multipart upload does not exist.                                                                                                                                                  |
   +---------------------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 405 Method Not Allowed    | The request method is not supported.   | The requested method or feature is not supported in the region where the bucket resides.                                                                                                 |
   +---------------------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 408 Request Timeout       | Request timed out.                     | The socket connection between the server and client timed out.                                                                                                                           |
   +---------------------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 409 Conflict              | Request conflicts occur.               | -  Buckets of the same name are created in different regions.                                                                                                                            |
   |                           |                                        | -  Deletion of a non-empty bucket is attempted.                                                                                                                                          |
   +---------------------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 500 Internal Server Error | Internal server error.                 | Internal server error.                                                                                                                                                                   |
   +---------------------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 503 Service Unavailable   | Service unavailable.                   | The server cannot be accessed temporarily.                                                                                                                                               |
   +---------------------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
