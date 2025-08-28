:original_name: obs_21_0302.html

.. _obs_21_0302:

Other Notable Issues
====================

SignatureDoesNotMatch
---------------------

::

   HTTP Code: 403
   Error Code: SignatureDoesNotMatch

Possible causes are as follows:

#. The SK input into ObsClient initialization is incorrect. Solution: Make sure that the SK is correct.
#. This problem is caused by a bug in the OBS Java SDK of an earlier version. Solution: Upgrade the SDK to the latest version.
#. OBS Java SDK 2.1.\ *x* versions are incompatible with the dependent library Apache HttpClient. Solution: Use httpcore-4.4.4 and httpclient-4.5.3.

MethodNotAllowed
----------------

::

   HTTP Code: 405
   Error Code: MethodNotAllowed

This error occurs because a feature on which the ObsClient API depends has not been rolled out on the requested OBS server. Contact the OBS O&M team for further confirmation.

BucketAlreadyOwnedByYou
-----------------------

::

   HTTP Code: 409
   Error Code: BucketAlreadyOwnedByYou

In OBS, a bucket name must be globally unique. Solution: If this error occurs when the **ObsClient.createBucket** is called, check whether the bucket exists. You can use either of the following methods to check whether a bucket exists:

Method 1 (recommended): Call **ObsClient.listBuckets** to query the list of all buckets that you own and check whether the bucket exists.

Method 2: Call **ObsClient.headBucket** to check whether the bucket exists.

.. note::

   **ObsClient.headBucket** can query only buckets in the current region, while **ObsClient.listBuckets** can query buckets in all regions.

BucketAlreadyExists
-------------------

::

   HTTP Code: 409
   Error Code: BucketAlreadyExists

In OBS, a bucket name must be globally unique. Solution: If this error occurs when **ObsClient.createBucket** is called, it indicates that the bucket has been created by another user. Use a different bucket name and try again.

.. _obs_21_0302__section58191624113616:

Connection Timeout
------------------

::

   HTTP Code: 408
   Caused by: java.net.ConnectException: Connection timed out: connect
       at java.net.DualStackPlainSocketImpl.waitForConnect(Native Method)
       at java.net.DualStackPlainSocketImpl.socketConnect(DualStackPlainSocketImpl.java:85)

Possible causes are as follows:

#. The endpoint input during ObsClient initialization is incorrect. Solution: Make sure that the endpoint is correct.
#. The network between the OBS client and OBS server is abnormal. Solution: Check the health status of the network.
#. The OBS domain name resolved by DNS is inaccessible. Solution: Contact the OBS O&M team.

.. _obs_21_0302__section885063114315:

Read/Write Timeout
------------------

::

   HTTP Code: 408
   Error Code:RequestTimeOut
   Caused by: java.net.SocketTimeoutException: timeout
       at okio.Okio$4.newTimeoutException(Okio.java:232)
       at okio.AsyncTimeout.exit(AsyncTimeout.java:285)
       at okio.AsyncTimeout$2.read(AsyncTimeout.java:241)

Possible causes are as follows:

#. The network latency between the OBS client and OBS server is too long. Solution: Check the health status of the network.
#. The network between the OBS client and OBS server is abnormal. Solution: Check the health status of the network.

Abnormal Returned Value -1
--------------------------

::

   HTTP Code: -1

Possible causes are as follows:

#. The OBS Java SDK of an earlier version is used and a connection timeout or read/write timeout occurs. Solution: See the solutions for :ref:`connection timeout <obs_21_0302__section58191624113616>` and :ref:`read/write timeout <obs_21_0302__section885063114315>`.
#. This is a bug in earlier versions of OBS Java SDK. Solution: Use .
#. The server returns an exception. Solution: Obtain the request ID returned by OBS server from the log and contact the OBS O&M team.

Unable to Obtain Error Codes from ObsException
----------------------------------------------

Possible causes are as follows:

#. An error is reported when **ObsClient.getBucketMetadata** or **ObsClient.getObjectMetadata** is called. In this scenario, the server does not return an error code because the request method used in the background is HEAD. Solution: Call **ObsException.getResponseCode** to obtain the HTTP status code to analyze the possible cause. For example, 403 indicates that the user does not have the access permission, and 404 indicates that the bucket or object does not exist. If the cause cannot be located, obtain the request ID returned by the OBS server from **ObsException** and contact the OBS O&M team.
#. The endpoint passed during ObsClient initialization cannot correspond to a valid IP address of the OBS server after DNS resolution. Solution: Check whether the endpoint is correct. If the endpoint is correct, contact the OBS O&M team.

UnknownHostException
--------------------

::

   Caused by: java.net.UnknownHostException: bucketname.unknowndomain.com
       at java.net.Inet6AddressImpl.lookupAllHostAddr(Native Method)
       at java.net.InetAddress$1.lookupAllHostAddr(InetAddress.java:901)
       at java.net.InetAddress.getAddressesFromNameService(InetAddress.java:1293)

Possible causes are as follows:

#. The endpoint input during ObsClient initialization is incorrect. Solution: Make sure that the endpoint is correct.
#. DNS cannot resolve the OBS domain name. Solution: Contact the OBS O&M team.

NullPointException
------------------

::

   Exception in thread "main" java.lang.NullPointerException
       at com.obs.services.internal.RestStorageService.isCname(RestStorageService.java:1213)
       at com.obs.services.ObsClient.doActionWithResult(ObsClient.java:2805)

