

## Overview

This document provides an overview of APIs and SDK code samples for custom domains.

| API | Operation | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom domain | Sets a custom domain for a bucket |
| GET Bucket domain    | Querying a custom domain | Queries the custom domain of a bucket |

## Setting Custom Domains

#### Feature description

This API is used to set a custom domain for a bucket.

#### Method prototype

```java
public void setBucketDomainConfiguration(String bucketName, BucketDomainConfiguration configuration);
public void setBucketDomainConfiguration(SetBucketDomainConfigurationRequest setBucketDomainConfigurationRequest);
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-domain)
```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, select **Object Operations** > **Uploading Objects** on the left sidebar, and see **simple operations** > **uploading a COSClient instance**.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

BucketDomainConfiguration bucketDomainConfiguration = new BucketDomainConfiguration();
DomainRule domainRule = new DomainRule();
domainRule.setStatus(DomainRule.ENABLED);
domainRule.setType(DomainRule.REST);
domainRule.setName("qq.com");
domainRule.setForcedReplacement(DomainRule.CNAME);
bucketDomainConfiguration.getDomainRules().add(domainRule);
cosClient.setBucketDomainConfiguration(bucketName, bucketDomainConfiguration);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------------------------- | ------------------------ | ----------------------------------- |
| setBucketDomainConfigurationRequest | Sets a custom domain request for a bucket | SetBucketDomainConfigurationRequest |

Description of the `Request` member:

| Request Member | Setting Method | Description | Type |
| ------------- | ------------------- | ------------------------------------------------------------ | ------------------------- |
| bucketName | Constructor or `set` method | Bucket that the custom domain is set for, formatted as `BucketName-APPID`. For more information, see the bucket naming conventions section in [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| configuration | Constructor or `set` method | Custom domain configuration of the bucket | BucketDomainConfiguration |

Description of the `BucketDomainConfiguration` member:

| Parameter | Description | Type |
| ----------- | ---------------------- | ---------------------------- |
| domainRules | Custom doamin configuration of the bucket | List&lt;DomainRule> domainRules |

Description of the `DomainRule` member:

| Parameter | Description | Type |
| ----------------- | ----------------------------------------- | ------ |
| name    | Custom domain name                                                                           | String      |
| status | Status of the domain name. Valid values: `ENABLED`, `DISABLED` | String |
| type    | Type of the origin server to bind. Valid values: `REST`, `WEBSITE`                                                             | String      |
| forcedReplacement | Replaces existing configurations. Valid values: `CNAME`, `TXT`                    | String |

#### Response description

- Success: No value is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Error codes

The following describes some common errors that may occur when you call this API:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The domain record already exists, and forced overwrite is not specified in the request; OR the domain record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The domain does not have an ICP filing in the Chinese mainland                          |

## Querying a Custom Domain

#### Description

This API is used to query the custom domain set for a bucket.

#### Method prototype

```java
public BucketDomainConfiguration getBucketDomainConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-domain)
```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, select **Object Operations** > **Uploading Objects** on the left sidebar, and see **simple operations** > **uploading a COSClient instance**.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

BucketDomainConfiguration bucketDomainConfiguration = cosClient.getBucketDomainConfiguration(bucketName);
String domainTxtVerification = bucketDomainConfiguration1.getDomainTxtVerification();
System.out.println(domainTxtVerification);
for (DomainRule rule : bucketDomainConfiguration.getDomainRules()) {
    System.out.println(rule.getName());
    System.out.println(rule.getStatus());
    System.out.println(rule.getType());
    System.out.println(rule.getClass());
}
```

#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for custom domain query, in the format of `BucketName-APPID`. For more information, see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

- Success: returns `BucketDomainConfiguration`, including the custom domain configuration of the bucket.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| domainTxtVerification | Domain verification information. This field is an MD5 checksum of a character string in the format: `cos[Region][BucketName-APPID][BucketCreateTime]`, where `Region` is the bucket region and `BucketCreateTime` is the time the bucket was created in GMT format | String |
