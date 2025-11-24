:original_name: obs_20_1202.html

.. _obs_20_1202:

Hosting Website Files in a Bucket
=================================

You can perform the following to implement website file hosting:

#. Upload a website file to your bucket in OBS as an object and set the MIME type for the object.
#. Set the object ACL to public read.
#. Access the object using a browser.

Code Examples: Website File Hosting
-----------------------------------

This example implements website file hosting.

::

   #include "eSDKOBS.h"
   #include <stdio.h>
   #include <sys/stat.h>
   // The response callback function. The content of properties in the callback can be recorded in callback_data (custom callback data).
   obs_status response_properties_callback(const obs_response_properties *properties, void *callback_data);
   int put_file_data_callback(int buffer_size, char *buffer,
       void *callback_data);
   void put_file_complete_callback(obs_status status,
       const obs_error_details *error,
       void *callback_data);
   typedef struct put_file_object_callback_data
   {
       FILE *infile;
       uint64_t content_length;
       obs_status ret_status;
   } put_file_object_callback_data;
   uint64_t open_file_and_get_length(char *localfile, put_file_object_callback_data *data);
   int main()
   {
       // The following code shows how to implement website file hosting:
       // Call the obs_initialize method at the program entry to initialize global resources such as the network and memory.
       obs_initialize(OBS_INIT_ALL);
       obs_options options;
       // Create and initialize options, including the access domain name (host_name), access keys (access_key_id and access_key_secret), bucket name (bucket_name), and bucket storage class (storage_class).
       init_obs_options(&options);
       // For host_name, enter the endpoint of the region where the bucket is located.
       options.bucket_options.host_name = "your-endpoint";
       // Hard-coded or plaintext AK and SK are risky. For security purposes, encrypt your AK and SK and store them in the configuration file or environment variables.
       // In this example, the AK and SK are stored in environment variables for identity authentication. Before running the code in this example, configure local environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY.
       options.bucket_options.access_key = getenv("ACCESS_KEY_ID");
       options.bucket_options.secret_access_key = getenv("SECRET_ACCESS_KEY");
       // Specify the bucket name, for example, example-bucket-name.
       char * bucketName = "example-bucket-name";
       options.bucket_options.bucket_name = bucketName;
       // Initialize the properties of the object to be uploaded.
       obs_put_properties put_properties;
       init_put_properties(&put_properties);
       // Name of the object to be uploaded
       char *key = "example_put_file_html_test.html";
       // Uploaded file
       char file_name[256] = "./example_local_file_test.html";
       // Set the MIME type.
       put_properties.content_type = "text/html";
       // Set the object ACL to public read.
       put_properties.canned_acl = OBS_CANNED_ACL_PUBLIC_READ;
       put_properties.content_disposition_filename = "";
       uint64_t content_length = 0;
       // Initialize the structure for storing the uploaded data.
       put_file_object_callback_data data;
       memset(&data, 0, sizeof(put_file_object_callback_data));
       // Open the file and obtain the file length.
       content_length = open_file_and_get_length(file_name, &data);
       // Set the callback function.
       obs_put_object_handler putobjectHandler =
       {
           { &response_properties_callback, &put_file_complete_callback },
           &put_file_data_callback
       };
       put_object(&options, key, content_length, &put_properties, 0, &putobjectHandler, &data);
       if (OBS_STATUS_OK == data.ret_status) {
           printf("put object from file successfully. \n");
       }
       else
       {
           printf("put object failed(%s).\n",
               obs_get_status_name(data.ret_status));
       }
       if (data.infile != NULL) {
           fclose(data.infile);
       }
       // Release the allocated global resources.
       obs_deinitialize();
   }
   // The response callback function. The content of properties in the callback can be recorded in callback_data (custom callback data).
   obs_status response_properties_callback(const obs_response_properties *properties, void *callback_data)
   {
       if (properties == NULL)
       {
           printf("error! obs_response_properties is null!");
           if (callback_data != NULL)
           {
               obs_sever_callback_data *data = (obs_sever_callback_data *)callback_data;
               printf("server_callback buf is %s, len is %llu",
                   data->buffer, data->buffer_len);
               return OBS_STATUS_OK;
           }
           else {
               printf("error! obs_sever_callback_data is null!");
               return OBS_STATUS_OK;
           }
       }
       // Print the response.
   #define print_nonnull(name, field)                                 \
       do {                                                           \
           if (properties-> field) {                                  \
               printf("%s: %s\n", name, properties->field);          \
           }                                                          \
       } while (0)
       print_nonnull("request_id", request_id);
       print_nonnull("request_id2", request_id2);
       print_nonnull("content_type", content_type);
       if (properties->content_length) {
           printf("content_length: %llu\n", properties->content_length);
       }
       print_nonnull("server", server);
       print_nonnull("ETag", etag);
       print_nonnull("expiration", expiration);
       print_nonnull("website_redirect_location", website_redirect_location);
       print_nonnull("version_id", version_id);
       print_nonnull("allow_origin", allow_origin);
       print_nonnull("allow_headers", allow_headers);
       print_nonnull("max_age", max_age);
       print_nonnull("allow_methods", allow_methods);
       print_nonnull("expose_headers", expose_headers);
       print_nonnull("storage_class", storage_class);
       print_nonnull("server_side_encryption", server_side_encryption);
       print_nonnull("kms_key_id", kms_key_id);
       print_nonnull("customer_algorithm", customer_algorithm);
       print_nonnull("customer_key_md5", customer_key_md5);
       print_nonnull("bucket_location", bucket_location);
       print_nonnull("obs_version", obs_version);
       print_nonnull("restore", restore);
       print_nonnull("obs_object_type", obs_object_type);
       print_nonnull("obs_next_append_position", obs_next_append_position);
       print_nonnull("obs_head_epid", obs_head_epid);
       print_nonnull("reserved_indicator", reserved_indicator);
       int i;
       for (i = 0; i < properties->meta_data_count; i++) {
           printf("x-obs-meta-%s: %s\n", properties->meta_data[i].name,
               properties->meta_data[i].value);
       }
       return OBS_STATUS_OK;
   }
   int put_file_data_callback(int buffer_size, char *buffer,
       void *callback_data)
   {
       put_file_object_callback_data *data =
           (put_file_object_callback_data *)callback_data;
       int ret = 0;
       if (data->content_length) {
           int toRead = ((data->content_length > (unsigned)buffer_size) ?
               (unsigned)buffer_size : data->content_length);
           ret = fread(buffer, 1, toRead, data->infile);
       }
       uint64_t originalContentLength = data->content_length;
       data->content_length -= ret;
       if (data->content_length) {
           printf("%llu bytes remaining ", (unsigned long long)data->content_length);
           printf("(%d%% complete) ...\n",
               (int)(((originalContentLength - data->content_length) * 100) / originalContentLength));
       }
       return ret;
   }
   void put_file_complete_callback(obs_status status,
       const obs_error_details *error,
       void *callback_data)
   {
       put_file_object_callback_data *data = (put_file_object_callback_data *)callback_data;
       data->ret_status = status;
   }
   uint64_t open_file_and_get_length(char *localfile, put_file_object_callback_data *data)
   {
       uint64_t content_length = 0;
       const char *body = 0;
       if (!content_length)
       {
           struct stat statbuf;
           if (stat(localfile, &statbuf) == -1)
           {
               fprintf(stderr, "\nERROR: Failed to stat file %s: ",
                   localfile);
               return 0;
           }
           content_length = statbuf.st_size;
       }
       if (!(data->infile = fopen(localfile, "rb")))
       {
           fprintf(stderr, "\nERROR: Failed to open input file %s: ",
               localfile);
           return 0;
       }
       data->content_length = content_length;
       return content_length;
   }
