:original_name: obs_22_1503.html

.. _obs_22_1503:

Log Analysis
============

Log Configuration
-----------------

OBS Python SDK provides the logging function based on the Python log library. You can call **ObsClient.initLog** to enable and configure logging. Sample code is as follows:

.. code-block::

   # Import the module.
   from obs import LogConf
   from obs import ObsClient

   # Create an instance of ObsClient.
   obsClient = ObsClient(
       access_key_id=os.getenv("AccessKeyID"),
       secret_access_key=os.getenv("SecretAccessKey"),
       server='https://your-endpoint'
   )

   # Specify the path to the log configuration file and initialize logs of ObsClient.
   obsClient.initLog(LogConf('./log.conf'), 'obs_logger');

.. note::

   -  The logging function is disabled by default. You need to enable it manually.
   -  The log configuration file example (**log.conf**) is included in the OBS Python SDK development package. Modify parameters in **log.conf** as needed.

.. important::

   The log module of the OBS Python SDK is thread secure but not process secure. If ObsClient is used in multi-process scenarios, you must configure an independent log path for each instance of ObsClient to prevent conflicts when multiple processes write logs concurrently.

Log Format
----------

The SDK log format is: *Log time*\ \|\ *Process ID*\ \|\ *Thread number*\ \|\ *Log level*\ \|\ *Log content*. The following are example logs:

.. code-block::

   2017-11-06 13:46:54,936|process:6100|thread:12700|DEBUG|HTTP(s)+XML|OBS_LOGGER|__parse_xml,188|http response result:status:200,reason:OK,code:None,message:None,headers:[('id-2', 'LgOKocHfuHe0rFSUHS6LcChzcoYes0luPgqxhUfCP58xp3MZh2n4YKRPpABV8GEK'), ('connection', 'close'), ('request-id', '0001AFF8E60000015F8FDA1EA5AE04E3'), ('date', 'Mon, 06 Nov 2017 05:42:37 GMT'), ('content-type', 'application/xml')]|
   2017-11-06 13:46:54,937|process:6100|thread:12700|INFO|HTTP(s)+XML|OBS_LOGGER|doClose,349|server inform to close connection|
   2017-11-06 13:46:54,937|process:6100|thread:12700|INFO|HTTP(s)+XML|OBS_LOGGER|wrapper,59|listBuckets cost 56 ms|

Log Level
---------

When current logs cannot be used to troubleshoot system faults, you can change the log level to obtain more information. You can obtain the most information in **DEBUG** logs and the least information in **ERROR** logs.

Log level description:

-  **DEBUG**: Debugging level. If this level is set, all logs will be printed.
-  **INFO**: Information level. If this level is set, logs at the **WARNING** level and the time consumed for each HTTP/HTTPS request will be printed.
-  **WARNING**: Warning level. If this level is set, logs at the **ERROR** level and some critical events will be printed.
-  **ERROR**: Error level. If this level is set, only error information will be printed.

.. note::

   In the configuration file, **LogFileLevel** is used to specify the log level for log files, and **PrintLogLevel** is used to specify the log level for the console.
