:original_name: obs_20_0108.html

.. _obs_20_0108:

Downloading an Object
=====================

This example shows how to download an object from a bucket to a directory and save the object as **test**.

Sample code:

.. code-block::

   static void test_get_object()
   {
       char *file_name = "./test";
       obs_object_info object_info;
       // Initialize option.
       obs_options option;
       init_obs_options(&option);
       option.bucket_options.host_name = "<your-endpoint>";
       option.bucket_options.bucket_name = "<Your bucketname>";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY.
       // Obtain an AK/SK pair on the management console.
       option.bucket_options.access_key = getenv("ACCESS_KEY_ID");
       option.bucket_options.secret_access_key = getenv("SECRET_ACCESS_KEY");
       // Set the object to be downloaded.
       memset(&object_info, 0, sizeof(obs_object_info));
       object_info.key = "<object key>";
       object_info.version_id = "<object version ID>";
       // Customize the structure for storing downloaded object data based on service requirements.
       get_object_callback_data data;
       data.ret_status = OBS_STATUS_BUTT;
       data.outfile = write_to_file(file_name);
       // Define range download parameters.
       obs_get_conditions getcondition;
       memset(&getcondition, 0, sizeof(obs_get_conditions));
       init_get_properties(&getcondition);
       // Customize callback function for download.
       obs_get_object_handler get_object_handler =
       {
           { &response_properties_callback, &get_object_complete_callback},
           &get_object_data_callback
       };
       get_object(&option, &object_info, &getcondition, 0, &get_object_handler, &data);
       if (OBS_STATUS_OK == data.ret_status) {
           printf("get object successfully. \n");
       }
       else
       {
           printf("get object failed(%s).\n", obs_get_status_name(data.ret_status));
       }
       fclose(data.outfile);
   }

.. note::

   For more information, see :ref:`Downloading an Object <obs_20_0501>`.
