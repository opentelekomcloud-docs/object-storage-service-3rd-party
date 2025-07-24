:original_name: obs_33_0517.html

.. _obs_33_0517:

Restoring a Cold Object
=======================

Function
--------

To obtain the content of an object in the Cold storage class, you need to restore the object first and then you can download it. After an object is restored, a copy of the object is saved in the Standard storage class. By doing so, the object in the Cold storage class and its copy in the Standard storage class co-exist in the bucket. The copy will be automatically deleted once its retention period expires.

This API is used to restore Cold objects in a specified bucket.

Restrictions
------------

-  To restore a Cold object, you must be the bucket owner or have the required permission (**obs:object:RestoreObject** in IAM or **RestoreObject** in a bucket policy.)
-  To prolong the validity period of the Cold data restored, you can repeatedly restore the data, but you will be billed for each restore. After a second restore, the validity period of Standard object copies will be prolonged, and you need to pay for storing these copies during the prolonged period.

Method
------

**func** (obsClient ObsClient) RestoreObject(input \*\ :ref:`RestoreObjectInput <obs_33_0517__table206638398315>`) (output \*\ :ref:`BaseModel <obs_33_0517__table14455523>`, err error)

Request Parameters
------------------

.. table:: **Table 1** List of request parameters

   +-----------------+----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                           | Mandatory (Yes/No) | Description                                                                                                     |
   +=================+================================================================+====================+=================================================================================================================+
   | input           | \*\ :ref:`RestoreObjectInput <obs_33_0517__table206638398315>` | Yes                | **Explanation:**                                                                                                |
   |                 |                                                                |                    |                                                                                                                 |
   |                 |                                                                |                    | Input parameters for restoring a Cold object. For details, see :ref:`Table 2 <obs_33_0517__table206638398315>`. |
   +-----------------+----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------+

.. _obs_33_0517__table206638398315:

.. table:: **Table 2** RestoreObjectInput

   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                                      | Mandatory (Yes/No) | Description                                                                                                                                                                                |
   +=================+===========================================================+====================+============================================================================================================================================================================================+
   | Bucket          | string                                                    | Yes                | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | Bucket name                                                                                                                                                                                |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Restrictions:**                                                                                                                                                                          |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                           |
   |                 |                                                           |                    | -  A bucket name:                                                                                                                                                                          |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                               |
   |                 |                                                           |                    |    -  Cannot be formatted as an IP address.                                                                                                                                                |
   |                 |                                                           |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                 |
   |                 |                                                           |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                            |
   |                 |                                                           |                    |    -  Cannot contain a period (.) and a hyphen (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                  |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.          |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | None                                                                                                                                                                                       |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key             | string                                                    | Yes                | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | Object name. An object is uniquely identified by an object name in a bucket. An object name is a complete path that does not contain the bucket name.                                      |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | The value must contain 1 to 1,024 characters.                                                                                                                                              |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | None                                                                                                                                                                                       |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | VersionId       | string                                                    | No                 | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | Version ID of the Cold object to be restored                                                                                                                                               |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | None. If this parameter is left blank, the latest version of the object is specified.                                                                                                      |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Days            | int                                                       | Yes                | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | After an object is restored, a Standard copy of it is generated. This parameter specifies how long the Standard copy can be retained, that is, the validity period of the restored object. |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | The value ranges from 1 to 30, in days.                                                                                                                                                    |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | None                                                                                                                                                                                       |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Tier            | :ref:`RestoreTierType <obs_33_0517__table14688520194419>` | No                 | **Explanation:**                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | Retrieval speed tiers. You can select a suitable tier based on your requirements for retrieval speed.                                                                                      |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Value range**:                                                                                                                                                                           |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | For details, see :ref:`Table 3 <obs_33_0517__table14688520194419>`.                                                                                                                        |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | **Default value**:                                                                                                                                                                         |
   |                 |                                                           |                    |                                                                                                                                                                                            |
   |                 |                                                           |                    | Standard                                                                                                                                                                                   |
   +-----------------+-----------------------------------------------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_33_0517__table14688520194419:

.. table:: **Table 3** RestoreTierType

   +----------------------+---------------+--------------------------------------------------------------------------+
   | Constant             | Default Value | Description                                                              |
   +======================+===============+==========================================================================+
   | RestoreTierExpedited | Expedited     | Objects can be quickly restored from Cold storage within 1 to 5 minutes. |
   +----------------------+---------------+--------------------------------------------------------------------------+
   | RestoreTierStandard  | Standard      | Objects can be restored from Cold storage within 3 to 5 hours.           |
   +----------------------+---------------+--------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 4** List of returned results

   +-----------------------+---------------------------------------------------+---------------------------------------------------------------------------------+
   | Parameter             | Type                                              | Description                                                                     |
   +=======================+===================================================+=================================================================================+
   | output                | \*\ :ref:`BaseModel <obs_33_0517__table14455523>` | **Explanation:**                                                                |
   |                       |                                                   |                                                                                 |
   |                       |                                                   | Returned results. For details, see :ref:`Table 5 <obs_33_0517__table14455523>`. |
   +-----------------------+---------------------------------------------------+---------------------------------------------------------------------------------+
   | err                   | error                                             | **Explanation:**                                                                |
   |                       |                                                   |                                                                                 |
   |                       |                                                   | Error messages returned by the API                                              |
   +-----------------------+---------------------------------------------------+---------------------------------------------------------------------------------+

.. _obs_33_0517__table14455523:

.. table:: **Table 5** BaseModel

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================+
   | StatusCode            | int                   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP status code                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RequestId             | string                | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Request ID returned by the OBS server                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ResponseHeaders       | map[string][]string   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP response headers                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example restores the Cold object **example/objectname** in bucket **examplebucket**.

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
       input := &obs.RestoreObjectInput{}
       // Specify a bucket name.
       input.Bucket = "examplebucket"
       // Specify the object (example/objectname in this example).
       input.Key = "example/objectname"
       // Specify the version ID of the object to be restored.
       input.VersionId = "G001117FCE89978B0000401205D5DC9A"
       // Specify how long the restored object will be retained, in days. 1 is used as an example, which can be any value from 1 to 30.
       input.Days = 1
       // Specify the restore speed (obs.RestoreTierExpedited as an example). By default, the object is restored at a standard speed.
       input.Tier = obs.RestoreTierExpedited
       // Restore the Cold object.
       output, err := obsClient.RestoreObject(input)
       if err == nil {
           fmt.Printf("Restore object(%s) under the bucket(%s) successful!\n", input.Key, input.Bucket)
           fmt.Printf("RequestId:%s\n", output.RequestId)
           return
       }
       fmt.Printf("Restore object(%s) under the bucket(%s) fail!\n", input.Key, input.Bucket)
       if obsError, ok := err.(obs.ObsError); ok {
           fmt.Println("An ObsError was found, which means your request sent to OBS was rejected with an error response.")
           fmt.Println(obsError.Error())
       } else {
           fmt.Println("An Exception was found, which means the client encountered an internal problem when attempting to communicate with OBS, for example, the client was unable to access the network.")
           fmt.Println(err)
       }
   }

.. note::

   -  The object specified in **ObsClient.RestoreObject** must be in the Cold storage class. Otherwise, an error will be reported.
   -  **RestoreObjectInput.Days** is used to specify how long (1 to 30 days) the restored object will be retained and **RestoreObjectInput.Tier** is used to specify how fast the object will be restored.
