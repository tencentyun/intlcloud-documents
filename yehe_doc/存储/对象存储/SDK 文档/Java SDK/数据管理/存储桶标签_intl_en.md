

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes a specified bucket tag |

## Setting Bucket Tag

#### Feature description

This API (PUT Bucket tagging) is used to set a tag for an existing bucket.

#### Method prototype

```java
public void setBucketTaggingConfiguration(SetBucketTaggingConfigurationRequest setBucketTaggingConfigurationRequest);
public void setBucketTaggingConfiguration(String bucketName, BucketTaggingConfiguration bucketTaggingConfiguration);
```

#### Sample request
[//]: # (.cssg-snippet-put-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
List<TagSet> tagSetList = new LinkedList<TagSet>();
TagSet tagSet = new TagSet();
tagSet.setTag("age", "18");
tagSet.setTag("name", "xiaoming");
tagSetList.add(tagSet);
BucketTaggingConfiguration bucketTaggingConfiguration = new BucketTaggingConfiguration();
bucketTaggingConfiguration.setTagSets(tagSetList);
SetBucketTaggingConfigurationRequest setBucketTaggingConfigurationRequest =
new SetBucketTaggingConfigurationRequest(bucketName, bucketTaggingConfiguration);
cosclient.setBucketTaggingConfiguration(setBucketTaggingConfigurationRequest);
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------------------------ | ------------------ | ------------------------------------ |
| setBucketTaggingConfigurationRequest | Request to set bucket tag | SetBucketTaggingConfigurationRequest  |

`Request` member description:

| Request Member | Setting Method | Description | Type |
| -------------------- | ------------------- | ------------------------------------------------------------ | -------------------------- |
| bucketName  | Constructor or set method | Bucket for which to set a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                 |
| taggingConfiguration | Constructor or set method | Bucket tag configuration                                             | BucketTaggingConfiguration |

`BucketLoggingConfiguration` member description:

| Parameter Name | Description | Type |
| -------- | -------------------- | ------------ |
| tagSets  | Bucket tag configuration set | List&lt;TagSet&gt; |

`TagSet` member description:

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------------------- |
| tags | Tag key and value, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 128 bytes | Map&lt;String, String&gt; |

#### Returned result description

- Success: no returned value.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

## Querying Bucket Tag

#### Feature description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Method prototype

```java
public BucketTaggingConfiguration getBucketTaggingConfiguration(String bucketName);
```

#### Sample request
[//]: # (.cssg-snippet-get-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
BucketTaggingConfiguration bucketTaggingConfiguration = cosclient.getBucketTaggingConfiguration(bucketName);
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for which to query a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Returned result description

- Success: `BucketTaggingConfiguration` is returned, which contains the tag configuration information of the bucket.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

## Deleting Bucket Tag

#### Feature description

This API (DELETE Bucket tagging) is used to delete an existing tag of a specified bucket.

#### Method prototype

```java
public void deleteBucketTaggingConfiguration(String bucketName);
```

#### Sample request
[//]: # (.cssg-snippet-delete-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
cosclient.deleteBucketTaggingConfiguration(bucketName);
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket for which to delete a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Returned result description

- Success: no returned value.
- Failure: an error (e.g., authentication failed) occurred and a `CosClientException` or `CosServiceException` exception was thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).
