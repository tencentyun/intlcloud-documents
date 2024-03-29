

## 简介

本文档提供关于存储桶标签的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                         |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | 设置存储桶标签 | 为已存在的存储桶设置标签         |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | 查询存储桶标签 | 查询指定存储桶下已有的存储桶标签 |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | 删除存储桶标签 | 删除指定的存储桶标签             |

## 设置存储桶标签

#### 功能说明

PUT Bucket tagging 用于为已存在的存储桶设置标签。

#### 方法原型

```java
public void setBucketTaggingConfiguration(SetBucketTaggingConfigurationRequest setBucketTaggingConfigurationRequest);
public void setBucketTaggingConfiguration(String bucketName, BucketTaggingConfiguration bucketTaggingConfiguration);
```

#### 请求示例

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

#### 参数说明

| 参数名称                             | 描述               | 类型                                 |
| ------------------------------------ | ------------------ | ------------------------------------ |
| setBucketTaggingConfigurationRequest | 存储桶标签设置请求 | SetBucketTaggingConfigurationRequest |

Request 成员说明 ：

| Request 成员         | 设置方法            | 描述                                                         | 类型                       |
| -------------------- | ------------------- | ------------------------------------------------------------ | -------------------------- |
| bucketName           | 构造函数或 set 方法 | 设置标签的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                     |
| taggingConfiguration | 构造函数或 set 方法 | 存储桶的标签配置                                             | BucketTaggingConfiguration |

BucketLoggingConfiguration 成员说明:

| 参数名称 | 描述                 | 类型         |
| -------- | -------------------- | ------------ |
| tagSets  | 存储桶的标签配置集合 | List&lt;TagSet&gt; |

TagSet 成员说明：

| 参数名称 | 描述                                                         | 类型                |
| -------- | ------------------------------------------------------------ | ------------------- |
| tags     | 标签的 Key 和 Value，长度不超过128字节,  Key 和 Value 支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | Map&lt;String, String&gt; |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/30599)。

## 查询存储桶标签

#### 功能说明

GET Bucket tagging 用于查询指定存储桶下已有的存储桶标签。

#### 方法原型

```java
public BucketTaggingConfiguration getBucketTaggingConfiguration(String bucketName);
```

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
BucketTaggingConfiguration bucketTaggingConfiguration = cosclient.getBucketTaggingConfiguration(bucketName);
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | 查询标签的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

- 成功：返回 BucketTaggingConfiguration，包含存储桶的标签设置信息。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/30599)。

## 删除存储桶标签

#### 功能说明

DELETE Bucket tagging 用于删除指定存储桶下已有的存储桶标签。

#### 方法原型

```java
public void deleteBucketTaggingConfiguration(String bucketName);
```

#### 请求示例

[//]: # (.cssg-snippet-delete-bucket-tagging)
```java
String bucketName = "examplebucket-1250000000";
cosclient.deleteBucketTaggingConfiguration(bucketName);
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | 被删除标签的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/30599)。
