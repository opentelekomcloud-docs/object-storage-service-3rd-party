:original_name: obs_20_0204.html

.. _obs_20_0204:

Configuring SDK Logging
=======================

The OBS C SDK log path is specified by the **LogPath** field in **OBS.ini**. By default, logs are stored in the **logs** directory at the same level as the **lib** directory of the C SDK dynamic library. **OBS.ini** must be in the same directory as **libeSDKLogAPI.so**.

The OBS C SDK allows you to use **set_obs_log_path** to specify a log path. This method has two parameters. The first parameter specifies a path and the second determines what to do under the path. If the second parameter is set to **True**, the SDK searches for **OBS.ini** in the path specified by the first parameter for log configuration. If the second parameter is set to **False**, the SDK generates **OBS.ini** and log files in the path specified by the first parameter.

.. note::

   -  For details about SDK logging, see :ref:`Log Analysis <obs_20_1603>`.
