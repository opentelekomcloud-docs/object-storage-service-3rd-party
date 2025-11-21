:original_name: obs_20_0901.html

.. _obs_20_0901:

Overview
========

OBS allows you to set lifecycle rules for buckets to automatically transition the storage class of an object or delete expired objects, to effectively use storage features and optimize the storage space. You can set multiple lifecycle rules based on the prefix. A lifecycle rule contains:

-  Rule ID, which uniquely identifies the rule
-  Prefix of objects that are under the control of this rule
-  Transition policy of an object of the latest version, which can be specified in either mode:

   #. How many days after the object is created
   #. Transition date

-  Expiration time of an object of the latest version, which can be specified in either mode:

   #. How many days after the object is created
   #. Expiration date

-  Transition time for a historical object version, which is specified in the following mode:

   -  How many days after an object version becomes historical

-  Expiration time of a historical object version, which can be specified in the following mode:

   -  How many days after the object becomes historical

-  Identifier specifying whether the setting is effective

.. note::

   -  An object will be automatically deleted by the OBS server once it expires.
   -  The time set in the transition policy of an object must be earlier than its expiration time, and the time set in the transition policy of a historical object version must be earlier than its expiration time.
   -  The expiration time and transition policy for a historical object version will take effect only after versioning is enabled for buckets.
