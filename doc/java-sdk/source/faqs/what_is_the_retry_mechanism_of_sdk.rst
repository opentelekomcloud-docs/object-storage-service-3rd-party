:original_name: obs_21_2109.html

.. _obs_21_2109:

What Is the Retry Mechanism of SDK?
===================================

SDK uses the **maxErrorRetry** parameter configured in :ref:`Creating and Configuring an OBS Client <obs_21_0202>` to retry. The default value for retry times is **3**. **0** to **5** is recommended.

If the network connection is abnormal or the server returns the 5\ *XX* error when an ObsClient API is called, the SDK performs an exponential backoff retry.

.. important::

   -  For **ObsClient.putObject**, when the data source is an InputStream other than FileInputStream, the SDK does not retry when an I/O exception occurs because the data stream cannot be re-read. The upper-layer application needs to retry.
   -  When **ObsClient.getObject** is successfully called and **ObsObject** is returned, the SDK does not retry when an I/O exception occurs during data reading from **ObsObject.getObjectContent** because this situation is beyond the scope of the processing logic of the SDK. The upper-layer application needs to retry.
