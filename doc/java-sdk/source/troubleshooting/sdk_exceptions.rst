:original_name: obs_21_2005.html

.. _obs_21_2005:

SDK Exceptions
==============

SDK custom exceptions (**ObsException**), thrown by **ObsClient**, are inherited from class **java.lang.RuntimeException**. Exceptions are usually OBS server errors, including :ref:`OBS error codes <obs_21_2002>` and error information. This facilitates users to locate problems and troubleshot faults.

**ObsException** contains the following error information:

-  **ObsException.getResponseCode()**: HTTP status code
-  **ObsException.getErrorCode()**: Error code returned by the OBS server
-  **ObsException.getErrorMessage()**: Error description returned by the OBS server
-  **ObsException.getErrorRequestId()**: Request ID returned by the OBS server
-  **ObsException.getErrorHostId()**: Requested server ID
-  **ObsException.getResponseHeaders()**: HTTP response headers
-  **ObsException.printStackTrace()**: Prints the detailed stack trace of an exception.
