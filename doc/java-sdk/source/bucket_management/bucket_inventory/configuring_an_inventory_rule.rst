:original_name: obs_21_0417.html

.. _obs_21_0417:

Configuring an Inventory Rule
=============================

Function
--------

This API configures an inventory rule for the bucket. With this API, object information in a bucket (source) is regularly listed and saved as CSV files. These files are then stored in a specified bucket (destination). In this manner, you can easily manage objects in a bucket. A source bucket can also be the destination bucket. A bucket inventory file contains the following object-related information: object versions, sizes, storage classes, tags, encryption statuses, and last modification time.

You can encrypt bucket inventory files using SSE-KMS.

Restrictions
------------

-  To configure an inventory rule for a bucket, you must be the bucket owner or have the required permission (**obs:bucket:PutBucketInventoryConfiguration** in IAM or **PutBucketInventoryConfiguration** in a bucket policy).
-  **Bucket versions**

   -  Bucket inventories can be generated only for OBS 3.0 buckets, but they can be stored in either OBS 3.0 or OBS 2.0.

-  **Number of bucket inventory rules**

   -  A bucket can have a maximum of 10 inventory rules.

-  **Source and destination buckets**

   -  The source bucket (for which a bucket inventory rule is configured) and the destination bucket (where the generated inventory files are stored) must belong to the same account.
   -  The source bucket and the destination bucket must be in the same region.
   -  Default encryption cannot be enabled for the destination bucket configured for storing inventory files.

-  **Functions**

   -  Inventory files must be in the CSV format.
   -  OBS can generate inventory files for all objects in a bucket or a group of objects whose names begin with the same prefix.
   -  If a bucket has multiple inventory rules, the filtering criteria in these rules must not overlap.

      -  If a bucket already has an inventory rule for the entire bucket, new inventory rules that filter objects by prefixes cannot be created. If you need an inventory rule that covers only a subset of objects in the bucket, first delete the inventory rule configured for the entire bucket.
      -  If an inventory rule that filters objects by a specified prefix already exists, you cannot create an inventory rule for the entire bucket. To create an inventory rule for the entire bucket, make sure that the bucket has no inventory rules that filter objects by specified prefixes.
      -  If a bucket already has an inventory rule that filters objects by the object name prefix, such as **ab**, the filter of a new inventory rule cannot be any prefix that contains **a**, **b**, or **ab**. If you still need to create such rules, delete the inventory rule that uses the prefix **ab** first.

   -  Bucket inventory files only support SSE-KMS encryption.

-  **Permissions**

   -  Inventory files are uploaded to the destination bucket by an OBS system user. Therefore, you need to grant the system user the permission to write objects to the destination bucket.

-  **Others**

   -  The bucket inventory function is offered for free, but inventory files are billed for the storage they use.

Method
------

obsClient.setInventoryConfiguration(:ref:`SetInventoryConfigurationRequest <obs_21_0417__table649204716910>` :ref:`request <obs_21_0417__table649204716910>`)

Request Parameters
------------------

.. _obs_21_0417__table649204716910:

