:original_name: obs_23_0001.html

.. _obs_23_0001:

Downloading and Installing an SDK
=================================

This topic provides the download links and installation methods of OBS SDK for Go.

.. _obs_23_0001__section7323173822517:

Downloading OBS SDK for Go
--------------------------

-  `Latest version of OBS SDK for Go <https://github.com/opentelekomcloud-community/obs-go-sdk>`__

Downloading a Go SDK and Using GoLand to Compile It
---------------------------------------------------

This procedure uses the latest version as an example:

#. Download :ref:`the SDK package <obs_23_0001__section7323173822517>`.
#. Decompress the package to obtain the following files: **src** (the SDK source code and sample code) and **README.MD** (the feature description file of SDK versions).
#. Use GoLand to create a Go project and copy the **obs**, **examples**, and **main** folders to the **src** folder of your Go project.
#. Right-click the Go project and choose **Build Project** from the drop-down list, and wait until the building is complete.

   .. note::

      After the building is complete, you can get a directory structure similar to the following:

      ├── bin

      ├── pkg

      ├── src

      -----├── examples

      -----├── main

      -----└── obs

      └── README.MD
