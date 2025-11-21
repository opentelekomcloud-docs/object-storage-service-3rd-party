:original_name: obs_20_0106.html

.. _obs_20_0106:

Creating a Bucket
=================

A bucket is a global namespace of OBS and is a data container. It functions as a root directory of a file system and can store objects.

Sample code:

.. code-block::

   static void test_create_bucket(obs_canned_acl canned_acl, char *bucket_name)
   {
       obs_status ret_status = OBS_STATUS_BUTT;
       // Create and initialize option.
       obs_options option;
       init_obs_options(&option);
       option.bucket_options.host_name = "<your-endpoint>";
       option.bucket_options.bucket_name = "<Your bucketname>";
   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY.
       // Obtain an AK/SK pair on the management console.
       option.bucket_options.access_key = getenv("ACCESS_KEY_ID");
       option.bucket_options.secret_access_key = getenv("SECRET_ACCESS_KEY");


       // Set the response callback function.
       obs_response_handler response_handler =
       {
           0, &response_complete_callback
       };

       // Create a bucket. For details about pre-defined ACLs, see the section "Configuring a Bucket ACL (SDK for C)".
       create_bucket(&option, "<bucket ACL>", NULL, &response_handler, &ret_status);
       if (ret_status == OBS_STATUS_OK) {
           printf("create bucket successfully. \n");
       }
       else
       {
           printf("create bucket failed(%s).\n", obs_get_status_name(ret_status));
       }
   }

.. note::

   Bucket names are globally unique. Ensure that the bucket you create is named differently from any other bucket. A bucket name must comply with the following rules:

   -  Contains 3 to 63 characters, starts with a digit or letter, and supports only lowercase letters, digits, hyphens (-), and periods (.)
   -  Cannot be an IP address.
   -  Cannot start or end with a hyphen (-) or period (.).
   -  Cannot contain two consecutive periods (..), for example, **my..bucket**.
   -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.
   -  If you create buckets of the same name, no error will be reported and the bucket properties comply with those set in the first creation request.

   The example here sets the bucket's ACL to private read and write, storage class to Standard, and location to the default region for the global domain name.

   For more information, see :ref:`Creating a Bucket <obs_20_0301>`.
