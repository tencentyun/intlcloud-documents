## 简介

本文档提供关于存储桶 Referer 白名单或者黑名单的 API 概览以及 SDK 示例代码。

>! 需要 COS Java SDK v5.6.52 及以上版本。
>

| API                                                          | 操作名         | 操作描述                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 设置存储桶 Referer | 设置存储桶 Referer 白名单或者黑名单 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 查询存储桶 Referer | 查询存储桶 Referer 白名单或者黑名单 |

## 设置存储桶 Referer

#### 功能说明

设置指定存储桶的 Referer 白名单或者黑名单（PUT Bucket referer）。

#### 方法原型

```java
public void setBucketRefererConfiguration(String bucketName, BucketRefererConfiguration configuration) throws CosClientException, CosServiceException;

public void setBucketRefererConfiguration(SetBucketRefererConfigurationRequest setBucketRefererConfigurationRequest) throws CosClientException, CosServiceException;
```

#### 请求示例

```java
// 源存储桶名称，需包含 appid
String bucketName = "examplebucket-1250000000";

BucketRefererConfiguration configuration = new BucketRefererConfiguration();

// 启用防盗链
configuration.setStatus(BucketRefererConfiguration.DISABLED);
// 设置防盗链类型为白名单
//configuration.setRefererType(BucketRefererConfiguration.WHITELIST);
// 设置防盗链类型为黑名单 (与白名单二选一)
configuration.setRefererType(BucketRefererConfiguration.BLACKLIST);

// 填写要设置的域名
configuration.addDomain("test.com");
configuration.addDomain("test.1.com");

//（可选）设置是否允许空防盗链访问，缺省就是 DENY
configuration.setEmptyReferConfiguration(BucketRefererConfiguration.DENY);
// configuration.setEmptyReferConfiguration(BucketRefererConfiguration.ALLOW);

cosClient.setBucketRefererConfiguration(bucketName, configuration);
```

#### 参数说明

| 参数名                                   | 参数描述                                                     | 类型                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                                   |
| configuration | 存储桶 Referer 配置                                               | BucketRefererConfiguration |

BucketRefererConfiguration 说明：

| 参数名          | 参数描述                                         | 类型    | 必选 | 方法      |
| -------------- | ----------------------------------------------- | ------ | ---- | -------- |
| Status         | 是否开启防盗链，枚举值：Enabled、Disabled           | String | 是   | setStatus |
| RefererType    | 防盗链类型，枚举值：Black-List、White-List          | String | 是   | setRefererType |
| Domain         | 生效域名，支持带端口和 IP、支持通配符\*, 支持多条        | String | 是   | addDomain |
| EmptyReferConfiguration | 是否允许空 Refer 访问，枚举值： Allow、Deny | String | 否  | setEmptyReferConfiguration |

#### 返回结果说明

  - 成功：无返回值。
  - 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

## 查询存储桶 Referer

#### 功能说明

查询指定存储桶 Referer 白名单或者黑名单（GET Bucket referer）。

#### 方法原型

```java
public BucketRefererConfiguration getBucketRefererConfiguration(String bucketName) throws CosClientException, CosServiceException
```

#### 请求示例

```java
// 源存储桶名称，需包含 appid
String bucketName = "examplebucket-1250000000";

BucketRefererConfiguration configuration = cosClient.getBucketRefererConfiguration(bucketName);

if (configuration == null) {
    System.out.printf("bucket %s does not have referer configuration\n", bucketName);
    return;
}

System.out.printf("status: %s\n", configuration.getStatus());
System.out.printf("referer type: %s\n", configuration.getRefererType());
System.out.printf("empty referer config: %s\n", configuration.getEmptyReferConfiguration());

for (String domain : configuration.getDomainList()) {
    System.out.printf("domain: %s\n", domain);
}
```

#### 参数说明

| 参数名       | 参数描述  | 类型  |
| ----------- | -------- | ---- |
| bucketName  | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                                   |

#### 返回结果说明

- 成功：返回存储桶的 Referer 白名单或者黑名单。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。
