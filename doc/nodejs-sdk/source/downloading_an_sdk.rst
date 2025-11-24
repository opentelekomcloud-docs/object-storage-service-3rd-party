:original_name: obs_29_0001.html

.. _obs_29_0001:

Downloading an SDK
==================

Download
--------

-  Latest version of OBS Node.js SDK: `Download <https://github.com/opentelekomcloud-community/obs-nodejs-sdk>`__

Compatibility
-------------

-  Recommended versions: Node 0.12.\ *x*, Node4.\ *x*, Node6.\ *x*, Node8.\ *x*, or Node10.\ *x*
-  Interface changes: The following table describes the interfaces not completely compatible with earlier versions 2.1.\ *x*:

   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Interface                  | Description                                                                                                                                                                    |
   +============================+================================================================================================================================================================================+
   | ObsClient.listBuckets      | In the response, the data type of **InterfaceResult.Buckets** was changed to **Array**. **InterfaceResult.Buckets.Bucket** was deleted.                                        |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.setBucketAcl     | In the request, the data type of **Grants** was changed to **Array**. **Grants.Grant** was deleted.                                                                            |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.getBucketAcl     | In the response, the data type of **InterfaceResult.Grants** was changed to **Array**. **InterfaceResult.Grants.Grant** was deleted.                                           |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.setObjectAcl     | In the request, the data type of **Grants** was changed to **Array**. **Grants.Grant** was deleted.                                                                            |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.getObjectAcl     | In the response, the data type of **InterfaceResult.Grants** was changed to **Array**. **InterfaceResult.Grants.Grant** was deleted.                                           |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.setBucketLogging | In the request, the data type of **LoggingEnabled.TargetGrants** was changed to **Array**. **LoggingEnabled.TargetGrants.Grant** was deleted.                                  |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.getBucketLogging | In the response, the data type of **InterfaceResult.LoggingEnabled.TargetGrants** was changed to **Array**. **InterfaceResult.LoggingEnabled.TargetGrants.Grant** was deleted. |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.setBucketWebsite | In the request, the data type of **RoutingRules** was changed to **Array**. **RoutingRules.RoutingRule** was deleted.                                                          |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.getBucketWebsite | In the response, the data type of **InterfaceResult.RoutingRules** was changed to **Array**. **InterfaceResult.RoutingRules.RoutingRule** was deleted.                         |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.setBucketCors    | In the request, **CorsRule** was renamed as **CorsRules**.                                                                                                                     |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.getBucketCors    | In the response, **InterfaceResult.CorsRule** was renamed as **InterfaceResult.CorsRules**.                                                                                    |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.setBucketTagging | In the request, the data type of **TagSet** was changed to **Array**. **TagSet.Tag** was deleted.                                                                              |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ObsClient.getBucketTagging | In the response, the data type of **InterfaceResult.TagSet** was changed to **Array**. **InterfaceResult.TagSet.Tag** was deleted.                                             |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
