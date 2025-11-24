:original_name: obs_20_1603.html

.. _obs_20_1603:

Log Analysis
============

Log Path
--------

The OBS C SDK log path is specified by the **LogPath** field in **OBS.ini**. By default, logs are stored in the **logs** directory at the same level as the **lib** directory of the C SDK dynamic library. To locate a fault, view **eSDK-OBS-API-*-C.run.log** or **obs-sdk-c.run.log** in the **logs** directory.

**OBS.ini** must be in the same directory as **libeSDKLogAPI.so**.

Log Format
----------

The SDK log format is: Log time|log level|thread ID|log content. The following are example logs:

.. code-block::

   Run logs
   2018-05-15 22:22:54 803| INFO|[140677572568864]|request_perform start

Log Levels
----------

When current logs cannot be used to troubleshoot system faults, you can change the log level to obtain more information. You can obtain the most information in **DEBUG(0)** logs and the least information in **ERROR(3)** logs.

Log level description:

-  DEBUG(0): Debug level. If this level is set, logs at the **INFO** level and some debugging information will be printed.
-  INFO(1): Information level. If this level is set, logs at the **WARN** level, calling process and key information of OBS APIs will be printed.
-  **WARN(2)**: Warning level. If this level is set, logs at the **ERROR** level and some critical events, such as **curl_global_init** initialization fail, will be printed.
-  **ERROR(3)**: Error level. If this level is set, only error information will be printed.

Enabling System Logging
-----------------------

In the **lib** directory, modify **OBS.ini**, modify the size, number, and level of logs. (The **\*_Run** parameter is the most common configuration item.)

.. code-block::

   ;Every line must be less than 1024
   [LogConfig]
   ;Log Size: unit=KB, 10MB = 10KB * 1024 = 10240KB
   LogSize_Interface=10240
   LogSize_Operation=10240
   LogSize_Run=10240
   ;Log Num
   LogNum_Interface=10
   LogNum_Operation=10
   LogNum_Run=10
   ;Log level: debug = 0,info = 1,warn = 2,error = 3
   LogLevel_Interface=0
   LogLevel_Operation=0
   LogLevel_Run=0
   ;LogFilePermission
   LogFilePermission=0600
   [ProductConfig]
   ;Product Name
   sdkname=eSDK-OBS-API-Linux-C
   [LogPath]
   ;Log Path is relative to the path of configuration file
   LogPath=../logs

Other Configurations
--------------------

In Windows, the **LogPath** field in the **OBS.ini** can be read in type wchar_t. To do that, you need to set the encoding for the file path first. An example is given here:

**set_file_path_code(UNICODE_CODE);**//**ANSI_CODE** is used by default.

In addition, the local file path for functions listed in the table below must also be in type wchar_t (parameters are passed in type char\* and processed into type wchar_t internally).

.. table:: **Table 1**

   +------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | Related Function | Description                                                                                                                                        |
   +==================+====================================================================================================================================================+
   | download_file    | The **downLoad_file** and **check_point_file** members of the **download_file_config** parameter must be in type wchar_t. Pass them in type char*. |
   +------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | upload_file      | The **upload_file** and **check_point_file** members of the **upload_file_config** parameter must be in type wchar_t. Pass them in type char*.     |
   +------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | set_obs_log_path | The **log_path** parameter must be in type wchar_t. Pass it in type char*.                                                                         |
   +------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