Possible causes are as follows:

#. **ObsClient.close** is called to close ObsClient and then another ObsClient API is called. Solution: Call **ObsClient.close** to release resources only before exiting the application.
#. This is a bug in earlier versions of OBS Java SDK. Solution: Use .

Connection Leakage
------------------

::

   A connection to xxx was leaked. Did you forget to close a response body?

This error occurs when **ObsClient.getObject** is not properly closed after it is called to obtain the data stream of the object to be downloaded. To fix this error, call the **ObsObject.getObjectContent.close** method in the **finally** statement block to close the connection.

Problem in SDK Version Upgrade
------------------------------

The third-party dependency of the SDK of an earlier version (2.1.\ *x*) is not completely compatible with that of the new SDK (3.\ *x*). If a program startup error occurs after the earlier version is upgraded to the new version, refer to :ref:`Resolving Dependency Missing or Conflicts <obs_21_0303>` to rectify the fault. If the fault persists, contact the OBS O&M team.

OkHttp Error After an SDK Upgrade
---------------------------------

::

   Exception in thread "main" java.lang.NoSuchMethodError: 'okhttp3.RequestBody okhttp3.RequestBody.create(java.lang.String, okhttp3.MediaType)'
       at com.obs.services.internal.RestConnectionService.createRequestBuilder(RestConnectionService.java:157)
       at com.obs.services.internal.RestConnectionService.setupConnection(RestConnectionService.java:148)
       at com.obs.services.internal.RestConnectionService.setupConnection(RestConnectionService.java:124)
       at com.obs.services.internal.RestStorageService.performRequest(RestStorageService.java:395)
       at com.obs.services.internal.RestStorageService.performRequest(RestStorageService.java:388)

This error occurs because OkHttp of an earlier version was used after the SDK upgrade. To resolve this issue, upgrade OkHttp to a required version by referring to :ref:`Resolving Dependency Missing or Conflicts <obs_21_0303>`.

StackOverflowError After an SDK Upgrade
---------------------------------------

::

   Caused by: java.lang.StackOverflowError
       at sun.misc.URLClassPath.getResource(URLClassPath.java:211) ~[?:1.8.0_91]
       at java.net.URLClassLoader$1.run(URLClassLoader.java:365) ~[?:1.8.0_91]
       at java.net.URLClassLoader$1.run(URLClassLoader.java:362) ~[?:1.8.0_91]
       at java.security.AccessController.doPrivileged(Native Method) ~[?:1.8.0_91]
       at java.net.URLClassLoader.findClass(URLClassLoader.java:361) ~[?:1.8.0_91]
       at java.lang.ClassLoader.loadClass(ClassLoader.java:424) ~[?:1.8.0_91]
       at java.lang.ClassLoader.loadClass(ClassLoader.java:357) ~[?:1.8.0_91]
       at org.apache.catalina.loader.WebappClassLoaderBase.loadClass(WebappClassLoaderBase.java:1806)

Check the JVM parameter **xss** and set it to **1 MB**. **xss** indicates the memory size allocated to each thread started by the JVM. By default, the value of **xss** is 256 KB for JDK 1.4 and 1 MB for JDK 1.5 or later.

SSL peer shut down incorrectly
------------------------------

::

   javax.net.ssl.SSLException: SSL peer shut down incorrectly
       at sun.security.ssl.InputRecord.readV3Record(InputRecord.java:596)
       at sun.security.ssl.InputRecord.read(InputRecord.java:532)
       at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:975)
       at sun.security.ssl.SSLSocketImpl.readDataRecord(SSLSocketImpl.java:933)
       at sun.security.ssl.AppInputStream.read(AppInputStream.java:105)
       at obs.shaded.okio.Okio$2.read(Okio.java:140)
       at obs.shaded.okio.AsyncTimeout$2.read(AsyncTimeout.java:237)
       at obs.shaded.okio.RealBufferedSource.read(RealBufferedSource.java:51)
       at obs.shaded.okhttp3.internal.http1.Http1ExchangeCodec$AbstractSource.read(Http1ExchangeCodec.java:389)
       at obs.shaded.okhttp3.internal.http1.Http1ExchangeCodec$FixedLengthSource.read(Http1ExchangeCodec.java:427)
       at obs.shaded.okhttp3.internal.connection.Exchange$ResponseBodySource.read(Exchange.java:286)
       at obs.shaded.okio.RealBufferedSource$1.read(RealBufferedSource.java:447)
       at java.util.zip.InflaterInputStream.fill(InflaterInputStream.java:238)
       at java.util.zip.InflaterInputStream.read(InflaterInputStream.java:158)
       at java.util.zip.GZIPInputStream.read(GZIPInputStream.java:117)
       at sun.nio.cs.StreamDecoder.readBytes(StreamDecoder.java:284)
       at sun.nio.cs.StreamDecoder.implRead(StreamDecoder.java:326)
       at sun.nio.cs.StreamDecoder.read(StreamDecoder.java:178)
       at java.io.InputStreamReader.read(InputStreamReader.java:184)
       at java.io.BufferedReader.fill(BufferedReader.java:161)
       at java.io.BufferedReader.readLine(BufferedReader.java:324)
       at java.io.BufferedReader.readLine(BufferedReader.java:389)

Do not read file streams by line during a download on the client. For details, see the demo for :ref:`a streaming download <obs_21_0702>`.

Others
------

For details, see :ref:`FAQs <obs_21_2100>`.
