## Overview

This document provides an overview of APIs and SDK sample codes related to cross-origin access.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting a cross-origin access configuration | Sets the cross-origin access permissions of bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying a cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

## Setting Cross-Origin Access Configuration

#### Feature description

This API (PUT Bucket cors) is used to set cross-origin access configuration on a bucket.

#### Method prototype

```java
public void setBucketCrossOriginConfiguration(String bucketName, BucketCrossOriginConfiguration bucketCrossOriginConfiguration);
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-cors)
```java
// Enter the bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
| bucketCrossOriginConfiguration | The cross-domain access rules set for a bucket | BucketCrossOriginConfiguration |
List<CORSRule> corsRules = new ArrayList<CORSRule>();
CORSRule corsRule = new CORSRule();
// Rule name
corsRule.setId("set-bucket-cors-test");
// Allowed HTTP method
corsRule.setAllowedMethods(CORSRule.AllowedMethods.PUT, CORSRule.AllowedMethods.GET, CORSRule.AllowedMethods.HEAD);
corsRule.setAllowedHeaders("x-cos-grant-full-control");
corsRule.setAllowedOrigins("http://mail.qq.com", "http://www.qq.com", "http://video.qq.com");
corsRule.setExposedHeaders("x-cos-request-id");
corsRule.setMaxAgeSeconds(60);
corsRules.add(corsRule);
bucketCORS.setRules(corsRules);
cosClient.setBucketCrossOriginConfiguration(bucketName, bucketCORS);
```


#### Parameter description

| Parameter | Description | Type |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| bucketCrossOriginConfiguration | Cross-origin access policy set for a bucket | BucketCrossOriginConfiguration |

#### Response description

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Querying Cross-Origin Access Configuration

#### Feature description

This API is used to query the cross-origin access configuration of a bucket.

#### Method prototype

```java
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-cors)
```java
// Enter the bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
BucketCrossOriginConfiguration corsGet = cosClient.getBucketCrossOriginConfiguration(bucketName);
List<CORSRule> corsRules = corsGet.getRules();
for (CORSRule rule : corsRules) {
    List<CORSRule.AllowedMethods> allowedMethods = rule.getAllowedMethods();
    List<String> allowedHeaders = rule.getAllowedHeaders();
    List<String> allowedOrigins = rule.getAllowedOrigins();
    List<String> exposedHeaders = rule.getExposedHeaders();
    int maxAgeSeconds = rule.getMaxAgeSeconds();
}
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

- Success: the cross-origin access rule of the bucket is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Deleting Cross-Origin Access Configuration

#### Feature description

This API is used to delete the cross-origin access configuration of a bucket.

#### Method prototype

```java
public void deleteBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-cors)
```java
// Bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucketCrossOriginConfiguration(bucketName);
```

#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
