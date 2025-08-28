:original_name: obs_21_2111.html

.. _obs_21_2111:

How Do I Obtain an Object URL?
==============================

If the uploaded object is set to be read by anonymous users, anonymous users can download the object through the object URL directly. Methods to obtain the object URL are as follows:

Method 1: Query by calling the API. After an object is uploaded using the ObsClient API, **PutObjectResult** is returned. You can call **getObjectUrl** to obtain the URL of the uploaded object. The sample code is as follows:

::

   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY_ID.
   // Obtain an AK/SK pair on the management console.
   String ak = System.getenv("ACCESS_KEY_ID");
   String sk = System.getenv("SECRET_ACCESS_KEY_ID");
   // Create an ObsClient instance.
   ObsClient obsClient = new ObsClient(ak, sk, endPoint);
   // Call putObject to upload the object and obtain the return result.
   PutObjectResult result = obsClient.putObject("bucketname", "objectname", new File("localfile"));
   // Read the URL of the uploaded object.
   System.out.println("\t" + result.getObjectUrl());

Method 2: Assemble the URL in the format of **https://**\ *Bucket name*\ **.**\ *Domain name*\ **/**\ *Directory level*\ **/**\ *Object name*.

.. note::

   -  If the object resides in the root directory of a bucket, its URL does not contain a directory level.
