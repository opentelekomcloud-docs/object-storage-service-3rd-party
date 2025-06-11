:original_name: obs_22_0501.html

.. _obs_22_0501:

Object Upload Overview (SDK for Python)
=======================================

You can use this API to upload an object to a specified bucket. In OBS, objects are basic data units that you can operate. OBS Python SDK provides many APIs for uploading objects using various methods:

-  :ref:`Text-based upload <obs_22_0901>`: Character strings are used as the data source of an object.
-  :ref:`Streaming upload <obs_22_0902>`: Readable objects that contain the **read** attribute are used as the data source of an object.
-  :ref:`File-based upload <obs_22_0903>`: Local files are used as the data source of objects.
-  :ref:`Multipart upload <obs_22_1003>`: Large files can be uploaded in multiple parts.
-  :ref:`Append upload <obs_22_0904>`: You can append data to an object.
-  :ref:`Resumable upload <obs_22_0905>`: It is an encapsulated and enhanced version of the multipart upload used for dealing with possible upload failures of large files when the network connection is unstable or a program crashes.
-  :ref:`Browser-based upload <obs_22_0907>`: You can upload objects to a specified bucket in HTML form.

SDK supports the upload of objects whose size ranges from 0 KB to 5 GB. For streaming upload, append upload, and file-based upload, data to be uploaded in a batch cannot be larger than 5 GB. If the file is larger than 5 GB, multipart upload (whose part size is smaller than 5 GB) is suitable. Browser-based upload allows files to be uploaded through a browser.

If you grant anonymous users the read permission for an object during the upload, anonymous users can access the object through a URL after the upload succeeds. The object URL is in the format of **https://bucket name.\ domain name/directory levels/object name**. If the object resides in the root directory of a bucket, its URL does not contain a directory level.
