:original_name: obs_20_0103.html

.. _obs_20_0103:

Creating Access Keys
====================

OBS uses the AK and SK in a user account for signature verification to make sure that only authorized accounts can access specified OBS resources. Detailed explanations about AK and SK are as follows:

-  An access key ID (AK) defines a user who accesses the OBS system. An AK belongs to only one user, but one user can have multiple AKs. The OBS system recognizes the users who access the system by their access key IDs.
-  A secret access key (SK) is the key used by users to access OBS. It is the authentication information generated based on the AK and the request header. An SK matches an AK, and they group into a pair.

Access keys are classified into :ref:`permanent access keys (AK/SK) <obs_20_0103__en-us_topic_0142815543_en-us_topic_0142814371_section563920502595>` and :ref:`temporary access keys (AK/SK and security token) <obs_20_0103__en-us_topic_0142815543_en-us_topic_0142814371_section111622513117>`. Each user can create at most two permanent access keys. Temporary access keys must be used within a given validity period. Once expired, they must be requested again. For security purposes, you are advised to use temporary access keys to access OBS. If you want to use permanent access keys, periodically update them. The following describes how to obtain two types of access keys.

.. _obs_20_0103__en-us_topic_0142815543_en-us_topic_0142814371_section563920502595:

Permanent Access Keys
---------------------

#. Log in to OBS Console.
#. In the upper right corner of the page, hover the cursor over the username and choose **My Credentials**.
#. On the **My Credentials** page, select **Access Keys** in the navigation pane on the left.
#. On the **Access Keys** page, click **Create Access Key**.
#. In the **Create Access Key** dialog box that is displayed, enter the password and verification code.

   .. note::

      -  If you have not bound an email address or mobile number, enter only the password.
      -  If you have bound an email address and a mobile number, you can select the verification by either email or mobile phone.

#. Click **OK**.
#. In the **Download Access Key** dialog box that is displayed, click **OK** to save the access keys to your browser's default download path.
#. Open the downloaded **credentials.csv** file to obtain the access keys (AK and SK).

   .. note::

      -  A user can create a maximum of two valid access keys.
      -  Keep the access key properly. If you click **Cancel** in the dialog box, the access keys will not be downloaded, and cannot be obtained later. You can re-create access keys if you need to use them.

.. _obs_20_0103__en-us_topic_0142815543_en-us_topic_0142814371_section111622513117:

Temporary Access Keys
---------------------

Temporary access keys are issued by the system and are only valid for 15 minutes to 24 hours. Once expired, they must be requested again. They follow the principle of least privilege. When a temporary AK/SK pair is used for authentication, a security token must be used at the same time.

For details about how to obtain temporary access keys, see `Obtaining a Temporary AK/SK <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0097949518.html>`__.

For details about how to use temporary access keys, see :ref:`Initializing option <obs_20_0105>`.
