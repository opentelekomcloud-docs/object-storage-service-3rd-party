:original_name: obs_29_0103.html

.. _obs_29_0103:

Creating Access Keys
====================

OBS uses access keys (AK and SK) for signature verification to ensure that only authorized accounts can access specified OBS resources. Detailed explanations are as follows:

-  An AK is an Access Key ID on OBS. One AK maps to only one user but one user can have multiple AKs. OBS recognizes users by their AKs.
-  An SK is the Secret Access Key on OBS, which is required as the key to access OBS. You can generate authentication information based on SKs and request header fields. SKs and AKs are in one-to-one mapping.

The procedure is as follows:

#. Log in to OBS Console.
#. In the upper right corner, hover the cursor over the username and choose **My Credentials**.
#. On the **My Credentials** page, select **Access Keys** in the navigation pane on the left.
#. On the **Access Keys** page, click **Create Access Key**.
#. In the **Add Access Key** dialog box that is displayed, enter the password and its verification code.

   .. note::

      -  If you have not bound an email address or mobile number, you need to enter only the password.
      -  If you have bound an email address and a mobile number, you can select the verification either by email address or mobile number.

#. Click **OK**.
#. In the **Download Access Key** dialog box that is displayed, click **OK** to save the access keys to your browser's default download path.
#. Open the downloaded **credentials.csv** file to obtain the access keys (AK and SK).

.. note::

   -  Each user can create up to two valid AK/SK pairs.
   -  To prevent the AK from being leaked, keep it secure. If you click **Cancel** in the dialog box, the AKs will not be downloaded, and you cannot download them later. You can re-create an access key if you need to use it.

-  To get temporary access keys, refer to the following:

   Temporary access keys are issued by the system and are only valid for 15 minutes to 24 hours. Once expired, they must be requested again. They follow the principle of least privilege. When a temporary AK/SK pair is used for authentication, a security token must be used at the same time.
