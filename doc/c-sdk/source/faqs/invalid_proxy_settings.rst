:original_name: obs_20_1804.html

.. _obs_20_1804:

Invalid Proxy Settings
======================

-  When the proxy is configured in a Windows SDK demo, the program reports the following error and the proxy configuration fails.

   |image1|

   **Root cause:** Due to asynchronous updates, the demo header file **eSDKOBS.h** of certain SDK versions diverges from the SDK **eSDKOBS.h**, rendering the proxy settings in the option invalid.

   **Solution:**

   #. Replace *yourSDKpath*\ **\\source\\eSDK_OBS_API\\eSDK_OBS_API_C++\\inc\\eSDKOBS.h** with *yourSDKpath*\ **\\source\\eSDK_OBS_API\\eSDK_OBS_API_C++\\build\\obs\\demo\\eSDKOBS.h**.

   #. Modify the demo as instructed here to adapt to the changes of **eSDKOBS.h**. (The adaptation of version 3.22.7 is used as an example. The adaptation process of other versions may differ.)

      In the *yourSDKpath*\ **\\source\\eSDK_OBS_API\\eSDK_OBS_API_C++\\build\\obs\\demo\\ demo_windows.cpp** file, in line 4749, add **obs_upload_file_server_callback server_callback**; in line 4750, add **, server_callback** after the fourth parameter in the **upload_file** function. See the following figure.

      |image2|

-  The proxy is configured but the connection still fails.

   **Root cause**: The proxy might not be configured in the **get_api_version** function of the SDK **request.c**.

   **Solution**:

   Configure the proxy (add the **CURLOPT_PROXY** and **CURLOPT_PROXYUSERPWD** items for curl) in the **get_api_version** function by referring to the method for configuring the proxy in the **setup_curl** function of the SDK **request.c**.

.. |image1| image:: /_static/images/en-us_image_0000002092274033.png
.. |image2| image:: /_static/images/en-us_image_0000002056116746.png
