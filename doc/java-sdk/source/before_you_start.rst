:original_name: obs_21_0101.html

.. _obs_21_0101:

Before You Start
================

This section describes version compatibility and important notes about Object Storage Service (OBS) SDK for Java.

Compatibility
-------------

-  Recommended JDK versions: JDK 8 or later
-  Third-party dependencies: This version is not completely compatible with earlier versions (2.1.\ *x*). OkHttp 3 should be used to replace HttpClient4.\ *x*.
-  Namespace: This version is compatible with earlier versions (2.1.\ *x*). All external APIs are contained in the **com.obs.services**, **com.obs.services.model**, and **com.obs.services.exception** packages.
-  API functions: This version is compatible with earlier versions (2.1.\ *x*).
-  The earlier 2.\ *X* versions are no longer maintained. You are advised to upgrade them to the latest version as soon as possible.

Important Notes
---------------

-  Make sure that you are familiar with OBS basic concepts in `Help Center <https://docs.otc.t-systems.com/en-us/usermanual/obs/en-us_topic_0045853692.html>`__, such as buckets, objects, regions, and access keys (AKs/SKs).
-  You can learn about how to call an API through the OBS SDK for Java by referring to :ref:`Using an OBS Client <obs_21_0100__section8686104202916>`.
-  After an API is called using an instance of **ObsClient**, if no exception is thrown, the return value is valid. If an exception is thrown, the operation fails. For details about errors, see :ref:`SDK Exceptions <obs_21_2005>`.
-  After an API is successfully called using an instance of **ObsClient**, a class or sub-class instance of :ref:`HeaderResponse <obs_21_2003>` that contains response headers will be returned.
-  Some features are available only in some regions. If an API call returns the 405 HTTP status code, check whether the region supports this feature.
