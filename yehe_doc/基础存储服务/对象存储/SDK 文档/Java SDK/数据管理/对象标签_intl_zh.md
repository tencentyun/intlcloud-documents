## 简介

本文档提供关于对象标签的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                     |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | 设置对象标签 | 为对象设置标签       |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | 查询对象标签 | 查询指定对象下已有的对象标签 |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | 删除对象标签 | 删除指定对象下已有的对象标签 |


## 设置对象标签

#### 功能说明

用于为对象设置标签。

#### 方法原型

```java
public SetObjectTaggingResult setObjectTagging(SetObjectTaggingRequest setObjectTaggingRequest);
```

#### 请求示例1：对已上传的对象设置标签

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

#### 请求示例2：上传对象时设置标签

```java
String bucketName = "examplebucket-1250000000";
String key = "testfiles/testTagging.txt";
InputStream is = new ByteArrayInputStream(new byte[]{'d', 'a', 't', 'a'});
ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setHeader("x-cos-tagging", "tag1=value1&tag2=value2");
cosclient.putObject(bucketName, key, is, objectMetadata);
```

#### 参数说明

| 参数名称                             | 描述               | 类型                                 |
| ------------------------------------ | ------------------ | ------------------------------------ |
| setObjectTaggingRequest | 对象标签设置请求 | SetObjectTaggingRequest |

Request 成员说明：

| Request 成员         | 设置方法            | 描述                      | 类型                       |
| -------------------  | ----------------- | ------------------------ | -------------------------- |
| bucketName  | 构造函数或 set 方法 | 设置标签的对象所在的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | 构造函数或者 set 方法 | 设置标签的对象键，对象键（Key）是对象在存储桶中的唯一标识，详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| objectTagging | 构造函数或 set 方法 | 对象的标签配置 | ObjectTagging |

ObjectTagging 成员说明：

| 参数名称 | 描述 | 类型 |
| ------  | ---- | ---- |
| tagSet | 对象的标签配置集合 | List&lt;Tag> |

Tag 成员说明：

|参数名称 | 描述 | 类型 |
| ----- | ---- | ---- |
| key | 标签的 key | String |
| value | 标签的 value | String |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

## 查询对象标签

### 功能说明

查询指定对象下已有的对象标签。

#### 方法原型

```java
public GetObjectTaggingResult getObjectTagging(GetObjectTaggingRequest getObjectTaggingRequest);
```

#### 请求示例

```java
String bucketName = "exampletbucket-1250000000";
String key = "exampletkey";
GetObjectTaggingRequest getObjectTaggingRequest = new GetObjectTaggingRequest(bucketName, key);
GetObjectTaggingResult getObjectTaggingResult = cosclient.getObjectTagging(getObjectTaggingRequest);
List<Tag> resultTagSet = getObjectTaggingResult.getTagSet();
System.out.println(resultTagSet.toString());
```

#### 参数说明

| 参数名称   | 描述        | 类型   |
| ---------- | ---------- | ------ |
| getObjectTaggingRequest | 对象标签查询请求 | GetObjectTaggingRequest |

Request 成员说明：

| Request 成员         | 设置方法            | 描述                      | 类型                       |
| -------------------- | ----------------- | ------------------------ | ------------------------- |
| bucketName  | 构造函数或 set 方法 | 设置标签的对象所在的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | 构造函数或者 set 方法 | 设置标签的对象键，对象键（Key）是对象在存储桶中的唯一标识，详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### 返回结果说明

- 成功：返回 GetObjectTaggingResult，包含对象的标签信息。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

## 删除对象标签

#### 功能说明

用于删除指定对象的已有标签。

#### 方法原型

```java
public DeleteObjectTaggingResult deleteObjectTagging(DeleteObjectTaggingRequest deleteObjectTaggingRequest);
```

#### 请求示例

```java
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
DeleteObjectTaggingRequest deleteObjectTaggingRequest = new DeleteObjectTaggingRequest(bucketName, key);
cosclient.deleteObjectTagging(deleteObjectTaggingRequest);
```

#### 参数说明

| 参数名称   | 描述        | 类型   |
| --------- | ---------- | ------ |
| deleteObjectTaggingRequest | 对象标签删除请求 | DeleteObjectTaggingRequest |

Request 成员说明：

| Request 成员         | 设置方法            | 描述                      | 类型                       |
| -------------------- | ------------------ | ----------------------- | -------------------------- |
| bucketName  | 构造函数或 set 方法 | 设置标签的对象所在的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | 构造函数或者 set 方法 | 设置标签的对象键，对象键（Key）是对象在存储桶中的唯一标识，详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。
