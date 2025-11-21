:original_name: obs_20_1811.html

.. _obs_20_1811:

Multipart Upload APIs
=====================

You can upload a large file using multipart upload. Multipart upload is applicable to many scenarios. Below are some examples.

-  A file to be uploaded is larger than 100 MB.
-  The network connection to the OBS server breaks often.
-  The size of a file to be uploaded is unknown.

A multipart upload consists of the following steps:

#. :ref:`Initiating a Multipart Upload <obs_20_0405>`
#. :ref:`Uploading a Part <obs_20_1810>`
#. :ref:`Assembling Parts <obs_20_1809>` or :ref:`Aborting a Multipart Upload <obs_20_1806>`

Multipart upload is mainly used for large file upload or when the network connection is poor. This example uploads a large file in parts concurrently:

.. code-block::

   static void test_concurrent_upload_part(char *filename, char *key, uint64_t uploadSliceSize)
   {
       obs_status ret_status = OBS_STATUS_BUTT;
       // Create and initialize option.
       obs_options option;
       init_obs_options(&option);
       option.bucket_options.host_name = "<your-endpoint>";
       option.bucket_options.bucket_name = "<Your bucketname>";

       //Read the AK/SK from environment variables.
       option.bucket_options.access_key = getenv("ACCESS_KEY_ID");
       option.bucket_options.secret_access_key = getenv("SECRET_ACCESS_KEY");
       char *concurrent_upload_id;
       uint64_t uploadSize = uploadSliceSize;
       uint64_t filesize =0;
       // Initialize the put_properties structure.
       obs_put_properties put_properties;
       init_put_properties(&put_properties);
       // Large file information: file pointer, file size, number of parts determined by part size
       test_upload_file_callback_data data;
       memset(&data, 0, sizeof(test_upload_file_callback_data));
       filesize = get_file_info(filename,&data);
       data.noStatus = 1;
       data.part_size = uploadSize;
       data.part_num = (filesize % uploadSize == 0) ? (filesize / uploadSize) : (filesize / uploadSize +1);
       // Initialize the callback function of the uploading part.
       obs_response_handler Handler =
       {
            &response_properties_callback, &response_complete_callback
       };
       // Callback function for assembling parts
       obs_complete_multi_part_upload_handler complete_multi_handler =
       {
           {&response_properties_callback,
            &response_complete_callback},
           &CompleteMultipartUploadCallback
       };
       //Initiating the multipart upload returns uploadId: uploadIdReturn.
       char uploadIdReturn[256] = {0};
       int upload_id_return_size = 255;
       initiate_multi_part_upload(&option,key,upload_id_return_size,uploadIdReturn, &putProperties,
               0,&Handler, &ret_status);
       if (OBS_STATUS_OK == ret_status) {
           printf("test init upload part return uploadIdReturn(%s). \n", uploadIdReturn);
           strcpy(concurrent_upload_id,uploadIdReturn);
       }
       else
       {
           printf("test init upload part failed(%s).\n", obs_get_status_name(ret_status));
       }
       // Concurrent upload
       test_concurrent_upload_file_callback_data *concurrent_upload_file;
       concurrent_upload_file =(test_concurrent_upload_file_callback_data *)malloc(
                       sizeof(test_concurrent_upload_file_callback_data)*(data.part_num+1));
       if(concurrent_upload_file == NULL)
       {
            printf("malloc test_concurrent_upload_file_callback_data failed!!!");
            return ;
       }
       test_concurrent_upload_file_callback_data *concurrent_upload_file_complete =
                                 concurrent_upload_file;
       start_upload_threads(data, concurrent_upload_id,filesize, key, option, concurrent_upload_file_complete);
       // Assemble parts.
       obs_complete_upload_Info *upload_Info = (obs_complete_upload_Info *)malloc(
                   sizeof(obs_complete_upload_Info)*data.part_num);
       for(i=0; i<data.part_num; i++)
       {
           upload_Info[i].part_number = concurrent_upload_file_complete[i].part_num;
           upload_Info[i].etag = concurrent_upload_file_complete[i].etag;
       }
       complete_multi_part_upload(&option, key, uploadIdReturn, data.part_num,upload_Info,&putProperties,&complete_multi_handler,&ret_status);
       if (ret_status == OBS_STATUS_OK) {
           printf("test complete upload successfully. \n");
       }
       else
       {
           printf("test complete upload failed(%s).\n", obs_get_status_name(ret_status));
       }
       if(concurrent_upload_file)
       {
           free(concurrent_upload_file);
           concurrent_upload_file = NULL;
       }
       if(upload_Info)
       {
           free(upload_Info);
           upload_Info = NULL;
       }
   }

.. note::

   When uploading a large file in parts, you need to use the **Offset** and **PartSize** parameters to specify the start and end positions of each part in the file.

.. caution::

   If the concurrency value is too great, timeout may occur due to network instability. In such case, you need to reduce that value.
