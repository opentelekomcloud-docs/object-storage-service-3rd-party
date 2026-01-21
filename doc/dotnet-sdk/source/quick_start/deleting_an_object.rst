:original_name: obs_25_0112.html

.. _obs_25_0112:

Deleting an Object
==================

This example deletes object **objectname** from bucket **bucketname**.

The example code is as follows:

.. code-block::

   DeleteObjectRequest request = new DeleteObjectRequest()
   {
       BucketName = "bucketname",
       ObjectKey = "objectname",
   };
   client.DeleteObject(request);

.. note::

   -  This example only deletes a single object. To delete objects in a batch, traverse objects and list to-be-deleted objects on your own.
   -  For details about deletion, see :ref:`Deleting Objects <obs_25_0604>`.
