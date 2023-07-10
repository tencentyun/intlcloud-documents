## Overview

This document provides an overview of APIs and SDK sample codes for cross-origin resource sharing (CORS).

For more information, see [Cross-Origin Resource Sharing](https://intl.cloud.tencent.com/document/product/436/40697). When you set the CORS configuration, see [Setting Cross-Origin Resource Sharing (CORS)](https://intl.cloud.tencent.com/document/product/436/13318) or [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/11488).

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS configuration | Sets the CORS permissions of bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

## Setting CORS Configuration

#### Description

This API is used to set the CORS configuration of a specified bucket.

#### Method prototype

```java
public void setBucketCrossOriginConfiguration(String bucketName, BucketCrossOriginConfiguration bucketCrossOriginConfiguration);
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-cors)
```java
// Enter the bucket name in the format: BucketName-APPID.
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
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see the bucket naming conventions section in [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| bucketCrossOriginConfiguration | The cross-origin access rules set for a bucket | BucketCrossOriginConfiguration |

#### Response description

- Success: No value is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Querying CORS Configuration

#### Description

This API is used to query the CORS configuration of a bucket.

#### Method prototype

```java
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-cors)
```java
// Enter the bucket name in the format: BucketName-APPID.
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
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see the bucket naming conventions section in [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

-Success: Returns the cross-origin rules for the bucket.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Deleting CORS Configuration

#### Description

This API is used to delete the CORS configuration of a bucket.

#### Method prototype

```java
public void deleteBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-cors)
```java
Bucket. Format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucketCrossOriginConfiguration(bucketName);
```

#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see the bucket naming conventions section in [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

- Success: No value is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
