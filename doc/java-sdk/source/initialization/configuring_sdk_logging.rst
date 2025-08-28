:original_name: obs_21_0204.html

.. _obs_21_0204:

Configuring SDK Logging
=======================

OBS SDK for Java offers logging based on the open-source Apache Log4j 2 library. By default, the SDK stores WARN log files to the directory specified by the JDK system variable **user.dir**. You can modify the log configuration file based on your needs.

Procedure
---------

#. Obtain the file **log4j2.xml** from the OBS SDK for Java package.
#. Modify the log level and storage path in the file as required.
#. Save the file to the **classpath** root directory, or call **Log4j2Configurator.setLogConfig** to specify the storage path of the file.

.. note::

   -  For details about SDK logging, see :ref:`Log Analysis <obs_21_2004>`.
   -  You can modify the **log4j2.xml** file to configure access permissions for log files.
