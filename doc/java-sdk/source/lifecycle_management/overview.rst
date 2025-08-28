:original_name: obs_21_1101.html

.. _obs_21_1101:

Overview
========

OBS allows you to set lifecycle rules for buckets to automatically transition the storage class of an object or delete expired objects, to effectively use storage features and optimize the storage space. You can set multiple lifecycle rules based on the prefix. A lifecycle rule must contain:

-  Rule ID, which uniquely identifies the rule
-  Prefix of objects that are under the control of this rule
-  Transition policy of an object of the latest version, which can be specified in either mode:

   #. How many days after the object is created
   #. Transition date

-  Expiration time of an object of the latest version, which can be specified in either mode:

   #. How many days after the object is created
   #. Expiration date

-  Transition policy of a noncurrent object version, which can be specified in the following mode:

   -  How many days after an object version becomes a noncurrent one

-  Expiration time of a noncurrent object version, which can be specified in the following mode:

   -  How many days after the object becomes a noncurrent object version

-  Identifier specifying whether the setting is effective
