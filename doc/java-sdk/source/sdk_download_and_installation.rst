:original_name: obs_21_0001.html

.. _obs_21_0001:

SDK Download and Installation
=============================

.. _obs_21_0001__section10285185142912:

Downloading OBS SDK for Java
----------------------------

-  Latest version of OBS Java SDK: `Download <https://github.com/opentelekomcloud-community/obs-java-sdk>`__

Compiling the Java Source Code
------------------------------

You can download the source code of SDK for Java and compile the source code to create a JAR package. Before using this method, ensure that the Java and Maven environments are correctly configured and can be used properly.

#. Download the source code by referring to :ref:`Downloading OBS SDK for Java <obs_21_0001__section10285185142912>` and decompress it.

#. Go to the directory where the source code is decompressed using commands.

#. Run the following command:

   Linux:

   .. code-block::

      mvn clean package -Dmaven.test.skip=true -f pom-java.xml

   Windows:

   .. code-block::

      mvn clean package "-Dmaven.test.skip=true" -f pom-java.xml

#. Find the generated JAR package in the **target** subdirectory of the decompressed directory.

#. Save the JAR package to the dependency path of the local project.
