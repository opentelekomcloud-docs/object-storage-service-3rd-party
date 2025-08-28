:original_name: obs_21_2115.html

.. _obs_21_2115:

How Can I Perform a Download in Multipart Mode?
===============================================

In a multipart download, you can specify the range of data to be downloaded. The procedure is as follows:

#. You need to initialize an instance of ObsClient by using AK, SK, and endpoint.
#. Specify the bucket name and object name to initialize **GetObjectRequest**. Call **GetObjectRequest.setRangeStart** and **GetObjectRequest.setRangeEnd** to set the start and end points of the object data to be downloaded.
#. Call **ObsClient.getObject** to send the **GetObjectRequest** request in step 2 to download the data in multipart mode.

For details, see :ref:`Downloading an Object - Range-Based <obs_21_0703>`.
