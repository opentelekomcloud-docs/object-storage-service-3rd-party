:original_name: obs_20_0202.html

.. _obs_20_0202:

Initializing the SDK
====================

**ObsClient** functions as the C client for accessing OBS. It offers callers a series of APIs for interaction with OBS. These APIs are used for managing and operating resources, such as buckets and objects, stored in OBS.

Before using the OBS C SDK to initiate an OBS request, you need to call the initialization API. When you are exiting the process, you need to call the initialization cancellation API to release resources.

Before using the C SDK, you must first call **obs_initialize** to complete the initialization. This API only needs to called once in a process.

.. code-block::

   obs_status  ret_status = OBS_STATUS_BUTT;
   ret_status = obs_initialize(OBS_INIT_ALL);
   if (OBS_STATUS_OK != ret_status)
   {
       printf("obs_initialize failed(%s).\n", obs_get_status_name(ret_status));
       return ret_status;
   }
   obs_deinitialize();
   // Do not repeatedly call obs_initialize or obs_deinitialize, because these operations may lead to invalid memory access.
