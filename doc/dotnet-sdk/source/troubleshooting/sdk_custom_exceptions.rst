:original_name: obs_25_1606.html

.. _obs_25_1606:

SDK Custom Exceptions
=====================

SDK custom exceptions (**ObsException**) are thrown by **ObsClient**. Exceptions are usually OBS server-side errors, including :ref:`OBS error codes <obs_25_1601>` and error information and aim to help users locate problems and troubleshot faults.

**ObsException** contains the following error information:

-  **ObsException.StatusCode**: HTTP status code
-  **ObsException.ErrorCode**: OBS server-side error code
-  **ObsException.ErrorMessage**: Error description returned by the OBS server
-  **ObsException.RequestId**: Request ID returned by the OBS server
-  **ObsException.HostId**: Requested server ID
