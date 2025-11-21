:original_name: obs_20_0107.html

.. _obs_20_0107:

Uploading an Object
===================

The data flow is saved to **callback_data** (see the **callback_data** definition in :ref:`Uploading an Object - Streaming <obs_20_0401>`). Use the callback function **put_object_data_callback** defined in **obs_put_object_handler** to copy the content of the uploaded object to **buffer**, a character pointer parameter of the callback function.

For more information, see :ref:`Uploading an Object - Streaming <obs_20_0401>`.

Sample code:

.. code-block::

   static void test_put_object_from_buffer()
   {
        // Buffer to be uploaded
       char *buffer = "abcdefg";
        // Length of the buffer to be uploaded
       int buffer_size = strlen(buffer);
        // Name of an object to be uploaded
       char *key = "put_buffer_test";

       // Initialize option.
       obs_options option;
       init_obs_options(&option);
       option.bucket_options.host_name = "<your-endpoint>";
       option.bucket_options.bucket_name = "<Your bucket name>";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY.
       // Obtain an AK/SK pair on the management console.
       option.bucket_options.access_key = getenv("ACCESS_KEY_ID");
       option.bucket_options.secret_access_key = getenv("SECRET_ACCESS_KEY");

       // Initialize the properties of an object to be uploaded.
       obs_put_properties put_properties;
       init_put_properties(&put_properties);
       // Customize the structure for storing uploaded data.
       put_buffer_object_callback_data data;
       memset(&data, 0, sizeof(put_buffer_object_callback_data));
       // Assign the buffer value to the structure.
       data.put_buffer = buffer;
       // Set buffersize.
       data.buffer_size = buffer_size;
       // Set the callback function. The corresponding callback function needs to be implemented.
       obs_put_object_handler putobjectHandler =
       {
           { &response_properties_callback, &put_buffer_complete_callback },
             &put_buffer_data_callback
       };
       put_object(&option, key, buffer_size, &put_properties,0,&putobjectHandler,&data);
       if (OBS_STATUS_OK == data.ret_status) {
           printf("put object from buffer successfully. \n");
       }
       else
       {
           printf("put object from buffer failed(%s).\n", obs_get_status_name(data.ret_status));
       }
   }
