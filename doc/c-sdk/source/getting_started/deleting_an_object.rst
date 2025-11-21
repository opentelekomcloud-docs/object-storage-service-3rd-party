:original_name: obs_20_0110.html

.. _obs_20_0110:

Deleting an Object
==================

This example shows how to delete an object from a bucket.

Sample code:

.. code-block::

   static void test_delete_object()
   {
       obs_status ret_status = OBS_STATUS_BUTT;
       // Create and initialize object information.
       obs_object_info object_info;
       memset(&object_info, 0, sizeof(obs_object_info));
       object_info.key = "<Your Key>";
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
       obs_response_handler responseHandler =
       {
           &response_properties_callback,
           &response_complete_callback
       };
       // Delete an object.
       delete_object(&option,&object_info,&responseHandler, &ret_status);
       if (OBS_STATUS_OK == ret_status)
       {
           printf("delete object successfully. \n");
       }
       else
       {
           printf("delete object failed(%s).\n", obs_get_status_name(ret_status));
       }
   }

.. note::

   -  For more information, see :ref:`Deleting an Object <obs_20_0604>`.
