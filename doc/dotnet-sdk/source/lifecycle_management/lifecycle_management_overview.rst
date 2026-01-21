:original_name: obs_25_0901.html

.. _obs_25_0901:

Lifecycle Management Overview
=============================

OBS allows you to set lifecycle rules for buckets to automatically transition the storage class of an object and delete expired objects, to effectively use storage features and optimize the storage space. You can set multiple lifecycle rules to match different object name prefixes. A lifecycle rule must contain:

-  Rule ID, which uniquely identifies the rule
-  A shared prefix of object names that are under the control of this rule
-  Transition policy of an object of the latest version, which can be specified in either mode:

   #. How many days after the object is created
   #. Transition date

-  Expiration time of the latest version of an object, which can be specified in either of the following method:

   #. How many days after the object is created
   #. Expiration date

-  Transition policy of a noncurrent object version, which can be specified in the following mode:

   -  How many days after the object becomes a noncurrent object version

-  Expiration time of a noncurrent object version, which can be specified in the following mode:

   -  How many days after the object becomes a noncurrent object version

-  Identifier specifying whether the setting is effective

.. note::

   -  An object will be automatically deleted by the OBS server once it expires.
   -  The time set in the transition policy of an object must be earlier than its expiration time, and the time set in the transition policy of a noncurrent object version must be earlier than its expiration time.
   -  The configured expiration time and transition policy for a noncurrent object version will take effect only when the versioning is enabled or suspended for a bucket.
