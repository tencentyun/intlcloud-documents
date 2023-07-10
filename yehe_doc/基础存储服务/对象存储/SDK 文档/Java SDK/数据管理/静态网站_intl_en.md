

## Overview

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets static website configuration for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration information of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website

#### Feature description

This API (PUT Bucket website) is used to configure a static website for a bucket.

#### Method prototype

```java
public void setBucketWebsiteConfiguration(String bucketName, BucketWebsiteConfiguration configuration)
throws CosClientException, CosServiceException;
public void setBucketWebsiteConfiguration(SetBucketWebsiteConfigurationRequest setBucketWebsiteConfigurationRequest)
throws CosClientException, CosServiceException;
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";
// Set bucket website
BucketWebsiteConfiguration bucketWebsiteConfiguration = new BucketWebsiteConfiguration();
// Index file
bucketWebsiteConfiguration.setIndexDocumentSuffix("index.html");
// Routing rule
List<RoutingRule> routingRuleList = new ArrayList<RoutingRule>();
RoutingRule routingRule = new RoutingRule();
RoutingRuleCondition routingRuleCondition = new RoutingRuleCondition();
routingRuleCondition.setHttpErrorCodeReturnedEquals("404");
routingRule.setCondition(routingRuleCondition);
RedirectRule redirectRule = new RedirectRule();
redirectRule.setProtocol("https");
redirectRule.setReplaceKeyPrefixWith("404.html");
routingRule.setRedirect(redirectRule);
routingRuleList.add(routingRule);
bucketWebsiteConfiguration.setRoutingRules(routingRuleList);
cosclient.setBucketWebsiteConfiguration(bucketName, bucketWebsiteConfiguration);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------------------------ | ---------------------- | ------------------------------------ |
| setBucketWebsiteConfigurationRequest | Request to set static website for bucket | SetBucketWebsiteConfigurationRequest |

`Request` member description:

| Request Member | Setting Method | Description | Type |
| ------------- | ------------------- | ------------------------------------------------------------ | -------------------------- |
| bucketName  | Constructor or set method | Bucket for which to set a static website in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                 |
| configuration | Constructor or set method | Static website configuration of bucket                                         | BucketWebsiteConfiguration |

`BucketWebsiteConfiguration` member description:

| Parameter Name | Description | Type |
| --------------------- | ----------------------------------------- | ----------------- |
| indexDocumentSuffix   | Index document                                  | String            |
| errorDocument         | Error document                                  | String            |
| redirectAllRequestsTo | Configuration for redirecting all requests                        | RedirectRule      |
| routingRules          | Sets redirect rules. Up to 100 `RoutingRule` can be set | List<RoutingRule> |

`RoutingRule` member description:

| Parameter Name | Description | Type |
| --------- | ------------------------------------------------------------ | -------------------- |
| condition | Specifies the condition for redirect. Either prefix match-triggered redirect or error code-triggered redirect can be specified at a time | RoutingRuleCondition |
| redirect  | Redirect rule                                                   | RedirectRule         |

`RoutingRuleCondition` member description:

| Parameter Name | Description | Type |
| --------------------------- | -------------------- | -------------------- |
| keyPrefixEquals             | Specifies the path for prefix-triggered redirect | RoutingRuleCondition |
| httpErrorCodeReturnedEquals | Specifies error code for redirect     | RedirectRule         |

`RedirectRule` member description:

| Parameter Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ------ |
| protocol             | Specifies the protocol for global redirect                                         | String |
| replaceKeyPrefixWith | Replaces the matched prefix with the specified content, which can be set only if `Condition` is `KeyPrefixEquals` | String |
| replaceKeyWith       | Replaces the entire `Key` with the specified content                                    | String |
| httpRedirectCode     | Specifies the protocol for global redirect                                         | String |

#### Returned result description

- Success: no returned value.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

## Querying Static Website Configuration

#### Feature description

This API (GET Bucket website) is used to query the configuration information of a static website associated with a bucket.

#### Method prototype

```java
public BucketWebsiteConfiguration getBucketWebsiteConfiguration(String bucketName)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";
BucketWebsiteConfiguration bucketWebsiteConfiguration = cosclient.getBucketWebsiteConfiguration(bucketName);
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for which to query static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Returned result description

- Success: `BucketWebsiteConfiguration` is returned, which contains the static website configuration information of the bucket.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

## Deleting Static Website Configuration

#### Feature description

This API (DELETE Bucket website) is used to delete the static website configuration of a bucket.

#### Method prototype

```java
public void deleteBucketWebsiteConfiguration(String bucketName) throws CosClientException, CosServiceException;
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";
cosclient.deleteBucketWebsiteConfiguration(bucketName);
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for which to delete static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Returned result description

- Success: no returned value.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).
