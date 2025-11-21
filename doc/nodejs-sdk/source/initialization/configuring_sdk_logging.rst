:original_name: obs_29_0204.html

.. _obs_29_0204:

Configuring SDK Logging
=======================

OBS Node.js SDK provides the logging function based on Log4js. You can call **ObsClient.initLog** to enable and configure logging. The following is a code sample:

.. code-block::

   obsClient.initLog({
   file_full_path:'./logs/OBS-SDK.log', //Set the path to the log file.
          max_log_size:20480, //Set the size of the log file, in bytes.
          backups:10, //Set the maximum number of log files that can be stored.
          level:'warn', //Set the log level.
          log_to_console:true //Set whether to print the log to console.
   });

.. note::

   -  The logging function is disabled by default. You need to enable it manually.
   -  For details about SDK logs, see :ref:`Log Analysis <obs_29_1603>`.
