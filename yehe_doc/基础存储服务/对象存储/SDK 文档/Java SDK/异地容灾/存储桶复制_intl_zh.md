## 简介

本文档提供关于存储桶复制的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | 设置存储桶复制 | 设置存储桶的存储桶复制规则 |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | 查询存储桶复制 | 查询存储桶的存储桶复制规则 |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | 删除存储桶复制 | 删除存储桶的存储桶复制规则 |

## 设置存储桶复制

#### 功能说明

设置指定存储桶的存储桶复制规则（PUT Bucket replication）。

#### 方法原型

```java
public void setBucketReplicationConfiguration(
        SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest)
                throws CosClientException, CosServiceException;
```

#### 请求示例

[//]: # (.cssg-snippet-put-bucket-replication)
```java
// 源存储桶名称，需包含 appid
String bucketName = "examplebucket-1250000000";

BucketReplicationConfiguration bucketReplicationConfiguration = new BucketReplicationConfiguration();
// 设置发起者身份, 格式为： qcs::cam::uin/<OwnerUin>:uin/<SubUin>
bucketReplicationConfiguration.setRoleName("qcs::cam::uin/100000000001:uin/100000000001");

// 设置目标存储桶和存储类型，QCS 的格式为：qcs::cos:[region]::[bucketname-AppId]
ReplicationDestinationConfig replicationDestinationConfig = new ReplicationDestinationConfig();
replicationDestinationConfig.setBucketQCS("qcs::cos:ap-beijing::destinationbucket-1250000000");
replicationDestinationConfig.setStorageClass(StorageClass.Standard);

// 设置规则状态和前缀
ReplicationRule replicationRule = new ReplicationRule();
replicationRule.setStatus(ReplicationRuleStatus.Enabled);
replicationRule.setPrefix("");
replicationRule.setDestinationConfig(replicationDestinationConfig);
// 添加规则
String ruleId = "replication-to-beijing";
bucketReplicationConfiguration.addRule(replicationRule);

SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest =
        new SetBucketReplicationConfigurationRequest(bucketName, bucketReplicationConfiguration);
cosClient.setBucketReplicationConfiguration(setBucketReplicationConfigurationRequest);
```



#### 参数说明

| 参数名                                   | 参数描述                                                     | 类型                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                                   |
| setBucketReplicationConfigurationRequest | 存储桶复制配置                                               | SetBucketReplicationConfigurationRequest |

#### 返回结果说明

  - 成功：无返回值。
  - 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。


## 查询存储桶复制

#### 功能说明

查询指定存储桶的存储桶复制规则（GET Bucket replication）。

#### 方法原型
```java
// 获取存储桶存储桶复制配置方法1
public BucketReplicationConfiguration getBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// 获取存储桶存储桶复制方法2        
public BucketReplicationConfiguration getBucketReplicationConfiguration(
            GetBucketReplicationConfigurationRequest getBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-replication)
```java
String bucketName = "examplebucket-1250000000";

// 获取存储桶存储桶复制配置方法1
BucketReplicationConfiguration brcfRet = cosClient.getBucketReplicationConfiguration(bucketName);

// 获取存储桶存储桶复制配置方法2
BucketReplicationConfiguration brcfRet2 = cosClient.getBucketReplicationConfiguration(
        new GetBucketReplicationConfigurationRequest(bucketName));
```


#### 参数说明

| 参数名                                   | 参数描述                                                     | 类型                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                                   |
| getBucketReplicationConfigurationRequest | 获取存储桶复制配置请求                                       | GetBucketReplicationConfigurationRequest |

#### 返回结果说明
- 成功：返回存储桶的存储桶复制规则。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。


## 删除存储桶复制

#### 功能说明

删除指定存储桶的存储桶复制规则（DELETE Bucket replication）。

#### 方法原型
```java
// 删除存储桶存储桶复制配置方法1
public void deleteBucketReplicationConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// 删除存储桶存储桶复制方法2        
public void deleteBucketReplicationConfiguration(
            DeleteBucketReplicationConfigurationRequest deleteBucketReplicationConfigurationRequest)
            throws CosClientException, CosServiceException;
```

#### 请求示例

[//]: # (.cssg-snippet-delete-bucket-replication)
```java
String bucketName = "examplebucket-1250000000";

// 删除存储桶存储桶复制配置方法1
cosClient.deleteBucketReplicationConfiguration(bucketName);

// 删除存储桶存储桶复制配置方法2
cosClient.deleteBucketReplicationConfiguration(new DeleteBucketReplicationConfigurationRequest(bucketName));
```


#### 参数说明

| 参数名                                      | 参数描述                                                     | 类型                                        |
| ------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| bucketName                                  | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| deleteBucketReplicationConfigurationRequest | 删除存储桶复制配置请求                                       | DeleteBucketReplicationConfigurationRequest |

#### 返回结果说明

  - 成功：无返回值。
  - 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。
