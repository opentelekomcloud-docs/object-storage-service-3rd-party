:original_name: obs_25_0103.html

.. _obs_25_0103:

Creating an AK and SK
=====================

Access keys consist of two parts: an access key ID (AK) and a secret access key (SK). OBS uses access keys to sign requests to make sure that only authorized accounts can access specified OBS resources. Detailed explanations about AK and SK are as follows:

-  An AK defines a user who accesses the OBS system. An AK belongs to only one user, but one user can have multiple AKs. The OBS system recognizes the users who access the system by their access key IDs.
-  An SK is the key used by users to access OBS. It is the authentication information generated based on the AK and the request header. An SK matches an AK, and they group into a pair.

The procedure is as follows:

#. Log in to OBS Console.
#. In the upper right corner of the page, hover the cursor over the username and choose **My Credentials**.
#. On the **My Credentials** page, select **Access Keys** in the navigation pane on the left.
#. On the **Access Keys** page, click **Create Access Key**.
#. In the **Create Access Key** dialog box that is displayed, enter the password and verification code.

   .. note::

      -  If you have not bound an email address or mobile number, you need to enter only the login password.
      -  If you have bound an email address and a mobile number, you can select the verification by either email or mobile phone.

#. Click **OK**.
#. In the **Download Access Key** dialog box that is displayed, click **OK** to save the access keys to your browser's default download path.
#. Open the downloaded **credentials.csv** file to obtain the access keys (AK and SK).

.. note::

   -  A user can create a maximum of two valid access keys.
   -  Keep the access key properly. If you click **Cancel** in the dialog box, the access keys will not be downloaded, and cannot be obtained later. You can re-create access keys if you need to use them.

-  To get temporary access keys, refer to the following:

   Temporary access keys are issued by the system and are only valid for 15 minutes to 24 hours. Once expired, they must be requested again. They follow the principle of least privilege. When a temporary AK/SK pair is used for authentication, a security token must be used at the same time.
