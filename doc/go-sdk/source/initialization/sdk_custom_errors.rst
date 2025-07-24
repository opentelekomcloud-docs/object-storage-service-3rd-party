:original_name: obs_33_0104.html

.. _obs_33_0104:

SDK Custom Errors
=================

Function
--------

Each time you fail to call an **ObsClient** API, an SDK custom error — containing an HTTP status code, OBS error code, and error message — is returned, to help you locate and rectify the fault.

Type Definition
---------------

.. code-block::

   type ObsError struct

Parameters
----------

+-----------------+---------------------+----------------------------------------------+
| Parameter       | Type                | Description                                  |
+=================+=====================+==============================================+
| StatusCode      | int                 | HTTP status code                             |
+-----------------+---------------------+----------------------------------------------+
| RequestId       | string              | Request ID returned by the OBS server        |
+-----------------+---------------------+----------------------------------------------+
| ResponseHeaders | map[string][]string | HTTP response headers                        |
+-----------------+---------------------+----------------------------------------------+
| Status          | string              | Reason description                           |
+-----------------+---------------------+----------------------------------------------+
| Code            | string              | Error code returned by the OBS server        |
+-----------------+---------------------+----------------------------------------------+
| Message         | string              | Error description returned by the OBS server |
+-----------------+---------------------+----------------------------------------------+
| Resource        | string              | Bucket and object related to the error       |
+-----------------+---------------------+----------------------------------------------+
| HostId          | string              | Requested server ID                          |
+-----------------+---------------------+----------------------------------------------+
