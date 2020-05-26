

## Overview

This document provides an overview of APIs and SDK code samples related to log management.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for the source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration information of the source bucket |

## Setting Log Management

#### Feature description

This API (PUT Bucket logging) is used to enable logging for the source bucket and store its access logs in a specified destination bucket.

#### Method prototype

```java
public void setBucketLoggingConfiguration(SetBucketLoggingConfigurationRequest setBucketLoggingConfigurationRequest);
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";
BucketLoggingConfiguration bucketLoggingConfiguration = new BucketLoggingConfiguration();
bucketLoggingConfiguration.setDestinationBucketName(bucketName);
bucketLoggingConfiguration.setLogFilePrefix("logs");
SetBucketLoggingConfigurationRequest setBucketLoggingConfigurationRequest = new SetBucketLoggingConfigurationRequest(bucketName, bucketLoggingConfiguration);
cosclient.setBucketLoggingConfiguration(setBucketLoggingConfigurationRequest);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------------------------ | ---------------- | ------------------------------------ |
| setBucketLoggingConfigurationRequest | Request to enable logging feature | SetBucketLoggingConfigurationRequest |

`Request` member description:

| Request Member | Setting Method | Description | Type |
| -------------------- | ------------------- | ------------------------------------------------------------ | -------------------------- |
| bucketName  | Constructor or set method | Source bucket for which to enable the logging feature in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| loggingConfiguration | Constructor or set method | Bucket logging feature configuration                                         | BucketLoggingConfiguration |

`BucketLoggingConfiguration` member description:

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| logFilePrefix         | Specified path in the destination bucket for storing logs                               | String |

#### Returned result description

- Success: no returned value.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

## Querying Log Management

#### Feature description

This API (GET Bucket logging) is used to query the log configuration information of a specified bucket.

#### Method prototype

```java
public BucketLoggingConfiguration getBucketLoggingConfiguration(String bucketName);
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";
BucketLoggingConfiguration bucketLoggingConfiguration = cosclient.getBucketLoggingConfiguration(bucketName);
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |

#### Returned result description

- Success: `BucketLoggingConfiguration` is returned, which contains the name of the destination bucket and specified path in the destination bucket for storing logs
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).
