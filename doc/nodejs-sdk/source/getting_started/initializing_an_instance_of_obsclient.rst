:original_name: obs_29_0107.html

.. _obs_29_0107:

Initializing an Instance of ObsClient
=====================================

Each time you want to send an HTTP/HTTPS request to OBS, you must create an instance of **ObsClient**. Sample code is as follows:

.. code-block::

   // Import the OBS library.
   // Use npm to install the client.
   const ObsClient = require("esdk-obs-nodejs");
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');

   // Create an instance of ObsClient.
   const obsClient = new ObsClient({
     //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
     // Obtain an AK/SK pair on the management console.
     access_key_id: process.env.ACCESS_KEY_ID,
     secret_access_key: process.env.SECRET_ACCESS_KEY,
     // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
     // security_token: process.env.SECURITY_TOKEN,
     // Enter the endpoint of the region where the bucket is located.
     server: "https://your-endpoint"
   });

   // Use the instance to access OBS.

   // Close the ObsClient instance.
   // obsClient.close();

.. caution::

   -  JavaScript is an asynchronous programming language. Therefore, you cannot call the close method when accessing OBS.
   -  An ObsClient instance cannot be used again after it is closed by calling **obsClient.close**.

.. note::

   -  For more information, see chapter "Initialization."
   -  For logging configuration, see :ref:`Configuring SDK Logging <obs_29_0204>`.
