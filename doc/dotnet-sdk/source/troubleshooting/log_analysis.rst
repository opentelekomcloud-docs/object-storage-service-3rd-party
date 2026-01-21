:original_name: obs_25_1602.html

.. _obs_25_1602:

Log Analysis
============

Log Path
--------

Log files of OBS .NET SDK are saved in the path, usually the save directory of executable files of the project, specified in configuration file **Log4Net.config**.

Log Level
---------

When current logs cannot be used to troubleshoot system faults, you can change the log level to obtain more information. You can obtain the most information in **DEBUG** logs and the least information in **ERROR** logs.

Log level description:

-  **DEBUG**: debugging level
-  **INFO**: information level
-  **WARN**: warning level
-  **ERROR**: error level

Analysis Method
---------------

To analyze and locate a problem or view the running status, you can find the related log file based on the date and view the running status or view logs in the log file for troubleshooting.

The procedure is as follows:

#. Find related logs.

   Find related API logs in the log file directory based on the time when the exception occurred and the operation. The following is an example of error logs:

   .. code-block::

      2018-05-23 21:55:02,103 [9] INFO  - ListObjectsRequest begin.
      2018-05-23 21:55:02,526 [9] INFO  - Send http request end, cost 385 ms
      2018-05-23 21:55:02,536 [9] ERROR - Rethrowing as a ObsException error in PerformRequest
      Request error, StatusCode:404, ErrorCode:NoSuchBucket, ErrorMessage:The specified bucket does not exist, RequestId:0403000001638D4819383F2D4A2B2C50, HostId:N8OMsHew7O/LMHua8qpm49geWphVJI6l2mnnzUIYwQwHAuzJw/kmV+O4iIcf0GRR
      2018-05-23 21:55:02,548 [9] ERROR - ListObjectsRequest exception code: NoSuchBucket, with message: Request error
      2018-05-23 21:55:02,553 [9] INFO  - ListObjectsRequest end, cost 449 ms

#. Analyze the cause based on the error logs.

   Assuming that the error code you obtain from the log file is **NoSuchBucket**, you can check it from the table in :ref:`OBS Server-Side Error Codes <obs_25_1601>` and know the error information is "The specified bucket does not exist."