.. table:: **Table 1** SetInventoryConfigurationRequest

   +------------------------+-----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Type                                                            | Mandatory (Yes/No) | Description                                                                                                                                                                       |
   +========================+=================================================================+====================+===================================================================================================================================================================================+
   | bucketName             | String                                                          | Yes                | **Explanation:**                                                                                                                                                                  |
   |                        |                                                                 |                    |                                                                                                                                                                                   |
   |                        |                                                                 |                    | Bucket name.                                                                                                                                                                      |
   |                        |                                                                 |                    |                                                                                                                                                                                   |
   |                        |                                                                 |                    | **Restrictions:**                                                                                                                                                                 |
   |                        |                                                                 |                    |                                                                                                                                                                                   |
   |                        |                                                                 |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                  |
   |                        |                                                                 |                    | -  A bucket name:                                                                                                                                                                 |
   |                        |                                                                 |                    |                                                                                                                                                                                   |
   |                        |                                                                 |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                      |
   |                        |                                                                 |                    |    -  Cannot be formatted as an IP address.                                                                                                                                       |
   |                        |                                                                 |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                        |
   |                        |                                                                 |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                   |
   |                        |                                                                 |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                           |
   |                        |                                                                 |                    |                                                                                                                                                                                   |
   |                        |                                                                 |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request. |
   |                        |                                                                 |                    |                                                                                                                                                                                   |
   |                        |                                                                 |                    | **Default value**:                                                                                                                                                                |
   |                        |                                                                 |                    |                                                                                                                                                                                   |
   |                        |                                                                 |                    | None                                                                                                                                                                              |
   +------------------------+-----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | inventoryConfiguration | :ref:`InventoryConfiguration <obs_21_0417__table9778173316119>` | Yes                | **Explanation:**                                                                                                                                                                  |
   |                        |                                                                 |                    |                                                                                                                                                                                   |
   |                        |                                                                 |                    | Inventory configurations for a bucket. For details, see :ref:`Table 2 <obs_21_0417__table9778173316119>`.                                                                         |
   +------------------------+-----------------------------------------------------------------+--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _obs_21_0417__table9778173316119:

