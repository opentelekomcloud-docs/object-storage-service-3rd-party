:original_name: obs_29_1603.html

.. _obs_29_1603:

Log Analysis
============

Log Configuration
-----------------

OBS Node.js SDK provides the logging function based on Log4js. You can call **ObsClient.initLog** to enable and configure logging. The sample code is as follows:

.. code-block::

   obsClient.initLog({
          name: 'test', // Log name
   file_full_path:'./logs/OBS-SDK.log', //Set the path to the log file.
   max_log_size:20480, //Set the size of the log file, in bytes.
   backups:10, //Set the maximum number of log files that can be stored.
   level:'warn', //Set the log level.
   log_to_console:true //Set whether to print the log to Console.
   });

.. note::

   -  The logging function is disabled by default. You need to enable it if needed.
   -  Use the **file_full_path** parameter to specify the path to the log file. The path can be set to an absolute path or a relative path.

Log Format
----------

The SDK log format is: Log time|log level|invoked interface|log content. The following are examples:

.. code-block::

   2017/10/12 10:21:05 666|INFO |ListBuckets|enter ListBuckets...
   2017/10/12 10:21:05 672|INFO |ListBuckets|prepare request parameters ok,then Send request to service start
   2017/10/12 10:21:05 715|INFO |ListBuckets|2017-10-12 10:21:05|http cost 34 ms|0|
   2017/10/12 10:21:05 716|INFO |ListBuckets|get response start, statusCode:200

Log Level
---------

When current logs cannot be used to troubleshoot system faults, you can change the log level to obtain more information. You can obtain the most information in **debug** logs and the least information in **error** logs.

The following describes each log level in detail.

-  **debug**: Debugging level. If this level is set, all log information will be printed.
-  **info**: Information level. If this level is set, information about logs of the **warn** level and time consumed for each HTTP/HTTPS request will be printed.
-  **warn**: Warning level. If this level is set, information about logs of the error level and information about partial critical events will be printed.
-  **error**: Error level. If this level is set, only error information will be printed.
