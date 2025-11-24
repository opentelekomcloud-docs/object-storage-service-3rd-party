:original_name: obs_29_0108.html

.. _obs_29_0108:

Creating a Bucket
=================

A bucket is a global namespace of OBS and is a data container. It functions as a root directory of a file system and can store objects. The following code shows how to create a bucket:

.. note::

   -  Bucket names are globally unique. Ensure that the bucket you create is named differently from any other bucket.
   -  A bucket name must comply with the following rules:

      -  Contains 3 to 63 characters, chosen from lowercase letters, digits, hyphens (-), and periods (.), and starts with a digit or letter.
      -  Cannot be an IP address.
      -  Cannot start or end with a hyphen (-) or period (.).
      -  Cannot contain two consecutive periods (..), for example, **my..bucket**.
      -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.

   -  If you create buckets of the same name, no error will be reported and the bucket properties comply with those set in the first creation request.

   -  For more information, see :ref:`Creating a Bucket <obs_29_0301>`.
