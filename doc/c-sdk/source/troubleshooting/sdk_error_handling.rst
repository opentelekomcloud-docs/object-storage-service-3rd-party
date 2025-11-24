:original_name: obs_20_1602.html

.. _obs_20_1602:

SDK Error Handling
==================

SDK errors include the errors returned during the check of function parameters and those returned by the OBS server.

SDK error handling information:

-  obs_status: Error code
-  obs_get_status_name(): Obtaining the error description
-  obs_status_is_retryable(): Checking whether the error code requires service retry
