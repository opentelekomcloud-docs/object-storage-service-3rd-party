:original_name: obs_21_0614.html

.. _obs_21_0614:

Multipart Upload Overview
=========================

Function
--------

You can upload large files using multipart upload. Multipart upload is applicable to many scenarios, including:

-  Files to be uploaded are larger than 100 MB.
-  The network condition is poor. Connection to the OBS server is constantly down.
-  Sizes of files to be uploaded are uncertain.

A multipart upload has the following advantages:

-  Higher throughput: You can upload parts in parallel to improve throughput.
-  Quick recovery from network failures: Uploading an object in parts helps minimize the impact of upload interruptions caused by network failures.
-  Flexible suspension and resumption of object uploads: You can upload parts at any time. A multipart upload will not expire after being initiated. You must explicitly complete or abort a multipart upload.
-  No need to know the size before uploading an object: You can upload an object while creating it.

A multipart upload consists of the following steps:

#. :ref:`Initiate a multipart upload <obs_21_0615>` (**ObsClient.initiateMultipartUpload**).
#. :ref:`Upload parts one by one or concurrently <obs_21_0616>` (**ObsClient.uploadPart**).
#. :ref:`Assemble parts <obs_21_0617>` (**ObsClient.completeMultipartUpload**) or :ref:`abort the multipart upload <obs_21_0619>` (**ObsClient.abortMultipartUpload**).
