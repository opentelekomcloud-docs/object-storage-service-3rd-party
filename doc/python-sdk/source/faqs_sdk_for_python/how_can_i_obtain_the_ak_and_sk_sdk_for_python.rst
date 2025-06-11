:original_name: obs_22_1609.html

.. _obs_22_1609:

How Can I Obtain the AK and SK? (SDK for Python)
================================================

OBS employs access keys (AK and SK) for signature verification to ensure that only authorized accounts can access specified OBS resources. Detailed explanations of access keys are as follows:

-  AK is short for Access Key ID. One AK maps to only one user but one user can have multiple AKs. OBS authenticates users by their AKs.
-  SK is short for Secret Access Key, which is used to access OBS. You can generate authentication information based on SKs and request headers. An SK maps to an AK, and they group into a pair.

To create an AK and SK pair, perform the following steps:

#. Log in to the management console.
#. In the upper right corner, hover your cursor over the username and choose **My Credentials**.
#. On the **My Credentials** page, click **Access Keys** in the navigation pane.
#. On the **Access Keys** page, click **Create Access Key**.
