:original_name: obs_25_0401.html

.. _obs_25_0401:

Object Upload Overview
======================

In OBS, objects are basic data units that users can perform operations on. OBS .NET SDK provides abundant APIs for object upload in the following methods:

-  :ref:`Performing a Streaming Upload <obs_25_0402>`
-  :ref:`Performing a File-Based Upload <obs_25_0403>`
-  :ref:`Performing an Asynchronous Upload <obs_25_0404>`
-  :ref:`Performing a Multipart Upload <obs_25_0408>`
-  :ref:`Performing an Appendable Upload <obs_25_0410>`
-  :ref:`Performing a Resumable Upload <obs_25_0412>`

The SDK supports the upload of objects whose size ranges from 0 KB to 5 GB. If a file is smaller than 5 GB, streaming upload, appendable upload, and file-based upload are applicable. If the file is larger than 5 GB, multipart upload (whose part size is smaller than 5 GB) is suitable.

If you grant anonymous users the read permission for an object during the upload, anonymous users can access the object through a URL after the upload is complete. The object URL is in the format of **https://bucket name.\ domain name/directory levels/object name**. If the object resides in the root directory of the bucket, its URL does not contain directory levels.
