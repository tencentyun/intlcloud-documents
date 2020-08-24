## Overview

This document provides an overview of APIs and SDK code samples related to custom domain name.

| API | Operation Name | Operation Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting custom domain name | Sets custom domain name information for a bucket |
| GET Bucket domain | Querying custom domain name | Queries the custom domain name information of a bucket |

## Setting Custom Domain Name

#### Feature description

This API (PUT Bucket domain) is used to configure a custom domain name for a bucket.

#### Method prototype

```java
public void setBucketDomainConfiguration(String bucketName, BucketDomainConfiguration configuration);
public void setBucketDomainConfiguration(SetBucketDomainConfigurationRequest setBucketDomainConfigurationRequest);
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";
BucketDomainConfiguration bucketDomainConfiguration = new BucketDomainConfiguration();
DomainRule domainRule = new DomainRule();
domainRule.setStatus(DomainRule.ENABLED);
domainRule.setType(DomainRule.REST);
domainRule.setName("qq.com");
domainRule.setForcedReplacement(DomainRule.CNAME);
bucketDomainConfiguration.getDomainRules().add(domainRule);
cosclient.setBucketDomainConfiguration(bucketName, bucketDomainConfiguration);
BucketDomainConfiguration bucketDomainConfiguration1 = cosclient.getBucketDomainConfiguration(bucketName);
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------------------------------- | ------------------------ | ----------------------------------- |
| setBucketDomainConfigurationRequest | Request to set custom domain name for bucket | SetBucketDomainConfigurationRequest |

`Request` member description:

| Request Member | Setting Method | Description | Type |
| ------------- | ------------------- | ------------------------------------------------------------ | ------------------------- |
| bucketName  | Constructor or set method | Bucket for which to set a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                 |
| configuration | Constructor or set method | Custom domain name configuration of bucket                                        | BucketDomainConfiguration |

`BucketDomainConfiguration` member description:

| Parameter Name | Description | Type |
| ----------- | ---------------------- | ---------------------------- |
| domainRules | Custom domain name configuration of bucket | List<DomainRule> domainRules |

`DomainRule` member description:

| Parameter Name | Description | Type |
| ----------------- | ----------------------------------------- | ------ |
| name                  | Custom domain name                                                   | String |
| status            | Domain name status. Valid values: ENABLED, DISABLED                     | String |
| type              | Type of bound origin server. Valid values: REST, WEBSITE                       | String |
| forcedReplacement | Forcibly overwrites existing configuration. Valid values: CNAME, TXT | String |

#### Returned result description

- Success: no returned value.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Returned error code description

Some frequent special errors that may occur with this request are listed below:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | The domain name record already exists, and no forced overwriting is set in the request. Or, the domain name record does not exist, but forced overwriting is set in the request. |
| HTTP 451 Unavailable For Legal Reasons | The domain name is served in Mainland China but has no ICP filing.                          |

## Querying Custom Domain Name

#### Feature description

This API (GET Bucket domain) is used to query the custom domain name information of a bucket.

#### Method prototype

```java
public BucketDomainConfiguration getBucketDomainConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";
BucketDomainConfiguration bucketDomainConfiguration1 = cosclient.getBucketDomainConfiguration(bucketName);
String domainTxtVerification = bucketDomainConfiguration1.getDomainTxtVerification()
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for which to query a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Returned result description

- Success: `BucketDomainConfiguration` is returned, which contains the custom domain name configuration information of the bucket.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Return parameter description

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| domainTxtVerification | Domain name verification information. This field is an MD5 check value, whose original string is in the following format: `cos[Region][BucketName-APPID][BucketCreateTime]`, where `Region` is the bucket region and `BucketCreateTime` is the bucket creation time in GMT | String |
