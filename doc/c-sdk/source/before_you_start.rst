:original_name: obs_20_0101.html

.. _obs_20_0101:

Before You Start
================

This section describes the version compatibility and important notes about the C SDK of Object Storage Service (OBS).

Compatibility
-------------

-  **3.*.\*** is compatible with **3.0.0**.

-  **3.*.\*** is incompatible with **2.*.\***.

-  **3.*.\*** is incompatible with **1.*.\***.

-  Arm compilation environment:

   .. code-block::

      NAME="EulerOS"
      VERSION="2.0 (SP8)"
      ID="euleros"
      ID_LIKE="rhel fedora centos"
      VERSION_ID="2.0"
      PRETTY_NAME="EulerOS 2.0 (SP8)"
      ANSI_COLOR="0;31"

   Kernel version:

   .. code-block::

      4.19.36-vhulk1905.1.0.h276.eulerosv2r8.aarch64

   gcc/g++ version:

   .. code-block::

      gcc (GCC) 10.3.0/g++ (GCC) 10.3.0

-  Linux compilation environment:

   .. code-block::

      NAME="CentOS Linux"
      VERSION="7 (Core)"
      ID="centos"
      ID_LIKE="rhel fedora"
      VERSION_ID="7"
      PRETTY_NAME="CentOS Linux 7 (Core)"
      ANSI_COLOR="0;31"
      CPE_NAME="cpe:/o:centos:centos:7"
      HOME_URL="https://www.centos.org/"
      BUG_REPORT_URL="https://bugs.centos.org/"

      CENTOS_MANTISBT_PROJECT="CentOS-7"
      CENTOS_MANTISBT_PROJECT_VERSION="7"
      REDHAT_SUPPORT_PRODUCT="centos"
      REDHAT_SUPPORT_PRODUCT_VERSION="7"

   Kernel version:

   .. code-block::

      3.10.0-957.5.1.el7.x86_64

   gcc/g++ version:

   .. code-block::

      gcc (GCC) 10.3.0/g++ (GCC) 10.3.0

   .. note::

      The required environments for compiling the SDK binary package are listed above. Compatibility is not guaranteed for other kernels and operating systems. If you need to use other operating systems or kernel versions, use the open-source code to compile on your own.

Important Notes
---------------

-  Ensure that you are familiar with OBS basic concepts mentioned in the `Help Center <https://docs.otc.t-systems.com/en-us/usermanual/obs/en-us_topic_0045853692.html>`__, such as bucket, object, region, and AK and SK.
-  After an API call is complete using an instance of ObsClient, view whether an exception is thrown. If no, the API call was successful. If yes, the operation failed. You can check the error information from :ref:`SDK Error Handling <obs_20_1602>`.
-  Some features are available only in some regions. If an API call returns the 405 HTTP status code, check whether the region supports this feature.
