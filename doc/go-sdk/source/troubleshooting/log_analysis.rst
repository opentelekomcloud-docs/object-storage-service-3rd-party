:original_name: obs_23_1603.html

.. _obs_23_1603:

Log Analysis
============

Log Configuration
-----------------

OBS Go SDK provides the logging function based on the **log** standard library. You can use **InitLog** to enable logging, **CloseLog** to disable logging, and synchronize log information in the cache to log files. Sample code:

.. code-block::

   // Import the dependency package.
   import (
          "obs-sdk-go/obs"
   )

   func main() {
          // Set the path for saving log files.
          var logFullPath string = "./logs/OBS-SDK.log"
          // Set the size (in bytes) for each log file.
          var maxLogSize int64 = 1024 * 1024 * 10
          // Set the number of retained log files.
          var backups int = 10
          // Set the log level.
          var level = obs.LEVEL_INFO
          // Specify whether to print logs to the console.
          var logToConsole bool = false

          // Enable logging.
          obs.InitLog(logFullPath, maxLogSize, backups, level, logToConsole)
          // Disable logging.
          obs.CloseLog()
   }

.. note::

   -  The logging function is disabled by default. You need to enable it manually.
   -  By default, logs are written to the cache (then written to log files after logs are accumulated to a certain amount). You can call **obs.CloseLog()** to forcibly synchronize the log information from the cache to log files.

Log Format
----------

The SDK log format is: Log time|file saving the printed log: row number|log level|log content The following are example logs:

.. code-block::

   2018/03/13 16:21:50 [INFO]: http.go:79|Enter method ListBuckets...
   2018/03/13 16:21:52 [INFO]: http.go:287|Do http request cost 2597 ms

Log Levels
----------

When current logs cannot be used to troubleshoot system faults, you can change the log level to obtain more information. The following table lists the enumeration constants provided by OBS Go SDK of supported log levels:

+-------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Constant    | Default Value | Description                                                                                                                                                                                                               |
+=============+===============+===========================================================================================================================================================================================================================+
| LEVEL_OFF   | 500           | Close level. If this level is set, logging will be disabled.                                                                                                                                                              |
+-------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| LEVEL_ERROR | 400           | Error level. If this level is set, only error information will be printed.                                                                                                                                                |
+-------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| LEVEL_WARN  | 300           | Warning level. If this level is set, information about logs at the error level and information about partial critical events will be printed.                                                                             |
+-------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| LEVEL_INFO  | 200           | Information level. If this level is set, information about logs of the warning level, time consumed for each HTTP/HTTPS request, and time consumed for calling the **ObsClient** API will be printed.                     |
+-------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| LEVEL_DEBUG | 100           | Debugging level. If this level is set, information about logs at the information level, HTTP/HTTPS request and response headers, and **stringToSign** information calculated by authentication algorithm will be printed. |
+-------------+---------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
