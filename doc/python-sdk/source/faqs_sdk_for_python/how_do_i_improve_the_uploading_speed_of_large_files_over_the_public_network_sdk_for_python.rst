:original_name: obs_22_1614.html

.. _obs_22_1614:

How Do I Improve the Uploading Speed of Large Files over the Public Network? (SDK for Python)
=============================================================================================

If a file exceeds 100 MB, you are advised to upload the file using multipart upload.

Multipart upload refers to splitting an object into multiple parts and uploading them separately. Each part is a contiguous portion of the object's data. You can upload parts in any sequence. A part can be reloaded after an upload failure, without affecting other parts. Uploading multiple parts of an object using multiple threads concurrently can greatly improve the transmission efficiency.

For details about the sample code, see :ref:`APIs Related to Multipart Upload (SDK for Python) <obs_22_1000>`.
