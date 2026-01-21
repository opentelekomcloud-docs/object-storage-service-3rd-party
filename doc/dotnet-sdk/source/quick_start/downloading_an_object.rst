:original_name: obs_25_0110.html

.. _obs_25_0110:

Downloading an Object
=====================

This example downloads object **objectname** from bucket **bucketname**.

The example code is as follows:

.. code-block::

   GetObjectRequest request = new GetObjectRequest()
   {
       BucketName = "bucketname",
       ObjectKey = "objectname",
   };
   using (GetObjectResponse response = client.GetObject(request))
   {
       //Save the object locally.
       string dest = "savepath";
       if (!File.Exists(dest))
       {
           response.WriteResponseStreamToFile(dest);
       }
   }

.. note::

   For more information, see :ref:`Object Download Overview <obs_25_0501>`.
