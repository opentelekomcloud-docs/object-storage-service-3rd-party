:original_name: obs_21_2121.html

.. _obs_21_2121:

Does the SDK Support Uploading, Downloading, or Copying Objects in a Batch?
===========================================================================

No.

Currently, the SDK does not provide such APIs. You need to encapsulate the service codes for uploading, downloading, or copying objects in a batch by yourself. The procedure is as follows:

#. List all objects to be uploaded, downloaded, or copied. For details about how to list objects to be downloaded, see :ref:`Listing Objects <obs_21_0803>`.
#. Call the API for uploading, downloading, or copying a single object for the listed objects.

Sample code:

::

   // Hard-coded or plaintext AK/SK are risky. For security purposes, encrypt your AK/SK and store them in the configuration file or environment variables. In this example, the AK/SK are stored in environment variables for identity authentication. Before running this example, configure environment variables ACCESS_KEY_ID and SECRET_ACCESS_KEY_ID.
   // Obtain an AK/SK pair on the management console.
   String ak = System.getenv("ACCESS_KEY_ID");
   String sk = System.getenv("SECRET_ACCESS_KEY_ID");
   final String bucketName = "bucketname";
   // Define the prefix of objects in a bucket.
   final String objectPre = "object/";
   // Folder to be uploaded
   final String localDirPath = "localDirPath";
   final List<File> list = new ArrayList<>();
   // Scan all objects in the folder.
   static void listFiles(File file){
       File[] fs = file.listFiles();
       assert fs != null;
       if (fs.length < 1){
           // If an empty folder needs to be uploaded, add it to the list.
           list.add(file);
       }else{
           for (File f:fs){
               if (f.isDirectory()){
                   listFiles(f);
               }
               if (f.isFile()){
                   // Add objects to be uploaded to the list.
                   list.add(f);
               }
           }
       }
   }
   // Traverse the folder to be uploaded and obtain all objects to be uploaded.
   File file = new File(localDirPath);
   listFiles(file);

   // Create an instance of ObsClient.
   final ObsClient obsClient = new ObsClient(ak, sk, endPoint);

   // Initialize the thread pool.
   ExecutorService executorService = Executors.newFixedThreadPool(20);

   // Concurrently upload parts.
   for (File f:list){
       executorService.execute(() -> {
           if (f.isDirectory()){
               // For empty folders, create empty folder objects in the bucket.
               String remoteObjectKey = objectPre + f.getPath().substring(localDirPath.length() + 1) + "/";
               obsClient.putObject(bucketName, remoteObjectKey, new ByteArrayInputStream(new byte[0]));
           }else{
               String remoteObjectKey = objectPre + f.getPath().substring(localDirPath.length() + 1);
               obsClient.putObject(bucketName, remoteObjectKey, new File(f.getPath()));
           }
       });
   }

   // Wait until the upload is complete.
   executorService.shutdown();
   while (!executorService.isTerminated())
   {
       try
       {
           executorService.awaitTermination(5, TimeUnit.SECONDS);
       }
       catch (InterruptedException e)
       {
           e.printStackTrace();
       }
   }
   // Close ObsClient.
   try {
       obsClient.close();
   } catch (IOException e) {
       e.printStackTrace();
   }

.. note::

   You can use multiple threads to concurrently upload, download, and copy data to improve efficiency.
