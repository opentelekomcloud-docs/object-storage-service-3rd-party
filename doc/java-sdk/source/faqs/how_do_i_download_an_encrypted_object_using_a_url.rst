:original_name: obs_21_2118.html

.. _obs_21_2118:

How Do I Download an Encrypted Object Using a URL?
==================================================

If the object is encrypted with SSE-KMS, the server automatically decrypts the object when you use the URL of the object to download it.

If the object is encrypted with SSE-C, you cannot access the object directly through a web browser because a request header is required for decryption. If you use code to download the encrypted object, configure the header by referring to :ref:`Code Example: Downloading an Object Encrypted Using SSE-C <obs_21_0901__section195111828105617>`.

.. note::

   Accessing a server-side encrypted object requires the HTTPS protocol.
