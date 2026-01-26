:original_name: obs_25_0105.html

.. _obs_25_0105:

Installing the SDK
==================

Installing the OBS .NET SDK. The example here uses the latest version.

#. Download the OBS .NET SDK development package. For details, see :ref:`SDK Download Links <obs_25_0001>`.
#. Decompress the development package to obtain folder **demo** (sample code) and file **Log4Net.config** (log configuration file). Start Visual Studio, open the project solution, and open the **esdk_obs_.net.sln** or **esdk_obs_.net_core.sln** file in the directory based on the project framework. Set the solution to **Release** and generate a solution. You can find **esdk_obs_.net.dll** and **log4net.dll** files in **bin/Release** in the decompression directory.
#. Start Visual Studio and choose **FILE** > **New** > **Project** > **Templates** > **Visual C#** > **Console Application** to create a Console Application project.
#. Right-click the new project and choose **References** > **Add Reference** and import file **esdk_obs_.net.dll**.
