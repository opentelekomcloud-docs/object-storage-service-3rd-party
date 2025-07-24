:original_name: obs_33_0001.html

.. _obs_33_0001:

Before You Start
================

This section describes the important notes about Object Storage Service (OBS) SDK for Go.

Important Notes
---------------

-  Some features are available only for some regions. If **405** HTTP status code is returned for a certain feature API, check whether the region supports that feature.
-  Namespace: **obs** is used as the namespace to be compatible with earlier OBS 2.0 versions (2.2.\ *x*). All data types and API definitions contained in the SDK belong to this namespace. Before using OBS SDK for Go, you need to import **obs**.
-  API functions are compatible with earlier OBS 2.0 versions (2.2.\ *x*).
