

## Overview

This document provides an overview of APIs and SDK code samples related to COS inventory.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Creating an inventory job | Creates an inventory job for a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries the inventory jobs of bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting inventory jobs | Deletes an inventory job from a bucket |

## Creating Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job for a bucket.

#### Method prototype

```java
public SetBucketInventoryConfigurationResult setBucketInventoryConfiguration(String bucketName, InventoryConfiguration inventoryConfiguration);
public SetBucketInventoryConfigurationResult setBucketInventoryConfiguration(SetBucketInventoryConfigurationRequest setBucketInventoryConfigurationRequest);
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-inventory)
```java
// The bucket name must contain appid
String bucketName = "examplebucket-1250000000";

InventoryConfiguration inventoryConfiguration = new InventoryConfiguration();
InventoryCosBucketDestination inventoryCosBucketDestination = new InventoryCosBucketDestination();
// Set format and prefix of the destination bucket for inventory output
inventoryCosBucketDestination.setAccountId("2779643970");
inventoryCosBucketDestination.setBucketArn("qcs::cos:ap-guangzhou::examplebucket-1250000000");
inventoryCosBucketDestination.setEncryption(new ServerSideEncryptionCOS());
inventoryCosBucketDestination.setFormat(InventoryFormat.CSV);
inventoryCosBucketDestination.setPrefix("inventory-output");
InventoryDestination inventoryDestination = new InventoryDestination();
inventoryDestination.setCosBucketDestination(inventoryCosBucketDestination);
inventoryConfiguration.setDestination(inventoryDestination);

// Set inventory scheduling frequency, scan prefix, ID, etc.
inventoryConfiguration.setEnabled(true);
inventoryConfiguration.setId("1");
InventorySchedule inventorySchedule = new InventorySchedule();
inventorySchedule.setFrequency(InventoryFrequency.Daily);
inventoryConfiguration.setSchedule(inventorySchedule);
InventoryPrefixPredicate inventoryFilter = new InventoryPrefixPredicate("test/");
inventoryConfiguration.setInventoryFilter(new InventoryFilter(inventoryFilter));
inventoryConfiguration.setIncludedObjectVersions(InventoryIncludedObjectVersions.All);
// Set optional output fields
List<String> optionalFields = new LinkedList<String>();
optionalFields.add(InventoryOptionalField.Size.toString());
optionalFields.add(InventoryOptionalField.LastModifiedDate.toString());
inventoryConfiguration.setOptionalFields(optionalFields);
SetBucketInventoryConfigurationRequest setBucketInventoryConfigurationRequest = new SetBucketInventoryConfigurationRequest();
setBucketInventoryConfigurationRequest.setBucketName(bucketName);
setBucketInventoryConfigurationRequest.setInventoryConfiguration(inventoryConfiguration);
cosClient.setBucketInventoryConfiguration(setBucketInventoryConfigurationRequest);

