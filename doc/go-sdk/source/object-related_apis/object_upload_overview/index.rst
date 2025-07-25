:original_name: obs_23_0401.html

.. _obs_23_0401:

Object Upload Overview
======================

In OBS, objects are basic data units that you can operate. OBS Go SDK provides abundant APIs for object upload in the following methods:

-  :ref:`Uploading an Object - Streaming <obs_23_0402>`
-  :ref:`Uploading an Object - File-Based <obs_23_0403>`
-  :ref:`Uploading a Part <obs_33_0512>`
-  :ref:`Uploading an Object - Resumable <obs_23_0409>`

SDK supports the upload of objects whose size ranges from 0 KB to 5 GB. If a file is smaller than 5 GB, streaming upload and file-based upload are applicable. If the file is larger than 5 GB, multipart upload (whose part size is smaller than 5 GB) is suitable.

If you grant anonymous users the read permission for an object during the upload, anonymous users can access the object through a URL after the upload is complete. The object URL is in the format of **https://**\ *bucket name*\ **.**\ *domain name*\ **/**\ *directory levels*\ **/**\ *object name*. If the object resides in the root directory of a bucket, its URL does not contain a directory level.

-  :ref:`Uploading an Object - Streaming <obs_23_0402>`
-  :ref:`Uploading an Object - File-Based <obs_23_0403>`
-  :ref:`Uploading an Object - Append <obs_23_0404>`
-  :ref:`Uploading an Object - Resumable <obs_23_0409>`

.. toctree::
   :maxdepth: 1
   :hidden: 

   uploading_an_object_streaming
   uploading_an_object_file-based
   uploading_an_object_append
   uploading_an_object_resumable
