:original_name: obs_25_0111.html

.. _obs_25_0111:

Listing Objects
===============

After objects are uploaded, you may want to view the objects contained in a bucket. Sample code is as follows:

.. code-block::

   ListObjectsRequest request = new ListObjectsRequest();
   request.BucketName = "bucketname";
   ListObjectsResponse response = client.ListObjects(request);
   foreach (ObsObject Object in response.ObsObjects)
   {
       Console.WriteLine("ObjectKey={0}, Size={1}", Object.ObjectKey, Object.Size);
   }

.. note::

   -  You can call **ListObjectsResponse.ObsObjects** to obtain the descriptions of all objects.
   -  In the previous sample code, 1000 objects will be listed, by default.
   -  For more information, see :ref:`Listing Objects <obs_25_0603>`.
