:original_name: obs_25_0204.html

.. _obs_25_0204:

Configuring SDK Logging
=======================

OBS .NET SDK provides the logging function, based on the Apache Log4net open library. You can add log configuration files to enable the logging function. The procedure is as follows:

#. Add a reference to **log4net.dll** in the project.
#. Copy configuration file **Log4Net.config** to **Debug** or **Release** under directory **bin** of the project, to ensure that the configuration file and the project's executable files are in the same directory.
#. Modify log levels in file **Log4Net.config** based on needs.

.. note::

   -  Without these operations, the logging function is in the disabled state and no logs will be generated.
   -  For details about SDK logs, see :ref:`Log Analysis <obs_25_1602>`.
   -  The save path of log files defaults to be that of the project's executable files and can be changed in **Log4Net.config**.
