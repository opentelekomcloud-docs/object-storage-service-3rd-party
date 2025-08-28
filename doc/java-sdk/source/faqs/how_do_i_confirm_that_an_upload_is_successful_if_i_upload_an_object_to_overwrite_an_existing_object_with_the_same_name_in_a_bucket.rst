:original_name: obs_21_2117.html

.. _obs_21_2117:

How Do I Confirm that an Upload is Successful If I Upload an Object to Overwrite an Existing Object with the Same Name in a Bucket?
===================================================================================================================================

After the upload is complete, you can call **ObsClient.getObjectMetadata** to obtain the size and last modification time of the newly uploaded object and compare them with those of the overwritten object.

If the sizes are the same and the last modification time of the new object is later than that of the overwritten object, the upload succeeded. Otherwise, the upload failed.

For details about how to call **ObsClient.getObjectMetadata**, see :ref:`Obtaining Object Metadata <obs_21_0801>`.
