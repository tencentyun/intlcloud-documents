

## 简介

本文档提供关于自定义域名的 API 概览以及 SDK 示例代码。

| API               | 操作名         | 操作描述                   |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain | 设置自定义域名 | 设置存储桶的自定义域名信息 |
| GET Bucket domain | 查询自定义域名 | 查询存储桶的自定义域名信息 |

## 设置自定义域名

#### 功能说明

PUT Bucket domain 用于为存储桶配置自定义域名。

#### 方法原型

```java
public void setBucketDomainConfiguration(String bucketName, BucketDomainConfiguration configuration);
public void setBucketDomainConfiguration(SetBucketDomainConfigurationRequest setBucketDomainConfigurationRequest);
```

#### 请求示例

[//]: # (.cssg-snippet-put-bucket-domain)
```java
// 调用 COS 接口之前必须保证本进程存在一个 COSClient 实例，如果没有则创建
// 详细代码参见对象操作 -> 上传对象 -> 简单操作 -> 创建 COSClient
COSClient cosClient = createCOSClient();
// 存储桶的命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式
String bucketName = "examplebucket-1250000000";

BucketDomainConfiguration bucketDomainConfiguration = new BucketDomainConfiguration();
DomainRule domainRule = new DomainRule();
domainRule.setStatus(DomainRule.ENABLED);
domainRule.setType(DomainRule.REST);
domainRule.setName("qq.com");
domainRule.setForcedReplacement(DomainRule.CNAME);
bucketDomainConfiguration.getDomainRules().add(domainRule);
cosClient.setBucketDomainConfiguration(bucketName, bucketDomainConfiguration);
```

#### 参数说明

| 参数名称                            | 描述                     | 类型                                |
| ----------------------------------- | ------------------------ | ----------------------------------- |
| setBucketDomainConfigurationRequest | 设置存储桶自定义域名请求 | SetBucketDomainConfigurationRequest |

Request 成员说明 ：

| Request 成员  | 设置方法            | 描述                                                         | 类型                      |
| ------------- | ------------------- | ------------------------------------------------------------ | ------------------------- |
| bucketName    | 构造函数或 set 方法 | 设置自定义域名的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String                    |
| configuration | 构造函数或 set 方法 | 存储桶的自定义域名配置                                       | BucketDomainConfiguration |

BucketDomainConfiguration 成员说明:

| 参数名称    | 描述                   | 类型                         |
| ----------- | ---------------------- | ---------------------------- |
| domainRules | 存储桶的自定义域名配置 | List&lt;DomainRule> domainRules |

DomainRule 成员说明：

| 参数名称          | 描述                                      | 类型   |
| ----------------- | ----------------------------------------- | ------ |
| name              | 自定义域名                                | String |
| status            | 域名上线状态，可选值有 ENABLED、DISABLED  | String |
| type              | 绑定的源站类型，可选值有 REST、WEBSITE    | String |
| forcedReplacement | 强制覆盖已存在的配置，可选值有 CNAME、TXT | String |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 返回错误码说明

该请求可能会发生的一些常见的特殊错误如下：

| 状态码                                 | 说明                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | 该域名记录已存在，且请求中没有设置强制覆盖。或者该域名记录不存在，且请求中设置了强制覆盖 |
| HTTP 451 Unavailable For Legal Reasons | 该域名是中国境内域名，并且没有备案                           |

## 查询自定义域名

#### 功能说明

GET Bucket domain 用于查询存储桶的自定义域名信息。

#### 方法原型

```java
public BucketDomainConfiguration getBucketDomainConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-domain)
```java
// 调用 COS 接口之前必须保证本进程存在一个 COSClient 实例，如果没有则创建
// 详细代码参见对象操作 -> 上传对象 -> 简单操作 -> 创建 COSClient
COSClient cosClient = createCOSClient();
// 存储桶的命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式
String bucketName = "examplebucket-1250000000";

BucketDomainConfiguration bucketDomainConfiguration = cosClient.getBucketDomainConfiguration(bucketName);
String domainTxtVerification = bucketDomainConfiguration1.getDomainTxtVerification();
System.out.println(domainTxtVerification);
for (DomainRule rule : bucketDomainConfiguration.getDomainRules()) {
    System.out.println(rule.getName());
    System.out.println(rule.getStatus());
    System.out.println(rule.getType());
    System.out.println(rule.getClass());
}
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | 查询自定义域名的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

- 成功：返回 BucketDomainConfiguration，包含存储桶的自定义域名设置信息。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 返回参数说明

| 参数名称              | 描述                                                         | 类型   |
| --------------------- | ------------------------------------------------------------ | ------ |
| domainTxtVerification | 域名校验信息，该字段是一个 MD5 校验值，原串格式为：`cos[Region][BucketName-APPID][BucketCreateTime]`，其中 Region 为存储桶所在地域，BucketCreateTime 为存储桶 GMT 创建时间 | String |
