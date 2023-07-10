## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning configuration of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning configuration of a bucket |

## Setting Versioning

#### Feature description

This API is used to set the versioning configuration for a bucket.

#### Method prototype
```java
public void setBucketVersioningConfiguration(SetBucketVersioningConfigurationRequest setBucketVersioningConfigurationRequest)
    throws CosClientException, CosServiceException;
```

#### Parameter description
| Parameter | Description | Type |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| setBucketVersioningConfigurationRequest | Versioning configuration | SetBucketVersioningConfigurationRequest |


#### Response description
  - Success: no value is returned.
  - Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

**Enable versioning**

[//]: # ".cssg-snippet-put-bucket-versioning"
```java
String bucketName = "examplebucket-1250000000";
// Enable versioning
cosClient.setBucketVersioningConfiguration(
        new SetBucketVersioningConfigurationRequest(bucketName,
                new BucketVersioningConfiguration(BucketVersioningConfiguration.ENABLED)));
```

**Suspending Versioning**

```java
String bucketName = "examplebucket-1250000000";
// Suspend versioning
cosClient.setBucketVersioningConfiguration(
new SetBucketVersioningConfigurationRequest(bucketName,
new BucketVersioningConfiguration(BucketVersioningConfiguration.SUSPENDED)));
```

## Querying Versioning

#### Feature description

This API is used to query the versioning configuration of a bucket.

#### Method prototype
```java
// Method 1: enter the bucket name
public BucketVersioningConfiguration getBucketVersioningConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// Method 2: get the configuration through GetBucketVersioningConfigurationRequest
public BucketVersioningConfiguration getBucketVersioningConfiguration(
    GetBucketVersioningConfigurationRequest getBucketVersioningConfigurationRequest)
        throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-get-bucket-versioning"
```java
String bucketName = "examplebucket-1250000000";
// Get versioning information
BucketVersioningConfiguration bvc =
        cosClient.getBucketVersioningConfiguration(bucketName);
// Get versioning information
BucketVersioningConfiguration bvc2 = cosClient.getBucketVersioningConfiguration(
        new GetBucketVersioningConfigurationRequest(bucketName));
```


#### Parameter description

| Parameter | Description | Type |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| getBucketVersioningConfigurationRequest | Request to get the versioning configuration | GetBucketVersioningConfigurationRequest |


#### Response description
- Success: the versioning configuration of the bucket is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
