## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.

>! COS Java SDK v5.6.52 or later is required.
>

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting bucket referer configuration | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying bucket referer configuration | Queries a bucket referer allowlist or blocklist |

## Setting Bucket Referer Configuration

#### Description

This API (PUT Bucket referer) is used to set a referer allowlist/blocklist for a bucket.

#### Method prototype

```java
public void setBucketRefererConfiguration(String bucketName, BucketRefererConfiguration configuration) throws CosClientException, CosServiceException;

public void setBucketRefererConfiguration(SetBucketRefererConfigurationRequest setBucketRefererConfigurationRequest) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Source bucket name, including appid
String bucketName = "examplebucket-1250000000";

BucketRefererConfiguration configuration = new BucketRefererConfiguration();

// Enable hotlink protection
configuration.setStatus(BucketRefererConfiguration.DISABLED);
// Set the hotlink protection type to allowlist
//configuration.setRefererType(BucketRefererConfiguration.WHITELIST);
// Set the hotlink protection type to blocklist (either allowlist or blocklist)
configuration.setRefererType(BucketRefererConfiguration.BLACKLIST);

// Enter the domain name to be set
configuration.addDomain("test.com");
configuration.addDomain("test.1.com");

// (Optional) Set whether to allow access with an empty referer (default value: DENY)
configuration.setEmptyReferConfiguration(BucketRefererConfiguration.DENY);
// configuration.setEmptyReferConfiguration(BucketRefererConfiguration.ALLOW);

cosClient.setBucketRefererConfiguration(bucketName, configuration);
```

#### Parameter description

| Parameter  | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| configuration | Referer configuration of a bucket                                               | BucketRefererConfiguration |

BucketRefererConfiguration description:

| Parameter          | Description                                         | Type    | Required | Method      |
| -------------- | ----------------------------------------------- | ------ | ---- | -------- |
| Status         | Whether to enable hotlink protection. Enumerated values: `Enabled`, `Disabled`           | String | Yes   | setStatus |
| RefererType    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String | Yes   | setRefererType |
| Domain         | Effective domain name. Supports one or multiple domain names with port numbers and IPs. The wildcard \* is also supported.        | String | Yes   | addDomain |
| EmptyReferConfiguration |  Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` | String | No  | setEmptyReferConfiguration |

#### Response description

  - Success: No value is returned.
  - Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Querying Bucket Referer Configuration

#### Description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

#### Method prototype

```java
public BucketRefererConfiguration getBucketRefererConfiguration(String bucketName) throws CosClientException, CosServiceException
```

#### Sample request

```java
// Source bucket name, including appid
String bucketName = "examplebucket-1250000000";

BucketRefererConfiguration configuration = cosClient.getBucketRefererConfiguration(bucketName);

if (configuration == null) {
    System.out.printf("bucket %s does not have referer configuration\n", bucketName);
    return;
}

System.out.printf("status: %s\n", configuration.getStatus());
System.out.printf("referer type: %s\n", configuration.getRefererType());
System.out.printf("empty referer config: %s\n", configuration.getEmptyReferConfiguration());

for (String domain : configuration.getDomainList()) {
    System.out.printf("domain: %s\n", domain);
}
```

#### Parameter description

| Parameter | Description | Type |
| ----------- | -------- | ---- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

- Success: The referer allowlist or blocklist of the bucket is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
