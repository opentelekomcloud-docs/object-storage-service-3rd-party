:original_name: obs_21_1401.html

.. _obs_21_1401:

Overview
========

Cross-origin access refers to access between different domains. Restricting cross-origin access is a browser policy for security purposes, that is, the same-origin policy.

Due to this same-origin policy, JavaScript in origin A cannot operate objects in origin B or C.

The same-origin policy requires the protocols, domain names (or IP addresses), and ports are all the same. If the protocols, domain names, and ports (if specified) of the two web pages are the same, the two web pages are in the same origin.

Cross-origin resource sharing (CORS) allows web application programs in one origin to access resources in another.

OBS supports CORS rules that allow the resources in OBS to be requested by other domains.

For more information about the application scenarios of CORS, see:

-  :ref:`Configuring a CORS Rule <obs_21_1402>`
-  :ref:`Obtaining a CORS Rule <obs_21_1403>`
-  :ref:`Deleting a CORS Rule <obs_21_1404>`
