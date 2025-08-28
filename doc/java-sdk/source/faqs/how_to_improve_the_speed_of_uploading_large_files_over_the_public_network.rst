:original_name: obs_21_2112.html

.. _obs_21_2112:

How to Improve the Speed of Uploading Large Files over the Public Network?
==========================================================================

If a file exceeds 100 MB, you are advised to upload the file using multipart upload.

Multipart upload refers to splitting an object into multiple parts and uploading them separately. Each part is a contiguous portion of the object's data. You can upload parts in any sequence. A part can be reloaded after an upload failure, without affecting other parts. Uploading multiple parts of an object using multiple threads concurrently can greatly improve the transmission efficiency.

For code examples, see :ref:`Multipart Upload <obs_21_0607>`.