.. table:: **Table 2** InventoryConfiguration

   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Type              | Mandatory (Yes/No) | Description                                                                                                                                                                                                                                |
   +========================+===================+====================+============================================================================================================================================================================================================================================+
   | configurationId        | String            | Yes                | **Explanation:**                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | ID of a bucket inventory rule.                                                                                                                                                                                                             |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Restrictions:**                                                                                                                                                                                                                          |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | The rule ID allows letters (a-z, A-Z), digits (0-9), hyphens (-), underscores (_), and periods (.).                                                                                                                                        |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Value range**:                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | The value can be up to 64 characters long.                                                                                                                                                                                                 |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Default value**:                                                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | None                                                                                                                                                                                                                                       |
   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | isEnabled              | boolean           | Yes                | **Explanation:**                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | Whether the bucket inventory rule is enabled.                                                                                                                                                                                              |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Value range**:                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **true**: The rule is enabled, and an inventory file is generated.                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **false**: The rule is disabled. No inventory file is generated.                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Default value**:                                                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | true                                                                                                                                                                                                                                       |
   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | objectPrefix           | String            | No                 | **Explanation:**                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | Used to filter objects. Only objects with the specified name prefix are included in the inventory.                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Value range**:                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                              |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Default value**:                                                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | None                                                                                                                                                                                                                                       |
   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | frequency              | String            | Yes                | **Explanation:**                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | Intervals when inventories are generated. You can set this parameter to **Daily** or **Weekly**. An inventory is generated within one hour from when it is configured for the first time. Then it is generated at the specified intervals. |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Value range**:                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Daily**: Inventories are generated once a day.                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Weekly**: Inventories are generated once a week.                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Default value**:                                                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | None                                                                                                                                                                                                                                       |
   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | inventoryFormat        | String            | Yes                | **Explanation:**                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | Inventory file format. Only the CSV format is supported.                                                                                                                                                                                   |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Value range**:                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | CSV                                                                                                                                                                                                                                        |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Default value**:                                                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | None                                                                                                                                                                                                                                       |
   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | destinationBucket      | String            | Yes                | **Explanation:**                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | Name of the bucket for storing inventories.                                                                                                                                                                                                |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Restrictions:**                                                                                                                                                                                                                          |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | -  A bucket name must be unique across all accounts and regions.                                                                                                                                                                           |
   |                        |                   |                    | -  A bucket name:                                                                                                                                                                                                                          |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    |    -  Must be 3 to 63 characters long and start with a digit or letter. Lowercase letters, digits, hyphens (-), and periods (.) are allowed.                                                                                               |
   |                        |                   |                    |    -  Cannot be formatted as an IP address.                                                                                                                                                                                                |
   |                        |                   |                    |    -  Cannot start or end with a hyphen (-) or period (.).                                                                                                                                                                                 |
   |                        |                   |                    |    -  Cannot contain two consecutive periods (..), for example, **my..bucket**.                                                                                                                                                            |
   |                        |                   |                    |    -  Cannot contain periods (.) and hyphens (-) adjacent to each other, for example, **my-.bucket** or **my.-bucket**.                                                                                                                    |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | -  If you repeatedly create buckets of the same name in the same region, no error will be reported and the bucket attributes comply with those set in the first creation request.                                                          |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Default value**:                                                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | None                                                                                                                                                                                                                                       |
   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | inventoryPrefix        | String            | No                 | **Explanation:**                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | The prefix of the inventory file name.                                                                                                                                                                                                     |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Value range**:                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | The value must contain 1 to 1,024 characters.                                                                                                                                                                                              |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Default value**:                                                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | If you do not specify this parameter, **BucketInventory** is used as the prefix by default.                                                                                                                                                |
   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | includedObjectVersions | String            | Yes                | **Explanation:**                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | Whether versions of objects are included in an inventory.                                                                                                                                                                                  |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Value range**:                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | -  If this parameter is set to **All**, all the versions of objects are included in the inventory, and version-related fields are added to the inventory, including: **VersionId**, **IsLatest**, and **DeleteMarker**.                    |
   |                        |                   |                    | -  If this parameter is set to **Current**, the inventory only lists information about the current object version and does not include any version-related fields.                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Default value**:                                                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | None                                                                                                                                                                                                                                       |
   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | optionalFields         | ArrayList<String> | No                 | **Explanation:**                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | Additional object metadata fields that are contained in an inventory file.                                                                                                                                                                 |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Value range**:                                                                                                                                                                                                                           |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Size**: Object size.                                                                                                                                                                                                                     |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **LastModifiedDate**: Last time when the object was modified.                                                                                                                                                                              |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **StorageClass**: The storage class of the object.                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **ETag**: The ETag value of the object.                                                                                                                                                                                                    |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **IsMultipartUploaded**: Whether the object was uploaded in a :ref:`multipart upload <obs_21_0607>`.                                                                                                                                       |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **ReplicationStatus**: The cross-region replication status of the object.                                                                                                                                                                  |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **EncryptionStatus**: The encryption status of the object.                                                                                                                                                                                 |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | **Default value**:                                                                                                                                                                                                                         |
   |                        |                   |                    |                                                                                                                                                                                                                                            |
   |                        |                   |                    | None                                                                                                                                                                                                                                       |
   +------------------------+-------------------+--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Responses
---------

.. table:: **Table 3** Common response headers

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================+
   | statusCode            | int                   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP status code.                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Value range**:                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | A status code is a group of digits that can be **2**\ *xx* (indicating successes) or **4**\ *xx* or **5**\ *xx* (indicating errors). It indicates the status of a response. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | responseHeaders       | Map<String, Object>   | **Explanation:**                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | HTTP response header list, composed of tuples. In a tuple, the **String** key indicates the name of the header, and the **Object** value indicates the value of the header. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **Default value**:                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | None                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Code Examples
-------------

This example configures an inventory for bucket **example-bucket** to list objects with the name prefix **exampleObjectPrefix**. The inventory files are stored in bucket **example-target-bucket** and the name prefix of the inventory files is **exampleInventoryPrefix**.

