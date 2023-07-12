## Overview

This document provides an overview of APIs and SDK code samples related to bucket copying.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-bucket replication | Sets a cross-bucket replication rule for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-bucket replication | Queries the cross-bucket replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-bucket replication | Deletes a cross-bucket replication rule of a bucket |

## Setting Cross-Bucket Replication

#### Description

This API (PUT Bucket replication) is used to set the cross-bucket replication rule for a bucket.

#### Method prototype

```java
public void setBucketReplicationConfiguration(
        SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest)
                throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-replication)
```java
// Source bucket name, including appid
String bucketName = "examplebucket-1250000000";

BucketReplicationConfiguration bucketReplicationConfiguration = new BucketReplicationConfiguration();
// Configure initiator identity in the format: qcs::cam::uin/<OwnerUin>:uin/<SubUin>
bucketReplicationConfiguration.setRoleName("qcs::cam::uin/100000000001:uin/100000000001");

// Configure the destination bucket and storage class in the QCS format: qcs::cos:[region]::[bucketname-AppId]
ReplicationDestinationConfig replicationDestinationConfig = new ReplicationDestinationConfig();
replicationDestinationConfig.setBucketQCS("qcs::cos:ap-beijing::destinationbucket-1250000000");
replicationDestinationConfig.setStorageClass(StorageClass.Standard);

// Configure the rule status and prefix
ReplicationRule replicationRule = new ReplicationRule();
replicationRule.setStatus(ReplicationRuleStatus.Enabled);
replicationRule.setPrefix("");
replicationRule.setDestinationConfig(replicationDestinationConfig);
// Add a rule
String ruleId = "replication-to-beijing";
bucketReplicationConfiguration.addRule(replicationRule);

SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest =
        new SetBucketReplicationConfigurationRequest(bucketName, bucketReplicationConfiguration);
cosClient.setBucketReplicationConfiguration(setBucketReplicationConfigurationRequest);
```



#### Parameter description

| Parameter  | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| setBucketReplicationConfigurationRequest | Cross-bucket replication configuration | SetBucketReplicationConfigurationRequest |

#### Response description

  - Success: No value is returned.
  - Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Querying Cross-Bucket Replication

#### Description

This API (GET Bucket replication) is used to query the cross-bucket replication rule of a bucket.

#### Method prototype
```java
// Method 1 to get the cross-bucket replication configuration of the bucket
public BucketReplicationConfiguration getBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// Method 2 to get the cross-bucket replication configuration of the bucket        
public BucketReplicationConfiguration getBucketReplicationConfiguration(
            GetBucketReplicationConfigurationRequest getBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-replication)
```java
String bucketName = "examplebucket-1250000000";

// Method 1 to get the cross-bucket replication configuration of the bucket
BucketReplicationConfiguration brcfRet = cosClient.getBucketReplicationConfiguration(bucketName);

// Method 2 to get the cross-bucket replication configuration of the bucket
BucketReplicationConfiguration brcfRet2 = cosClient.getBucketReplicationConfiguration(
        new GetBucketReplicationConfigurationRequest(bucketName));
```


#### Parameter description

| Parameter  | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| getBucketReplicationConfigurationRequest | Obtaining cross-bucket replication configuration requests                                       | GetBucketReplicationConfigurationRequest |

#### Response description
- Success: Returns the cross-bucket replication rule for the bucket.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Deleting Cross-Bucket Replication

#### Description

This API (DELETE Bucket replication) is used to delete a cross-bucket replication rule from a bucket.

#### Method prototype
```java
// Method 1 to delete the cross-bucket replication configuration of the bucket
public void deleteBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// Method 2 to delete the cross-bucket replication configuration of the bucket        
public void deleteBucketReplicationConfiguration(
            DeleteBucketReplicationConfigurationRequest deleteBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-replication)
```java
String bucketName = "examplebucket-1250000000";

// Method 1 to delete the cross-bucket replication configuration of the bucket
cosClient.deleteBucketReplicationConfiguration(bucketName);

// Method 2 to delete the cross-bucket replication configuration of the bucket
cosClient.deleteBucketReplicationConfiguration(new DeleteBucketReplicationConfigurationRequest(bucketName));
```


#### Parameter description

| Parameter | Description | Type |
| ------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| deleteBucketReplicationConfigurationRequest | Deleting cross-bucket replication configuration requests                                       | DeleteBucketReplicationConfigurationRequest |

#### Response description

  - Success: No value is returned.
  - Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
