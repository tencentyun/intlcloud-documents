

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a bucket |

## Setting a Bucket Tag

#### API description

This API is used to set tags for an existing bucket.

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
cosClient.setBucketTaggingConfiguration(setBucketTaggingConfigurationRequest);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------------------ | ------------------ | ------------------------------------ |
| setBucketTaggingConfigurationRequest | Request to set the bucket tag | SetBucketTaggingConfigurationRequest |

Request member description:

| Request Member | Set Method | Description | Type |
| -------------------- | ------------------- | ------------------------------------------------------------ | -------------------------- |
| bucketName | Constructor or set method | Bucket that the tag is set for, formatted as `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| taggingConfiguration | Constructor or set method | Tagging configuration of the bucket | BucketTaggingConfiguration |

Description of the `BucketLoggingConfiguration` member:

| Parameter | Description | Type |
| -------- | -------------------- | ------------ |
| tagSets  | Collection of tags for the bucket | List&lt;TagSet&gt; |

Description of the `TagSet` member:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------------------- |
| tags | The tag’s key and value, which cannot exceed 128 bytes and can contain letters, digits, spaces, plus signs (+), minus signs (−), underscores (_), equal signs (=), dots (.), colons (:), and slashes (/). | Map&lt;String, String&gt; |

#### Response description

- Success: No value is returned.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Querying Bucket Tags

#### API description

This API is used to query the existing tags of a specified bucket.

#### Method prototype

```java
public BucketTaggingConfiguration getBucketTaggingConfiguration(String bucketName);
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
BucketTaggingConfiguration bucketTaggingConfiguration = cosClient.getBucketTaggingConfiguration(bucketName);
```

#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket to query the tags from, formatted as `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

- Success: returns `BucketTaggingConfiguration`, including the bucket’s tagging configuration.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Deleting Bucket Tags

#### API description

This API is used to delete the existing tags from a bucket.

#### Method prototype

```java
public void deleteBucketTaggingConfiguration(String bucketName);
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucketTaggingConfiguration(bucketName);
```

#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket to delete the tags from, formatted as `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

- Success: No value is returned.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