::

   import com.obs.services.ObsClient;
   import com.obs.services.exception.ObsException;
   import com.obs.services.model.HeaderResponse;
   import com.obs.services.model.inventory.InventoryConfiguration;
   import com.obs.services.model.inventory.SetInventoryConfigurationRequest;
   public class SetInventoryConfiguration001
   {
       public static void main(String[] args) {
           // Obtain an AK/SK pair using environment variables or import the AK/SK pair in other ways. Using hard coding may result in leakage.
           // Obtain an AK/SK pair on the management console.
           String ak = System.getenv("ACCESS_KEY_ID");
           String sk = System.getenv("SECRET_ACCESS_KEY_ID");
           // (Optional) If you are using a temporary AK/SK pair and a security token to access OBS, you are advised not to use hard coding, which may result in information leakage.
           // Obtain an AK/SK pair and a security token using environment variables or import them in other ways.
           // String securityToken = System.getenv("SECURITY_TOKEN");
           // Enter the endpoint corresponding to the region where the bucket is to be created.
           String endPoint = "https://your-endpoint";
           // Obtain an endpoint using environment variables or import it in other ways.
           // String endPoint = System.getenv("ENDPOINT");

           // Create an ObsClient instance.
           // Use the permanent AK/SK pair to initialize the client.
           ObsClient obsClient = new ObsClient(ak, sk,endPoint);
           // Use the temporary AK/SK pair and security token to initialize the client.
           // ObsClient obsClient = new ObsClient(ak, sk, securityToken, endPoint);

           try {
               // Set the following parameters.
               String exampleBucketName = "example-bucket";
               String exampleTargetBucketName = "example-target-bucket";
               String exampleConfigurationId = "exampleConfigId001";
               String exampleInventoryPrefix = "exampleInventoryPrefix";
               String exampleObjectPrefix = "exampleObjectPrefix";
               // Set parameters for the inventory rule.
               InventoryConfiguration exampleConfiguration = new InventoryConfiguration();
               exampleConfiguration.setDestinationBucket(exampleTargetBucketName);
               exampleConfiguration.setConfigurationId(exampleConfigurationId);
               exampleConfiguration.setInventoryFormat(InventoryConfiguration.InventoryFormatOptions.CSV);
               exampleConfiguration.setFrequency(InventoryConfiguration.FrequencyOptions.DAILY);
               exampleConfiguration.setEnabled(true);
               exampleConfiguration.setIncludedObjectVersions(
                       InventoryConfiguration.IncludedObjectVersionsOptions.CURRENT);
               exampleConfiguration.setInventoryPrefix(exampleInventoryPrefix);
               exampleConfiguration.setObjectPrefix(exampleObjectPrefix);
               // Set additional metadata fields that will be contained in the inventory file.
               exampleConfiguration
                       .getOptionalFields()
                       .add(InventoryConfiguration.OptionalFieldOptions.IS_MULTIPART_UPLOADED);
               exampleConfiguration.getOptionalFields().add(InventoryConfiguration.OptionalFieldOptions.ETAG);
               exampleConfiguration
                       .getOptionalFields()
                       .add(InventoryConfiguration.OptionalFieldOptions.REPLICATION_STATUS);
               SetInventoryConfigurationRequest request =
                       new SetInventoryConfigurationRequest(exampleBucketName, exampleConfiguration);
               // Set the inventory rule.
               HeaderResponse response = obsClient.setInventoryConfiguration(request);
               System.out.println("SetInventoryConfiguration succeeded");
               System.out.println("HTTP Code: " + response.getStatusCode());
           } catch (ObsException e) {
               System.out.println("SetInventoryConfiguration failed");
               // Request failed. Print the HTTP status code.
               System.out.println("HTTP Code: " + e.getResponseCode());
               // Request failed. Print the server-side error code.
               System.out.println("Error Code:" + e.getErrorCode());
               // Request failed. Print the error details.
               System.out.println("Error Message:" + e.getErrorMessage());
               // Request failed. Print the request ID.
               System.out.println("Request ID:" + e.getErrorRequestId());
               System.out.println("Host ID:" + e.getErrorHostId());
           } catch (Exception e) {
               System.out.println("SetInventoryConfiguration failed");
               // Print other error information.
               e.printStackTrace();
           }
       }
   }
