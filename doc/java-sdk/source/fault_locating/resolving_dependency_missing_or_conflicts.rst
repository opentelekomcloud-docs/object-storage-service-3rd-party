:original_name: obs_21_0303.html

.. _obs_21_0303:

Resolving Dependency Missing or Conflicts
=========================================

Dependency missing and dependency conflict are commonly encountered in Java development or during SDK integration. If error message "ClassNotFoundException" or "NoClassDefFoundError" is reported during application compilation and running, check whether this is a dependency-triggered problem. If yes, perform the following steps to locate and rectify the fault.

Dependency Missing
------------------

The following table lists the third-party components (including their versions) that the latest SDK depends on.

=================== ======= =======================================
Dependency          Version Description
=================== ======= =======================================
okhttp              4.11.0  Used to send HTTP requests.
okio                3.5.0   Component of OkHttp
java-xmlbuilder     1.3     Used to construct and parse XML files.
jackson-core        2.13.3  Used to construct and parse JSON files.
jackson-databind    2.15.0  Component of jackson-core
jackson-annotations 2.13.3  Component of jackson-core
=================== ======= =======================================

Dependency Conflict
-------------------

If your project has multiple versions of OBS Java SDK packages or third-party dependencies, dependency conflicts may occur. If there are SDKs of earlier versions, delete them and use the latest version. If there are multiple versions of third-party dependencies, replace the conflict ones with the versions required by the SDK.
