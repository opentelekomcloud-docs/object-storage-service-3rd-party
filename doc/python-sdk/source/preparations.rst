:original_name: obs_22_0300.html

.. _obs_22_0300:

Preparations
============

Before using OBS SDK for Python to access OBS, you need to prepare the service and development environments. To prepare the service environment, you must get an account and an access key. Both of them are necessary for interaction between OBS SDK for Python and OBS. To ensure successful SDK installation and SDK-based code development and running, you should also set up a local development environment, for example, installing dependencies and development tools.

Preparing Access Keys
---------------------

Access keys consist of two parts: an access key ID (AK) and a secret access key (SK). OBS uses access keys to sign requests to make sure that only authorized accounts can access specified OBS resources. Programmatic access must be enabled for an IAM user before the IAM user can get access keys. Access keys are explained as follows:

-  One AK maps to only one user but one user can have multiple AKs. OBS authenticates users by their AKs.
-  An SK is required for accessing OBS. Authentication information is generated based on the SK and request headers. AKs and SKs are in one-to-one match.

Access keys are classified into permanent access keys (AK/SK) and temporary access keys (AK/SK and security token). Each user can create at most two permanent access keys. Temporary access keys must be used within a given validity period. Once expired, they must be requested again. For security purposes, you are advised to use temporary access keys to access OBS. If you want to use permanent access keys, periodically update them. The following describes how to obtain two types of access keys.

-  To get permanent access keys, do as follows:

   #. Log in to the management console.
   #. In the upper right corner, hover over the username and choose **My Credentials**.
   #. On the **My Credentials** page, click **Access Keys** in the navigation pane.
   #. On the **Access Keys** page, click **Create Access Key**.
   #. In the displayed dialog box, enter the login password and verification code.

      .. note::

         -  If you have not bound an email address or a mobile number yet, only the login password is required.
         -  If you have bound both an email address and a mobile number, you can use either of them for verification.

   #. Click **OK**.
   #. Click **Download**. The access key file is automatically saved to your browser's default download path.
   #. Open the downloaded **credentials.csv** file to obtain the access keys (AK and SK).

      .. note::

         -  Each user can create a maximum of two valid access key pairs.
         -  Keep AKs and SKs properly to prevent information leakage. If you click **Cancel** in the download dialog box, the access keys will not be downloaded and cannot be downloaded later. You can create a new AK/SK pair if needed.

-  To get temporary access keys, refer to the following:

   Temporary access keys are issued by the system and are only valid for 15 minutes to 24 hours. Once expired, they must be requested again. They follow the principle of least privilege. When a temporary AK/SK pair is used for authentication, a security token must be used at the same time.

Setting Up a Development Environment
------------------------------------

-  Download a proper Python version from the `Python official website <https://www.python.org/>`__ and install it.

   -  Recommended Python 2.\ *x* version: 2.7.\ *x*
   -  Recommended Python 3.\ *x* versions: 3.6, 3.7, 3.8, 3.9, 3.10, and 3.11

   .. note::

      Python 3.5 and earlier versions are not recommended. If you need to use these versions, run the **pip install secrets** command to install the secrets module. You can install python2-secrets on Python 2.7.

-  Download the latest community version of PyCharm from the `PyCharm official website <https://www.jetbrains.com/pycharm/>`__.
-  Run **pip install pycryptodome==3.10.1** to install the cryptographic library.
