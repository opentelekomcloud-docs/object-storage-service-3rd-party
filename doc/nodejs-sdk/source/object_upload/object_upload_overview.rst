:original_name: obs_29_0401.html

.. _obs_29_0401:

Object Upload Overview
======================

In OBS, objects are basic data units that users can perform operations on. OBS Node.js SDK provides abundant APIs for object upload in the following methods:

-  :ref:`Uploading an Object - Text-Based <obs_29_0402>`
-  :ref:`Uploading an Object - Streaming <obs_29_0403>`
-  :ref:`Uploading an Object - File-Based <obs_29_0404>`
-  :ref:`Initiating a Multipart Upload <obs_29_1902>`
-  :ref:`Uploading an Object - Append <obs_29_0409>`
-  :ref:`Uploading an Object - Resumable <obs_29_0411>`
-  :ref:`Uploading an Object - Browser-Based <obs_29_0412>`

The SDK supports the upload of objects whose size ranges from 0 KB to 5 GB. For streaming upload, appendable upload, and file-based upload, data to be uploaded at a time cannot be larger than 5 GB. If the file is larger than 5 GB, multipart upload (whose part size is smaller than 5 GB) is suitable. Browser-based upload allows files to be uploaded through a browser.

If you grant anonymous users the read permission for an object during the upload, anonymous users can access the object through a URL after the upload is complete. The object URL is in the format of **https://bucket name.\ domain name/directory levels/object name**. If the object resides in the root directory of the bucket, its URL does not contain directory levels.
