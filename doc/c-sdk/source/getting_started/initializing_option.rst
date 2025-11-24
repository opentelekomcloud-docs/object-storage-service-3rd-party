:original_name: obs_20_0105.html

.. _obs_20_0105:

Initializing **option**
=======================

When the function of SDK for C is called, the **option** parameter must be passed. You can use function **init_obs_options** to initialize the **option** configuration, including the AK, SK, endpoint, bucket, timeout, and temporary authentication.

-  Sample code for creating and initializing **option** using permanent access keys (AK/SK):

   .. code-block::

      // Create and initialize option.
      obs_options option;
      init_obs_options(&option);
      option.bucket_options.host_name = "<your-endpoint>";
      option.bucket_options.bucket_name = "<Your bucketname>";

      // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY.
      // Obtain an AK/SK pair on the management console.
      option.bucket_options.access_key = getenv("ACCESS_KEY_ID");
      option.bucket_options.secret_access_key = getenv("SECRET_ACCESS_KEY");

-  Sample code for creating and initializing **option** using temporary access keys (AK/SK and SecurityToken):

   .. code-block::

      // Create and initialize option.
      obs_options option;
      init_obs_options(&option);
      option.bucket_options.host_name = "<your-endpoint>";
      option.bucket_options.bucket_name = "<Your bucketname>";

      // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY.
      // Obtain an AK/SK pair on the management console.
      option.bucket_options.access_key = getenv("ACCESS_KEY_ID");
      option.bucket_options.secret_access_key = getenv("SECRET_ACCESS_KEY");
      option.bucket_options.token = getenv("SecurityToken");

   .. note::

      -  OBS is a global service. When obtaining temporary credentials, set the token scope to **domain** to make the token applicable to all projects and regions within an account.
