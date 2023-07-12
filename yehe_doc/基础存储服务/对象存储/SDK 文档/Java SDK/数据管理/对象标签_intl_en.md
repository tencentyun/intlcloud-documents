## Overview

This document provides an overview of APIs and SDK code samples related to object tagging.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Tagging an object | Tags an uploaded object. |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object. |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object. |


## Tagging an Object

#### Description

This API is used to tag an object.

#### Method prototype

```java
public SetObjectTaggingResult setObjectTagging(SetObjectTaggingRequest setObjectTaggingRequest);
```

#### Sample 1. Tagging an uploaded object

```java
String bucketName = "examplebucket-1250000000";
String key = "exampletkey";
List<Tag> tags = new LinkedList<>();
tags.add(new Tag("tag1", "value1"));
tags.add(new Tag("tag2", "value2"));
ObjectTagging objectTagging = new ObjectTagging(tags);
SetObjectTaggingRequest setObjectTaggingRequest = new SetObjectTaggingRequest(bucketName, key, objectTagging);
cosclient.setObjectTagging(setObjectTaggingRequest);
```

#### Sample 2. Tagging an object when it is uploaded

```java
String bucketName = "examplebucket-1250000000";
String key = "testfiles/testTagging.txt";
InputStream is = new ByteArrayInputStream(new byte[]{'d', 'a', 't', 'a'});
ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setHeader("x-cos-tagging", "tag1=value1&tag2=value2");
cosclient.putObject(bucketName, key, is, objectMetadata);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------------------ | ------------------ | ------------------------------------ |
| setObjectTaggingRequest | Object tagging request | SetObjectTaggingRequest |

The request members are described as follows:

| Request Member | Setting Method | Description | Type |
| -------------------  | ----------------- | ------------------------ | -------------------------- |
| bucketName | Via a constructor or the `set` method | Bucket of the object to tag in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| Key | Via a constructor or the `set` method | Key of the object to tag. An object key uniquely identifies an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| objectTagging | Via a constructor or the `set` method | Object tagging | ObjectTagging |

`ObjectTagging` member description:

| Parameter | Description | Type |
| ------  | ---- | ---- |
| tagSet | Tags to add to the object | List&lt;Tag> |

`Tag` member description:

| Parameter | Description | Type |
| ----- | ---- | ---- |
| key | Tag key | String |
| value | Tag value | String |

#### Response description

- Success: No value is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Querying Object Tags

### Description

This API is used to query the existing tags of a specified object.

#### Method prototype

```java
public GetObjectTaggingResult getObjectTagging(GetObjectTaggingRequest getObjectTaggingRequest);
```

#### Sample request

```java
String bucketName = "exampletbucket-1250000000";
String key = "exampletkey";
GetObjectTaggingRequest getObjectTaggingRequest = new GetObjectTaggingRequest(bucketName, key);
GetObjectTaggingResult getObjectTaggingResult = cosclient.getObjectTagging(getObjectTaggingRequest);
List<Tag> resultTagSet = getObjectTaggingResult.getTagSet();
System.out.println(resultTagSet.toString());
```

#### Parameter description

| Parameter | Description | Type |
| ---------- | ---------- | ------ |
| getObjectTaggingRequest | Request to query the tags of an object | GetObjectTaggingRequest |

The request members are described as follows:

| Request Member | Setting Method | Description | Type |
| -------------------- | ----------------- | ------------------------ | ------------------------- |
| bucketName | Via a constructor or the `set` method | Bucket of the object to tag in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| Key | Via a constructor or the `set` method | Key of the object to tag. An object key uniquely identifies an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response description

- Success: `GetObjectTaggingResult` is returned, which includes the tag information of the object.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Deleting Object Tags

#### Description

This API is used to delete the existing tags of a specified object.

#### Method prototype

```java
public DeleteObjectTaggingResult deleteObjectTagging(DeleteObjectTaggingRequest deleteObjectTaggingRequest);
```

#### Sample request

```java
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
DeleteObjectTaggingRequest deleteObjectTaggingRequest = new DeleteObjectTaggingRequest(bucketName, key);
cosclient.deleteObjectTagging(deleteObjectTaggingRequest);
```

#### Parameter description

| Parameter | Description | Type |
| --------- | ---------- | ------ |
| deleteObjectTaggingRequest | Request to delete the tags of an object | DeleteObjectTaggingRequest |

The request members are described as follows:

| Request Member | Setting Method | Description | Type |
| -------------------- | ------------------ | ----------------------- | -------------------------- |
| bucketName | Via a constructor or the `set` method | Bucket of the object to tag in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| Key | Via a constructor or the `set` method | Key of the object to tag. An object key uniquely identifies an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response description

- Success: No value is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
