:original_name: obs_29_0801.html

.. _obs_29_0801:

Versioning Overview
===================

You can use versioning to store multiple versions of an object in a bucket.

When versioning is enabled for a bucket, OBS keeps multiple versions of an object in the bucket, allowing you to easily retrieve and restore historical versions or recover data in the event of accidental changes or application failures.

By default, versioning is disabled for new OBS buckets. In this case, if a newly uploaded object is using the name of the previously uploaded one, the new object will overwrite the previous one.

For details about different versioning operations, see:

-  :ref:`Configuring Versioning for a Bucket <obs_29_0802>`
-  :ref:`Viewing the Versioning Status of a Bucket <obs_29_0803>`
-  :ref:`Deleting an Object Version <obs_29_0809>`
