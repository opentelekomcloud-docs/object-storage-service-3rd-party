:original_name: obs_33_0501.html

.. _obs_33_0501:

Object API Overview
===================

OBS SDK for Go provides methods for accessing OBS using object-related APIs (except for resumable transfer APIs) with signed URLs. Such methods may contain the following three parameters (except for **ObsClient.PutFileWithSignedUrl**):

-  A signed URL
-  Headers required in a request made by using a signed URL
-  Data carried in a request (optional)

For details about how to generate a signed URL, see :ref:`Creating a Signed URL <obs_33_0601>`.
