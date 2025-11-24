:original_name: obs_29_1602.html

.. _obs_29_1602:

SDK Common Results
==================

After you call an API in an instance of the **ObsClient** class, a common result object will be returned if no exception is thrown. The following table lists the fields of the object:

+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| Parameter       |              | Type                                                                 | Description                                                                                                        |
+=================+==============+======================================================================+====================================================================================================================+
| CommonMsg       |              | Object                                                               | Common information generated after the API is called, including HTTP status code and error code.                   |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| ``-``           | Status       | Number                                                               | HTTP status code. If the value is smaller than **300**, the operation succeeds. Otherwise, the operation fails.    |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
|                 | Code         | String                                                               | Error code returned by the OBS server. If **Status** is smaller than **300**, the value is null.                   |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
|                 | Message      | String                                                               | Error description returned by the OBS server. If **Status** is smaller than **300**, the value is null.            |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
|                 | HostId       | String                                                               | Requested Server ID. If **Status** is smaller than **300**, the value is null.                                     |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
|                 | RequestId    | String                                                               | Request ID returned by the OBS server                                                                              |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
|                 | Id2          | String                                                               | Request ID2 returned by the OBS server                                                                             |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
|                 | Indicator    | String                                                               | Detailed error code returned by the OBS server. If **Status** is smaller than **300**, the value is null.          |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| InterfaceResult |              | Object                                                               | Result data generated after the operation is successful. If **Status** is greater than **300**, the value is null. |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
| ``-``           | RequestId    | String                                                               | Request ID returned by the OBS server.                                                                             |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
|                 | Id2          | String                                                               | Request ID2 returned by the OBS server                                                                             |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
|                 | Other fields | For details, see the **Response** area in the corresponding section. |                                                                                                                    |
+-----------------+--------------+----------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+

Sample code:

.. code-block::

   // Import the OBS library.
   // Use npm to install the client.
   var ObsClient = require('esdk-obs-nodejs');
   // Use the source code to install the client.
   // var ObsClient = require('./lib/obs');

   // Create an instance of ObsClient.
   const obsClient = new ObsClient({
       //Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
       //Obtain an AK/SK pair on the management console.
       access_key_id: process.env.ACCESS_KEY_ID,
       secret_access_key: process.env.SECRET_ACCESS_KEY,

       server : 'https://your-endpoint'
   });

   // Call APIs to perform operations, such as downloading an object.
   obsClient.getObject({
          Bucket : 'bucketname',
          Key : 'objectname',
   }, (err, result) => {
          if(!err){
                 if(result.CommonMsg.Status < 300){
                       // Obtain RequestId.
                        console.log('RequestId-->' + result.InterfaceResult.RequestId);
                        // Obtain other parameters.
                        console.log('Content-->' + result.InterfaceResult.Content.toString());
                 }else{
                        // Obtain Code and Message.
                        console.log('Code-->' + result.CommonMsg.Code);
                        console.log('Message-->' + result.CommonMsg.Message);
                 }
          }
   });
