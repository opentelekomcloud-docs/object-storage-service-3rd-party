:original_name: obs_21_2003.html

.. _obs_21_2003:

SDK Common Response Headers
===========================

After you successfully call an API in an instance of ObsClient, an instance of the HeaderResponse class (or of its sub-class) will be returned.

It contains information about HTTP/HTTPS response headers.

Sample code for processing public response headers:

::

   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY_ID.
   // Obtain an AK/SK pair on the management console.
   String ak = System.getenv("ACCESS_KEY_ID");
   String sk = System.getenv("SECRET_ACCESS_KEY_ID");
   // Create an ObsClient instance.
   ObsClient obsClient = new ObsClient(ak, sk, endPoint);
   HeaderResponse response = obsClient.createBucket("bucketname");

   // Obtain the request ID from the common response headers.
   System.out.println("\t" + response.getRequestId());

   obsClient.close();
