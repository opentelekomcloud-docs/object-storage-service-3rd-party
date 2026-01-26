:original_name: obs_25_1001.html

.. _obs_25_1001:

CORS Overview
=============

Cross-origin access refers to access between different domains. Restricting cross-origin access is a browser policy for security purposes, that is, the same-origin policy.

Due to this same-origin policy, JavaScript in origin A cannot operate objects in origin B or C.

The same-origin policy requires the protocols, domain names (or IP addresses), and ports are all the same. If the protocols, domain names, and ports (if specified) of the two web pages are the same, the two web pages are in the same origin.

CORS allows web application programs in one origin to access resources in another. OBS provides developers with APIs for facilitating cross-origin resource access.