inventoryConfiguration.setId("2");
inventorySchedule.setFrequency(InventoryFrequency.Weekly);
cosClient.setBucketInventoryConfiguration(setBucketInventoryConfigurationRequest);
```

#### Parameter description

| Parameter | Description | Type |
| -------------------------------------- | ---------------------- | -------------------------------------- |
| setBucketInventoryConfigurationRequest | Request to set static website for bucket | SetBucketInventoryConfigurationRequest |

Request member description:

| Request Member | Setting Method | Description | Type |
| ---------------------- | ------------------- | ------------------------------------------------------------ | ---------------------- |
| bucketName  | Constructor or set method | Bucket for which to set an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String                 |
| inventoryConfiguration | Constructor or set method | Inventory configuration of bucket                                             | InventoryConfiguration |

`InventoryConfiguration` member description:

| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | -------------------- |
| id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |
| destination            | Information of the bucket to store the inventory result after export                                | InventoryDestination |
| isEnabled              | Inventory status flag                                           | Boolean              |
| inventoryFilter        | Filters the objects to be analyzed. The inventory feature will analyze the objects that match the prefix set in `Filter` | InventoryFilter      |
| includedObjectVersions | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | String |
| optionalFields         | Name of fields that can be optionally included in the inventory result | List<String>         |
| schedule               | Configures inventory job frequency                                             | InventorySchedule    |

`InventoryDestination` member description:

| Parameter | Description | Type |
| -------------------- | ------------------------------ | ----------------------------- |
| cosBucketDestination | Information of the bucket to store the inventory result after export | InventoryCosBucketDestination |

`InventoryCosBucketDestination` member description:

| Parameter  | Description | Type |
| ---------- | ----------------------------------------- | ------------------- |
| accountId  | Bucket owner ID                         | String              |
| bucketArn  | Name of the bucket where the inventory result is stored | String |
| format | File format of the inventory result. Valid values: CSV | String |
| prefix | Prefix of the inventory result | String |
| encryption | Option to provide server-side encryption for the inventory result            | InventoryEncryption |

`InventoryFilter` member description:

| Parameter | Description | Type |
| --------- | -------------- | ------------------------ |
| predicate | Filters the objects to be analyzed | InventoryFilterPredicate |

An implementation class of `InventoryFilter` is `InventoryPrefixPredicate` with the following members:

| Parameter  | Description | Type |
| -------- | -------------------- | ------ |
| prefix | Prefix of the objects to be analyzed | String |

`InventorySchedule` member description:

| Parameter | Description | Type |
| --------- | --------------------------------------------------------- | ------ |
| frequency | Inventory job frequency. Enumerated values: Daily, Weekly | String |

#### Response description

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Error code description

The following describes some common errors that may occur when you make requests using this API.

| Error Code | Description | Status Code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You most likely do not have access permission for the bucket | HTTP 403 Forbidden   |

## Querying Inventory Jobs

#### Feature description

This API (GET Bucket inventory) is used to query the inventory job information in a bucket.

#### Method prototype

```java
public GetBucketInventoryConfigurationResult getBucketInventoryConfiguration(String bucketName, String id) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-inventory)
```java
String bucketName = "examplebucket-1250000000";
String id = "1";
GetBucketInventoryConfigurationResult getBucketInventoryConfigurationResult = cosClient.getBucketInventoryConfiguration(bucketName, id);
```

#### Parameter description

| Parameter  | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for which to query an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |

#### Response description

- Success: `GetBucketInventoryConfigurationResult` is returned, which contains the configuration information of the inventory corresponding to the specified ID for the bucket.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Querying All Inventories

#### Feature description

This API (List Bucket Inventory Configurations) is used to request that all inventory jobs in a bucket be returned.

#### Method prototype

```java
public ListBucketInventoryConfigurationsResult listBucketInventoryConfigurations(ListBucketInventoryConfigurationsRequest listBucketInventoryConfigurationsRequest) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-list-bucket-inventory)
```java
String bucketName = "examplebucket-1250000000";      
ListBucketInventoryConfigurationsRequest listBucketInventoryConfigurationsRequest = new ListBucketInventoryConfigurationsRequest();
listBucketInventoryConfigurationsRequest.setBucketName(bucketName);
ListBucketInventoryConfigurationsResult listBucketInventoryConfigurationsResult = cosClient.listBucketInventoryConfigurations(listBucketInventoryConfigurationsRequest);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| bucketName        | Destination bucket to store the inventory result in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| continuationToken |  If `IsTruncated` in the COS response body is `true` and there is a parameter value in the `NextContinuationToken` node, you can use this parameter as the parameter value of `continuation-token` to get the inventory job information of the next page | String |

#### Response description

- Success: `ListBucketInventoryConfigurationsResult` is returned, which contains the configuration information of the inventory corresponding to the specified ID for the bucket.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Deleting Inventory Job

#### Feature description

This API (DELETE Bucket inventory) is used to delete a specified inventory job of a bucket.

#### Method prototype

```java
public DeleteBucketInventoryConfigurationResult deleteBucketInventoryConfiguration(String bucketName, String id) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-inventory)
```java
String bucketName = "examplebucket-1250000000";      
String id = "1";
cosClient.deleteBucketInventoryConfiguration(bucketName, id);
```

#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for which to delete an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |

#### Response description

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
