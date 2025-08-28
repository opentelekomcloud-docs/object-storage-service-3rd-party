:original_name: obs_21_0301.html

.. _obs_21_0301:

Methods
=======

If problems occur when using the OBS Java SDK, you can perform the following steps to analyze and locate the problems.

#. Make sure that of OBS Java SDK is used.

#. Make sure that the logging function of OBS Java SDK is enabled. For details about how to enable the function, see the :ref:`Log Analysis <obs_21_2004>` section. The recommended log level is WARN.

#. Make sure that the program code of the OBS Java SDK complies with :ref:`Using an OBS Client <obs_21_0100__section8686104202916>`. All call exceptions of ObsClient APIs are processed as required. The following is a code example of uploading an object:

   ::

      ObsClient obsClient = null;
      try
      {
          String endPoint = "https://your-endpoint";
          // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY_ID.
          // Obtain an AK/SK pair on the management console.
          String ak = System.getenv("ACCESS_KEY_ID");
          String sk = System.getenv("SECRET_ACCESS_KEY_ID");

          obsClient = new ObsClient(ak, sk, endPoint);
          HeaderResponse response = obsClient.putObject("bucketname", "objectname", new ByteArrayInputStream("Hello OBS".getBytes()));
          // (Optional) If a call is successful, record the HTTP status code and request ID returned by the server.
          System.out.println(response.getStatusCode());
          System.out.println(response.getRequestId());
      }
      catch (ObsException e)
      {
          // Recommended: When an exception occurs, record the HTTP status code, server-side error code, and request ID returned by the server.
          System.out.println("HTTP Code: " + e.getResponseCode());
          System.out.println("Error Code:" + e.getErrorCode());
          System.out.println("Request ID:" + e.getErrorRequestId());
          // Recommended: When an exception occurs, record the stack information.
          e.printStackTrace(System.out);
      }

   .. note::

      You can click :ref:`here <obs_21_2005>` to view the details about **ObsException**.

#. If an exception occurs when an ObsClient API is called, obtain the :ref:`HTTP status code <obs_21_2001>` and :ref:`OBS server-side error code <obs_21_2002>` from **ObsException** or log file, and compare them to locate the exception cause.

#. If the exception cause cannot be found in step 4, obtain the request ID returned by the OBS server from **ObsException** or log file and contact the OBS server O&M team to locate the cause.

#. If the request ID is unable to be obtained, collect the stack information of **ObsException** and contact the OBS client O&M team to locate the cause.
