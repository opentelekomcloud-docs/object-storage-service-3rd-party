:original_name: obs_29_0105.html

.. _obs_29_0105:

Installing the SDK
==================

Installing the SDK with the Source Code
---------------------------------------

The following procedures use OBS Node.js SDK of the latest version as an example.

#. Download the OBS Node.js SDK by referring to :ref:`Downloading an SDK <obs_29_0001>`.
#. Decompress the development package to obtain folder **examples** (code examples), folder **lib** (SDK source code), file **package.json** (dependency configuration file), and file **README.txt** (feature description file of SDK versions).
#. On the command-line interface (CLI), go to the directory under which the SDK development package was decompressed, and run the **npm install** command to install dependency libraries. A **node_modules** folder will be generated.
#. (Optional) In the Eclipse JavaScript project, import the source code: Open Eclipse JavaScript IDE and choose **Import** > **Projects from Folder or Archive**. For **Import source**, select the directory under which the SDK development package is decompressed.

.. note::

   After the installation, the directory structure is similar to the following:

   ├── examples

   ├── lib

   ├── node_modules

   ├── package.json

   └── README.txt
