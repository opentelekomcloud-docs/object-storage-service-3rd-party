:original_name: obs_29_1606.html

.. _obs_29_1606:

Unmatched Signatures
====================

**Problem**: The HTTP status code obtained from **CommonMsg.Status** was **403**, and the OBS server-side error code obtained from **CommonMsg.Code** was **SignatureDoesNotMatch**.

**Solution:**

#. Check whether a bucket name was added before the endpoint. This will lead to a signature mismatch.

#. Ensure that the AK and SK matched, were both correctly specified, and were the same as those used in the request.

#. Check StringToSign.

   The structure of StringToSign should be as follows:

   .. code-block::

      HTTP-Verb + "\n" + Content-MD5 + "\n" + Content-Type + "\n" + Date + "\n" + CanonicalizedHeaders + CanonicalizedResource
