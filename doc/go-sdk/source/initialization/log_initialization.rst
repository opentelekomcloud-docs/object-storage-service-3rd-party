:original_name: obs_33_0103.html

.. _obs_33_0103:

Log Initialization
==================

Function
--------

You can enable the SDK log function to record log information generated during API calling into log files for subsequent data analysis or fault location. You can use **InitLog** to enable logging, **CloseLog** to disable logging, and **SyncLog** to synchronize log information from the cache to log files.

Initialization Method
---------------------

::

   func InitLog(logFullPath string, maxLogSize int64, backups int, level Level, logToConsole bool) error

Parameters
----------

+-----------------+------------------------------------------------+--------------------+--------------------------------------------------+
| Parameter       | Type                                           | Mandatory (Yes/No) | Description                                      |
+=================+================================================+====================+==================================================+
| logFullPath     | string                                         | Yes                | Full path to the log file                        |
+-----------------+------------------------------------------------+--------------------+--------------------------------------------------+
| maxLogSize      | int64                                          | Yes                | Log file size in bytes                           |
+-----------------+------------------------------------------------+--------------------+--------------------------------------------------+
| backups         | int                                            | Yes                | Maximum number of log files that can be retained |
+-----------------+------------------------------------------------+--------------------+--------------------------------------------------+
| level           | :ref:`Level <obs_33_0103__table1475162813438>` | Yes                | Log level                                        |
+-----------------+------------------------------------------------+--------------------+--------------------------------------------------+
| logToConsole    | bool                                           | Yes                | Whether to print logs to the console             |
|                 |                                                |                    |                                                  |
|                 |                                                |                    | Value options: **true** or **false**             |
|                 |                                                |                    |                                                  |
|                 |                                                |                    | **true**: Logs are printed to the console.       |
|                 |                                                |                    |                                                  |
|                 |                                                |                    | **false**: Logs are not printed to the console.  |
|                 |                                                |                    |                                                  |
|                 |                                                |                    | Default value: **false**                         |
+-----------------+------------------------------------------------+--------------------+--------------------------------------------------+

.. _obs_33_0103__table1475162813438:

.. table:: **Table 1** Level

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

Code Examples
-------------

::

   // Import the dependency package.
   import (
       "obs-sdk-go/obs"
   )

   func main() {
          // Set a path for saving log files.
          var logFullPath string = "./logs/OBS-SDK.log"
          // Set a size (in bytes) for each log file.
          var maxLogSize int64 = 1024 * 1024 * 10
          // Set the number of retained log files.
          var backups int = 10
          // Set a log level.
          var level = obs.LEVEL_INFO
          // Specify whether to print logs to OBS Console.
          var logToConsole bool = false
          // Enable logging.
          obs.InitLog(logFullPath, maxLogSize, backups, level, logToConsole)
          // Disable logging and synchronize cached data to log files.
          obs.CloseLog()

   }

.. note::

   -  The logging function is disabled by default. You need to enable it manually.
   -  For details about SDK logs, see :ref:`Log Analysis <obs_23_1603>`.
   -  By default, logs are written to the cache (then written to log files after logs are accumulated to a certain amount). You can call **obs.CloseLog()** to forcibly synchronize the log information from the cache to log files.
