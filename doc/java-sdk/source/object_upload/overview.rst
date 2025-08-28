:original_name: obs_21_0601.html

.. _obs_21_0601:

Overview
========

In OBS, objects are basic data units that users can perform operations on. OBS Java SDK provides abundant APIs for object upload in the following methods:

-  :ref:`Streaming <obs_21_0602>`
-  :ref:`File-based <obs_21_0603>`
-  :ref:`Multipart <obs_21_0607>`
-  :ref:`Appendable <obs_21_0609>`
-  :ref:`Resumable <obs_21_0611>`
-  :ref:`Browser-based <obs_21_0612>`

The SDK supports the upload of objects whose size ranges from 0 KB to 5 GB. For streaming upload, appendable upload, and file-based upload, data to be uploaded cannot be larger than 5 GB. If the file is larger than 5 GB, multipart upload (where each part is smaller than 5 GB) is suitable. Browser-based upload allows files to be uploaded through a browser.

If you grant anonymous users the read permission for an object during the upload, anonymous users can access the object through a URL after the upload is complete. The object URL is in the format of **https://bucket name.\ domain name/directory level/object name**. If the object resides in the root directory of the bucket, its URL does not contain directory levels.
