:original_name: obs_22_1607.html

.. _obs_22_1607:

How Do I Make an Object Accessible to Anonymous Users? (SDK for Python)
=======================================================================

To do this, perform the following steps:

#. Set the object access permission to **public-read** by referring to :ref:`Configuring an Object ACL (SDK for Python) <obs_22_0922>`.
#. Obtain the URL of the object by referring to :ref:`How Do I Obtain an Object URL? (Python SDK) <obs_22_1613>` and provide it to anonymous users.
#. An anonymous user can access the object by entering the URL on a browser.
