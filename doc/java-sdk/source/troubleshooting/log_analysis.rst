:original_name: obs_21_2004.html

.. _obs_21_2004:

Log Analysis
============

How To Enable Logging
---------------------

#. Save the **log4j2.xml** file obtained from the OBS Java SDK package to the **classpath** root directory.
#. Call **Log4j2Configurator.setLogConfig** to specify the save path of **log4j2.xml** directly.

.. note::

   You can obtain the default log configuration file **log4j2.xml** from the OBS Java SDK package, and then modify to customize the file.

Log Path
--------

The log path of OBS Java SDK is specified in **log4j2.xml**. Logs are saved in the path represented by system variable **user.dir** of JDK by default. In general, there are three logs files as follows:

+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| File Name                   | Description                                                                                                                   |
+=============================+===============================================================================================================================+
| OBS-SDK.interface_north.log | Northbound log file, which saves the logs about the communication between OBS Java SDK and third-party applications of users. |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| OBS-SDK.interface_south.log | Southbound log file, which saves the logs about the communication between OBS Java SDK and the OBS server.                    |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------+
| OBS-SDK.access.log          | Run log file of the OBS server.                                                                                               |
+-----------------------------+-------------------------------------------------------------------------------------------------------------------------------+

Log Format
----------

The SDK log format is: *Log time*\ \|\ *Thread number*\ \|\ *Log level*\ \|\ *Log content*. The following are example logs:

.. code-block::

   #Southbound logs
   2017-08-21 17:40:07 133|main|INFO |HttpClient cost 157 ms to apply http request
   2017-08-21 17:40:07 133|main|INFO |Received expected response code: true
   2017-08-21 17:40:07 133|main|INFO |expected code(s): [200, 204].

   #Northbound logs
   2017-08-21 17:40:06 820|main|INFO |Storage|1|HTTP+XML|ObsClient||||2017-08-21 17:40:05|2017-08-21 17:40:06|||0|
   2017-08-21 17:40:07 136|main|INFO |Storage|1|HTTP+XML|setObjectAcl||||2017-08-21 17:40:06|2017-08-21 17:40:07|||0|
   2017-08-21 17:40:07 137|main|INFO |ObsClient [setObjectAcl] cost 312 ms

Log Level
---------

When current logs cannot be used to troubleshoot system faults, you can change the log level to obtain more information. You can obtain the most information in **TRACE** logs and the least information in **ERROR** logs.

Log level description:

-  **OFF**: Close level. If this level is set, logging will be disabled.
-  **TRACE**: Trace level. If this level is set, all log information will be printed. This level is not recommended.
-  **DEBUG**: Debugging level. If this level is set, information about logs of the **INFO** level and above, HTTP/HTTPS request and response headers, and **StringToSign** information calculated by authentication algorithm will be printed.
-  **INFO**: Information level. If this level is set, information about logs of the **WARN** level and above, time consumed for each HTTP/HTTPS request, and time consumed for calling the ObsClient API will be printed.
-  **WARN**: Warning level. If this level is set, information about logs of the **ERROR** level and above, as well as information about some critical events (for example, the number of retry attempts exceeds the upper limit) will be printed.
-  **ERROR**: Error level. If this level is set, only error information will be printed.

How to Set
----------

The following sample code shows how to set different levels for the southbound logs, northbound logs, and OBS server run logs. (For details about log configuration, see configuration file **log4j2.xml**.)

::

   <!-- north log -->
   <Logger name="com.obs.services.AbstractClient" level="INFO" additivity="false">
         <AppenderRef ref="NorthInterfaceLogAppender" />
   </Logger>

   <!-- south log -->
   <Logger name="com.obs.services.internal.RestStorageService" level="WARN" additivity="false">
          <AppenderRef ref="SouthInterfaceLogAppender" />
   </Logger>

   <!-- access log -->
   <Logger name="com.obs.log.AccessLogger" level="ERROR" additivity="false">
           <AppenderRef ref="AccessLogAppender" />
   </Logger>
