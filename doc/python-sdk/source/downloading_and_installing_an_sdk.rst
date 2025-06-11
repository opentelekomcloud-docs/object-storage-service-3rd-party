:original_name: obs_22_0400.html

.. _obs_22_0400:

Downloading and Installing an SDK
=================================

This topic provides the download links and installation methods of OBS SDK for Python.

Downloading OBS SDK for Python
------------------------------

Latest version of OBS Python SDK source code: `Download <https://github.com/opentelekomcloud-community/obs-python-sdk>`__

Installing OBS SDK for Python
-----------------------------

You can use the methods listed in :ref:`Table 1 <obs_22_0400__table6377143115452>` to install OBS SDK for Python.

.. _obs_22_0400__table6377143115452:

.. table:: **Table 1** Methods of installing OBS SDK for Python

   +-----+---------------------------------------------------------------------------------+
   | No. | Method                                                                          |
   +=====+=================================================================================+
   | 1   | :ref:`Installing Using the Source Code <obs_22_0400__section6866125102510>`     |
   +-----+---------------------------------------------------------------------------------+
   | 2   | :ref:`Installing the SDK Using setuptools <obs_22_0400__section66901737144816>` |
   +-----+---------------------------------------------------------------------------------+

.. _obs_22_0400__section6866125102510:

Method: Installing the SDK Using the Source Code
------------------------------------------------

The following procedures show an example of installing the latest version of OBS Python SDK.

#.  the SDK package and decompress it.
#. Run **pip install pycryptodome==3.10.1** to install the cryptographic library.
#. Decompress the development package to obtain folder **src** (SDK source code), folder **examples** (sample code), file **README.txt** (feature description file of SDK versions), and file **log.conf** (SDK log configuration file).
#. Use PyCharm to create a project, copy the folders and files obtained in the previous step to the project, right-click folder **src**, and choose **Mark Directory as** > **Sources Root**.

   .. note::

      After the configuration, the directory structure is similar to the following:

      ├── examples

      ├── src

      ├── log.conf

      └── README.md

.. _obs_22_0400__section66901737144816:

Method: Installing the SDK Using setuptools
-------------------------------------------

The following procedures show an example of installing the latest version of OBS Python SDK.

#.  the SDK package and decompress it.
#. Download and install `setuptools <https://pypi.python.org/pypi/setuptools/>`__.
#. On the command-line interface (CLI), go to folder **src** under the directory where the development package is decompressed.
#. Run the **python setup.py install** command to install the SDK.
#. After the installation, check whether a folder named **esdk_obs_python-<versionId>-*.egg** is generated in **Lib/site-package** under the Python installation directory.

   .. note::

      -  If you use this method to install the SDK, you need to delete folder **esdk_obs_python-**\ *<versionId>*\ **-*.egg** when you re-install the SDK.
      -  If SDK modules cannot be loaded after you have performed the previous steps, you can directly add the absolute path of the **src** directory in OBS Python SDK to the **sys.path** list.
