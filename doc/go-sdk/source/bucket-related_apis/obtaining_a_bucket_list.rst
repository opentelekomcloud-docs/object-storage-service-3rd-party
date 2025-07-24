:original_name: obs_33_0403.html

.. _obs_33_0403:

Obtaining a Bucket List
=======================

Function
--------

OBS buckets are containers for storing objects you upload to OBS. This API returns a list of all buckets that meet the specified conditions in all regions of the current account. Returned buckets are listed in alphabetical order.

Restrictions
------------

-  To obtain a bucket list, you must have the **obs:bucket:ListAllMyBuckets** permission.

Method
------

**func** (obsClient ObsClient) ListBuckets(input \*\ :ref:`ListBucketsInput <obs_33_0403__table14455523>`) (output \*\ :ref:`ListBucketsOutput <obs_33_0403__table2078171205919>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+----------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                     | Mandatory (Yes/No) | Description                                                                                                 |
   +=================+==========================================================+====================+=============================================================================================================+
   | input           | \*\ :ref:`ListBucketsInput <obs_33_0403__table14455523>` | No                 | **Explanation:**                                                                                            |
   |                 |                                                          |                    |                                                                                                             |
   |                 |                                                          |                    | Input parameters for obtaining a bucket list. For details, see :ref:`Table 2 <obs_33_0403__table14455523>`. |
   +-----------------+----------------------------------------------------------+--------------------+-------------------------------------------------------------------------------------------------------------+

.. _obs_33_0403__table14455523:

.. table:: **Table 2** ListBucketsInput

   +-----------------+-----------------+--------------------+---------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No) | Description                                       |
   +=================+=================+====================+===================================================+
   | QueryLocation   | bool            | No                 | **Explanation:**                                  |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | Whether to query the bucket region                |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | **Value range**:                                  |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | -  **true**: The bucket location is queried.      |
   |                 |                 |                    | -  **false**: The bucket location is not queried. |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | **Default value**:                                |
   |                 |                 |                    |                                                   |
   |                 |                 |                    | false                                             |
   +-----------------+-----------------+--------------------+---------------------------------------------------+

.. table:: **Table 3** BucketType

   ======== ============= =======================================
   Constant Default Value Description
   ======== ============= =======================================
   OBJECT   OBJECT        An object bucket
   POSIX    POSIX         A parallel POSIX-compatible file bucket
   ======== ============= =======================================

Responses
---------

.. table:: **Table 4** List of returned results

   +-----------------------+----------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | Parameter             | Type                                                           | Description                                                                          |
   +=======================+================================================================+======================================================================================+
   | output                | \*\ :ref:`ListBucketsOutput <obs_33_0403__table2078171205919>` | **Explanation:**                                                                     |
   |                       |                                                                |                                                                                      |
   |                       |                                                                | Returned results. For details, see :ref:`Table 5 <obs_33_0403__table2078171205919>`. |
   +-----------------------+----------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | err                   | error                                                          | **Explanation:**                                                                     |
   |                       |                                                                |                                                                                      |
   |                       |                                                                | Error messages returned by the API                                                   |
   +-----------------------+----------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. _obs_33_0403__table2078171205919:

.. table:: **Table 5** ListBucketsOutput

   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                | Description                                                                                                                                                                 |
   +=======================+=====================================================+=============================================================================================================================================================================+
   | StatusCode            | int                                                 | **Explanation:**                                                                                                                                                            |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | HTTP status code                                                                                                                                                            |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | **Value range**:                                                                                                                                                            |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | **Default value**:                                                                                                                                                          |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | None                                                                                                                                                                        |
   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                                              | **Explanation:**                                                                                                                                                            |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | Request ID returned by the OBS server                                                                                                                                       |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | **Default value**:                                                                                                                                                          |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | None                                                                                                                                                                        |
   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ResponseHeaders       | map[string][]string                                 | **Explanation:**                                                                                                                                                            |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | HTTP response headers                                                                                                                                                       |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | **Default value**:                                                                                                                                                          |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | None                                                                                                                                                                        |
   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Owner                 | :ref:`Owner <obs_33_0403__table324615128264>`       | **Explanation:**                                                                                                                                                            |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | The owner of the buckets listed                                                                                                                                             |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | **Value range**:                                                                                                                                                            |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | See :ref:`Owner <obs_33_0403__table324615128264>`.                                                                                                                          |
   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Buckets               | []\ :ref:`Bucket <obs_33_0403__table6719114116524>` | **Explanation:**                                                                                                                                                            |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | Bucket information list                                                                                                                                                     |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | **Value range**:                                                                                                                                                            |
   |                       |                                                     |                                                                                                                                                                             |
   |                       |                                                     | See :ref:`Bucket <obs_33_0403__table6719114116524>`.                                                                                                                        |
   +-----------------------+-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0403__table324615128264:

.. table:: **Table 6** Owner

   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory (Yes/No)                 | Description                                                                                |
   +=================+=================+====================================+============================================================================================+
   | ID              | string          | Yes if used as a request parameter | **Explanation:**                                                                           |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | Account (domain) ID of the owner                                                           |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | **Value range**:                                                                           |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | To obtain the account ID, see :ref:`How Do I Get My Account ID and User ID? <obs_23_1712>` |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | **Default value**:                                                                         |
   |                 |                 |                                    |                                                                                            |
   |                 |                 |                                    | None                                                                                       |
   +-----------------+-----------------+------------------------------------+--------------------------------------------------------------------------------------------+

.. _obs_33_0403__table6719114116524:

.. table:: **Table 7** Bucket

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                                               |
   +=======================+=======================+===========================================================================================================================================================================================================================================================================================================================+
   | Name                  | string                | **Explanation:**                                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | Bucket name                                                                                                                                                                                                                                                                                                               |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | **Restrictions:**                                                                                                                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                                                                                                          |
   |                       |                       | -  A bucket name:                                                                                                                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                                                                                                              |
   |                       |                       |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                                                                                               |
   |                       |                       |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                                                                                                |
   |                       |                       |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                                                                                                           |
   |                       |                       |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | CreationDate          | time.Time             | **Explanation:**                                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | Time when the bucket was created                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | **Default value**:                                                                                                                                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | None                                                                                                                                                                                                                                                                                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Location              | string                | **Explanation:**                                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | Region where a bucket is located                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | **Value range**:                                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                                           |
   |                       |                       | To learn about valid regions and endpoints, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__. An endpoint is the request address for calling an API. Endpoints vary depending on services and regions. To obtain the regions and endpoints, contact the enterprise administrator. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example lists all buckets.

::

   package main
   import (
       "fmt"
       "os"
       "obs-sdk-go/obs"
   )
   func main() {
       //Obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways. Using hard coding may result in leakage.
       //Obtain an AK/SK pair on the management console.
       ak := os.Getenv("AccessKeyID")
       sk := os.Getenv("SecretAccessKey")
       // (Optional) If you use a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding to reduce leakage risks. You can obtain an AK/SK pair using environment variables or import an AK/SK pair in other ways.
       // securityToken := os.Getenv("SecurityToken")
       // Enter the endpoint of the region where the bucket locates.
       endPoint := "https://your-endpoint"
       // Create an obsClient instance.
       // If you use a temporary AK/SK pair and a security token to access OBS, use the obs.WithSecurityToken method to specify a security token when creating an instance.
       obsClient, err := obs.New(ak, sk, endPoint/*, obs.WithSecurityToken(securityToken)*/)
       if err != nil {
           fmt.Printf("Create obsClient error, errMsg: %s", err.Error())
       }
       input := &obs.ListBucketsInput{}
   // Specify whether Location exists in the bucket list. true is used as an example. The default value is false.
       input.QueryLocation = true
       // Specify a bucket type. obs.OBJECT is used as an example, indicating that all buckets are listed. This parameter is not specified by default, indicating that all buckets and parallel file systems are listed.
       input.BucketType = obs.OBJECT
       // List buckets.
       output, err := obsClient.ListBuckets(input)
       if err == nil {
           fmt.Printf("List buckets successful!\n")
           fmt.Printf("RequestId:%s\n", output.RequestId)
           for index, val := range output.Buckets {
               fmt.Printf("Bucket[%d]-Name:%s,CreationDate:%s\n", index, val.Name, val.CreationDate)
           }
           return
       }
       fmt.Printf("List buckets fail!\n")
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }
