:original_name: obs_25_0000.html

.. _obs_25_0000:

Before You Start
================

This section describes version compatibility and important notes about Object Storage Service (OBS) SDK for .NET.

Compatibility
-------------

-  Recommended .NET versions: .NET Framework 3.5, 4.0, or 4.5; .NET Core 2.0 or 3.1; .NET 6 or 7
-  The namespaces used in earlier versions (2.\ *x.x*) are reorganized and all public APIs are now in namespaces **OBS** and **OBS.Model**.
-  API functions are redesigned and not compatible with those provided by earlier versions (2.\ *x.x*).

Important Notes
---------------

-  Ensure that you are familiar with OBS basic concepts in `Help Center <https://docs.otc.t-systems.com/en-us/usermanual/obs/en-us_topic_0045853692.html>`__, such as buckets, objects, regions, and access keys (AKs/SKs).
-  You can see :ref:`General Examples of ObsClient <obs_25_0113>` to learn how to call OBS .NET SDK APIs in a general manner.
-  After an API is called using an instance of **ObsClient**, if no exception is thrown, the return value is valid. If an exception is thrown, the operation fails, and you can obtain the exception details from the instance of :ref:`ObsException <obs_25_1606>`.
-  After an API is successfully called using an instance of **ObsClient**, an instance of :ref:`HeaderResponse <obs_25_1605>` that contains response headers will be returned.
