## 简介

本文档提供关于版本控制的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 设置版本控制 | 设置存储桶的版本控制功能 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 查询版本控制 | 查询存储桶的版本控制信息 |

## 设置版本控制

#### 功能说明

设置指定存储桶的版本控制功能（PUT Bucket versioning）。

#### 方法原型
```java
public void setBucketVersioningConfiguration(SetBucketVersioningConfigurationRequest setBucketVersioningConfigurationRequest)
    throws CosClientException, CosServiceException;
```

#### 参数说明
| 参数名称                                | 描述                                                         | 类型                                    |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| setBucketVersioningConfigurationRequest | 版本控制配置                                                 | SetBucketVersioningConfigurationRequest |


#### 返回结果说明
  - 成功：无返回值。
  - 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

**开启版本控制**

[//]: # ".cssg-snippet-put-bucket-versioning"
```java
String bucketName = "examplebucket-1250000000";
// 开启版本控制
cosClient.setBucketVersioningConfiguration(
        new SetBucketVersioningConfigurationRequest(bucketName,
                new BucketVersioningConfiguration(BucketVersioningConfiguration.ENABLED)));
```

**暂停版本控制**

```java
String bucketName = "examplebucket-1250000000";
// 暂停版本控制
cosClient.setBucketVersioningConfiguration(
new SetBucketVersioningConfigurationRequest(bucketName,
new BucketVersioningConfiguration(BucketVersioningConfiguration.SUSPENDED)));
```

## 查询版本控制

#### 功能说明

查询指定存储桶的版本控制信息（GET Bucket versioning）。

#### 方法原型
```java
// 方法1 传入存储桶名称即可
public BucketVersioningConfiguration getBucketVersioningConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// 方法2 通过GetBucketVersioningConfigurationRequest 获取
public BucketVersioningConfiguration getBucketVersioningConfiguration(
    GetBucketVersioningConfigurationRequest getBucketVersioningConfigurationRequest)
        throws CosClientException, CosServiceException;
```

#### 请求示例

[//]: # ".cssg-snippet-get-bucket-versioning"
```java
String bucketName = "examplebucket-1250000000";
// 获取版本控制
BucketVersioningConfiguration bvc =
        cosClient.getBucketVersioningConfiguration(bucketName);
// 获取版本控制
BucketVersioningConfiguration bvc2 = cosClient.getBucketVersioningConfiguration(
        new GetBucketVersioningConfigurationRequest(bucketName));
```


#### 参数说明

| 参数名称                                | 描述                                                         | 类型                                    |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName                              | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                                  |
| getBucketVersioningConfigurationRequest | 获取版本控制配置请求                                         | GetBucketVersioningConfigurationRequest |


#### 返回结果说明
- 成功：返回存储桶的多版本配置。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。
