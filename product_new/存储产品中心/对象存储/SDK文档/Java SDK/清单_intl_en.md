

## Overview

This document provides an overview of APIs and SDK code samples related to inventory.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting an inventory job | Sets an inventory job in a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries inventory jobs for a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job of a bucket |

## Setting Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job in a bucket.

#### Method prototype

```java
public SetBucketInventoryConfigurationResult setBucketInventoryConfiguration(String bucketName, InventoryConfiguration inventoryConfiguration);
public SetBucketInventoryConfigurationResult setBucketInventoryConfiguration(SetBucketInventoryConfigurationRequest setBucketInventoryConfigurationRequest);
```

#### Sample request

```java
// The bucket name should include the `appid`
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
cosclient.setBucketInventoryConfiguration(setBucketInventoryConfigurationRequest);

inventoryConfiguration.setId("2");
inventorySchedule.setFrequency(InventoryFrequency.Weekly);
cosclient.setBucketInventoryConfiguration(setBucketInventoryConfigurationRequest);
```

#### Parameter description

| Parameter Name | Description | Type |
| -------------------------------------- | ---------------------- | -------------------------------------- |
| setBucketInventoryConfigurationRequest | Request to set static website for bucket | SetBucketInventoryConfigurationRequest |

`Request` member description:

| Request Member | Setting Method | Description | Type |
| ---------------------- | ------------------- | ------------------------------------------------------------ | ---------------------- |
| bucketName  | Constructor or set method | Bucket for which to set an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                 |
| inventoryConfiguration | Constructor or set method | Inventory configuration of bucket                                             | InventoryConfiguration |

`InventoryConfiguration` member description:

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | -------------------- |
| id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |
| destination            | Information of the bucket where the inventory result is stored after export                                | InventoryDestination |
| isEnabled              | Inventory status flag                                           | Boolean              |
| inventoryFilter        | Filters the objects to be analyzed. The inventory feature will analyze the objects that match the prefix set in `Filter` | InventoryFilter      |
| includedObjectVersions | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | String |
| optionalFields         | Name of fields that can be optionally included in the inventory result | List<String>         |
| schedule               | Configures inventory job frequency                                             | InventorySchedule    |

`InventoryDestination` member description:

| Parameter Name | Description | Type |
| -------------------- | ------------------------------ | ----------------------------- |
| cosBucketDestination | Information of the bucket where the inventory result is stored after export | InventoryCosBucketDestination |

`InventoryCosBucketDestination` member description:

| Parameter Name | Description | Type |
| ---------- | ----------------------------------------- | ------------------- |
| accountId  | Bucket owner ID                         | String              |
| bucketArn  | Name of the bucket where the inventory result is stored | String |
| format | File format of the inventory result. CSV is available | String |
| prefix | Prefix of the inventory result | String |
| encryption | Option to provide server-side encryption for the inventory result            | InventoryEncryption |

`InventoryFilter` member description:

| Parameter Name | Description | Type |
| --------- | -------------- | ------------------------ |
| predicate | Filters the objects to be analyzed | InventoryFilterPredicate |

An implementation class of `InventoryFilter` is `InventoryPrefixPredicate` with the following members:

| Parameter Name | Description | Type |
| -------- | -------------------- | ------ |
| prefix | Prefix of the objects to be analyzed | String |

`InventorySchedule` member description:

| Parameter Name | Description | Type |
| --------- | --------------------------------------------------------- | ------ |
| frequency | Inventory job frequency. Enumerated values: Daily, Weekly | String |

#### Returned result description

- Success: no returned value.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Error code description

Some frequent special errors that may occur with this request are listed below:

| Error code | Description | Status code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You probably do not have access to the bucket. | HTTP 403 Forbidden |

## Querying Inventory Job

#### Feature description

This API (GET Bucket inventory) is used to query the inventory job information in a bucket.

#### Method prototype

```java
public GetBucketInventoryConfigurationResult getBucketInventoryConfiguration(String bucketName, String id) throws CosClientException, CosServiceException;
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";
String id = "1";
GetBucketInventoryConfigurationResult getBucketInventoryConfigurationResult = cosclient.getBucketInventoryConfiguration(bucketName, id);

```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for which to query an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |

#### Returned result description

- Success: `GetBucketInventoryConfigurationResult` is returned, which contains the configuration information of the inventory corresponding to the specified ID for the bucket.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

## Querying All Inventories

#### Feature description

This API (List Bucket Inventory Configurations) is used to request that all inventory jobs in a bucket be returned.

#### Method prototype

```java
public ListBucketInventoryConfigurationsResult listBucketInventoryConfigurations(ListBucketInventoryConfigurationsRequest listBucketInventoryConfigurationsRequest) throws CosClientException, CosServiceException;
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";      
ListBucketInventoryConfigurationsRequest listBucketInventoryConfigurationsRequest = new ListBucketInventoryConfigurationsRequest();
listBucketInventoryConfigurationsRequest.setBucketName(bucketName);
ListBucketInventoryConfigurationsResult listBucketInventoryConfigurationsResult = cosclient.listBucketInventoryConfigurations(listBucketInventoryConfigurationsRequest);
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| bucketName        | Destination bucket where to store inventory results in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| continuationToken | If `IsTruncated` in the COS response body is `true` and there is a parameter value in the `NextContinuationToken` node, you can use this parameter as the parameter value of `continuation-token` to get the inventory job information of the next page | String |

#### Returned result description

- Success: `ListBucketInventoryConfigurationsResult` is returned, which contains the configuration information of the inventory corresponding to the specified ID for the bucket.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

## Deleting Inventory Job

#### Feature description

This API (DELETE Bucket inventory) is used to delete a specified inventory job of a bucket.

#### Method prototype

```java
public DeleteBucketInventoryConfigurationResult deleteBucketInventoryConfiguration(String bucketName, String id) throws CosClientException, CosServiceException;
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";      
String id = "1";
cosclient.deleteBucketInventoryConfiguration(bucketName, id);
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for which to delete an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |

#### Returned result description

- Success: no returned value.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).
