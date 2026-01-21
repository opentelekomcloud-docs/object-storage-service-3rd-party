:original_name: obs_25_0109.html

.. _obs_25_0109:

Uploading an Object
===================

This example uploads string **Hello OBS** to bucket **bucketname** as object **objectname**.

The example code is as follows:

.. code-block::

   PutObjectRequest request = new PutObjectRequest
   {
       BucketName = "bucketname",
       ObjectKey = "objectname",
       InputStream = new MemoryStream(Encoding.UTF8.GetBytes("Hello OBS"))
   };
   client.PutObject(request);

.. note::

   -  For more information, see :ref:`Object Upload Overview <obs_25_0401>`.
