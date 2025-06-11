:original_name: obs_22_0603.html

.. _obs_22_0603:

Log Initialization
==================

Function
--------

You can enable the SDK log function to record log information generated during API calling into log files for subsequent data analysis or fault location. The procedure is as follows:

#. Find file **log.conf** in the OBS Python SDK. The content format is as follows:

   .. code-block::

      [LOGCONF]

      #Configure log file dir
      LogFileDir          = ./logs

      #Configure log file name
      LogFileName         = eSDK-OBS-PYTHON.log

      #Configure log file size, unit:MB
      LogFileSize         = 30

      #Configure max log file numbers
      LogFileNumber       = 5

      #Configure log level for log file (DEBUG | INFO | WARNING | ERROR)
      LogFileLevel        = INFO

      #Configure whether to print log to console (Yes:1 No:0)
      PrintLogToConsole   = 0

      #Configure log level for console (DEBUG | INFO | WARNING | ERROR)
      PrintLogLevel       = WARNING

#. Modify parameters in the **log.conf** file as needed.

#. Call **ObsClient.initLog** to enable the logging function.

.. note::

   -  The logging function is disabled by default. You need to enable it manually.
   -  For details about SDK logs, see :ref:`Log Analysis <obs_22_1503>`.
   -  You can change the log file permissions in the system based on your actual needs.

.. important::

   The log module of the OBS Python SDK is thread secure but not process secure. If ObsClient is used in multi-process scenarios, you must configure an independent log path for each instance of ObsClient to prevent conflicts when multiple processes write logs concurrently.

Method
------

.. code-block::

   obsClient.initLog(
       log_config='*** Your Log Configuration Parameters ***',
       log_name='*** Your Log Name ***'
   )

Constructor Parameter Description
---------------------------------

+------------+--------------------------------------------------+--------------------+-----------------------------+
| Parameter  | Type                                             | Mandatory (Yes/No) | Description                 |
+============+==================================================+====================+=============================+
| log_config | :ref:`LogConf <obs_22_0603__table1318119339147>` | Yes                | Log configuration parameter |
+------------+--------------------------------------------------+--------------------+-----------------------------+
| log_name   | str                                              | No                 | Log name                    |
+------------+--------------------------------------------------+--------------------+-----------------------------+

.. _obs_22_0603__table1318119339147:

.. table:: **Table 1** LogConf

   +-------------+------+--------------------+-------------------------------------------------------------------------------+
   | Parameter   | Type | Mandatory (Yes/No) | Description                                                                   |
   +=============+======+====================+===============================================================================+
   | config_file | str  | Yes                | Path to the log configuration file                                            |
   +-------------+------+--------------------+-------------------------------------------------------------------------------+
   | sec         | str  | No                 | Section name in the log configuration file. The default value is **LOGCONF**. |
   +-------------+------+--------------------+-------------------------------------------------------------------------------+

Code Examples
-------------

.. code-block::

   # Import the module.
   from obs import ObsClient

   # Obtain an AK and SK pair using environment variables or import the AK and SK pair in other ways. Using hard coding may result in leakage.
   # Obtain an AK and SK pair on the management console.
   ak = os.getenv("AccessKeyID")
   sk = os.getenv("SecretAccessKey")
   # (Optional) If you use a temporary AK and SK pair and a security token to access OBS, obtain them from environment variables.
   security_token = os.getenv("SecurityToken")
   # Set server to the endpoint of the region where the bucket is located.
   server = "https://your-endpoint"

   # Create an obsClient instance.
   # If you use a temporary AK and SK pair and a security token to access OBS, you must specify security_token when creating an instance.
   obsClient = ObsClient(access_key_id=ak, secret_access_key=sk, server=server)

   # Import the log module.
   from obs import LogConf

   # Specify the path to the log configuration file and initialize logs of ObsClient.
   obsClient.initLog(LogConf('./log.conf'), '*** Your Log Name ***')

   # Use ObsClient to access OBS.

   # Disable ObsClient logging.
   obsClient.close()
