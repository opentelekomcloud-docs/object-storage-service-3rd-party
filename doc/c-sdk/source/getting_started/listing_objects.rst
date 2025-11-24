:original_name: obs_20_0109.html

.. _obs_20_0109:

Listing Objects
===============

This example shows how to list all objects in a bucket.

Sample code:

.. code-block::

   static void test_list_bucket_objects()
   {
       // Create and initialize option.
       obs_options option;
       init_obs_options(&option);
       option.bucket_options.host_name = "<your-endpoint>";
       option.bucket_options.bucket_name = "<Your bucketname>";

   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY.
       // Obtain an AK/SK pair on the management console.
       option.bucket_options.access_key = getenv("ACCESS_KEY_ID");
       option.bucket_options.secret_access_key = getenv("SECRET_ACCESS_KEY");

       // Set response callback function.
       obs_list_objects_handler list_bucket_objects_handler =
       {
           { &response_properties_callback, &list_objects_complete_callback },
           &list_objects_callback
       };

       // Customize callback data.
       list_bucket_callback_data data;
       memset(&data, 0, sizeof(list_bucket_callback_data));
       // List objects.
       list_bucket_objects(&option, "<prefix>", "<marker>", "<delimiter>", "<maxkeys>", &list_bucket_objects_handler, &data);
       if (OBS_STATUS_OK == data.ret_status) {
           printf("list bucket objects successfully. \n");
       }
       else
       {
           printf("list bucket objects failed(%s).\n",
               obs_get_status_name(data.ret_status));
       }
   }

.. note::

   -  For more information, see :ref:`Listing Objects in a Bucket <obs_20_0603>`.
