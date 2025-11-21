:original_name: obs_29_0202.html

.. _obs_29_0202:

Creating an Instance of ObsClient
=================================

**ObsClient** functions as the Node.js client for accessing OBS. It offers callers a series of APIs for interaction with OBS and is used for managing and operating resources, such as buckets and objects, stored in OBS. To use OBS Node.js SDK to send a request to OBS, you need to initialize an instance of **ObsClient** and modify parameters related to initial configurations of the instance based on actual needs.

By Using the Constructor
------------------------

-  Sample code for creating an ObsClient instance using permanent access keys (AKs/SKs):

   .. code-block::

      // Import the OBS library.
      // Use npm to install the client.
      const ObsClient = require("esdk-obs-nodejs");
      // Use the source code to install the client.
      // var ObsClient = require('./lib/obs');

      // Create an instance of ObsClient.
      const obsClient = new ObsClient({
        // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
        // Obtain an AK/SK pair on the management console.
        access_key_id: process.env.ACCESS_KEY_ID,
        secret_access_key: process.env.SECRET_ACCESS_KEY,
        // Enter the endpoint of the region where the bucket is located.
        server: "https://your-endpoint"
      });

      // Use the instance to access OBS.

      // Close the ObsClient instance.
      // obsClient.close();

-  Sample code for creating an ObsClient instance using temporary security credentials (AKs/SKs and security tokens):

   .. code-block::

      // Import the OBS library.
      // Use npm to install the client.
      const ObsClient = require("esdk-obs-nodejs");
      // Use the source code to install the client.
      // var ObsClient = require('./lib/obs');

      // Create an instance of ObsClient.
      const obsClient = new ObsClient({
        // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
        // Obtain an AK/SK pair on the management console.
        access_key_id: process.env.ACCESS_KEY_ID,
        secret_access_key: process.env.SECRET_ACCESS_KEY,
        // If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
        security_token: process.env.SECURITY_TOKEN,
        // Enter the endpoint of the region where the bucket is located.
        server: "https://your-endpoint"
      });

      // Use the instance to access OBS.

      // Close the ObsClient instance.
      // obsClient.close();

By Using the Factory Method
---------------------------

-  Sample code for creating an ObsClient instance using permanent access keys (AKs/SKs):

   .. code-block::

      // Import the OBS library.
      // Use npm to install the client.
      var ObsClient = require('esdk-obs-nodejs');
      // Use the source code to install the client.
      // var ObsClient = require('./lib/obs');

      // Initialize an ObsClient instance by using the factory method.
      var obsClient = new ObsClient();
      obsClient.factory({
        // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
        // Obtain an AK/SK pair on the management console.
        access_key_id: process.env.ACCESS_KEY_ID,
        secret_access_key: process.env.SECRET_ACCESS_KEY,
        // Enter the endpoint of the region where the bucket is located.
        server: "https://your-endpoint"
      });

      // Use the instance to access OBS.

      // Close the ObsClient instance.
      // obsClient.close();

-  Sample code for creating an ObsClient instance using temporary security credentials (AKs/SKs and security tokens):

   .. code-block::

      // Import the OBS library.
      // Use npm to install the client.
      var ObsClient = require('esdk-obs-nodejs');
      // Use the source code to install the client.
      // var ObsClient = require('./lib/obs');

      // Initialize an ObsClient instance by using the factory method.
      var obsClient = new ObsClient();
      obsClient.factory({
        // Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
        // Obtain an AK/SK pair on the management console.
        access_key_id: process.env.ACCESS_KEY_ID,
        secret_access_key: process.env.SECRET_ACCESS_KEY,
        // If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
        security_token: process.env.SECURITY_TOKEN,
        // Enter the endpoint of the region where the bucket is located.
        server: "https://your-endpoint"
      });

      // Use the instance to access OBS.

      // Close the ObsClient instance.
      // obsClient.close();

.. note::

   -  The project can contain one or more ObsClient instances.

   -  An ObsClient instance cannot be used again after it is closed by calling the close method.
