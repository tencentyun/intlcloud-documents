## 1. 接口描述

接口请求域名： cloudaudit.tencentcloudapi.com 。

查询跟踪集详情

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](https://intl.cloud.tencent.com/document/api/1021/34192)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeAudit。 |
| Version | 是 | String | 公共参数，本接口取值：2019-03-19。 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| AuditName | 是 | String | 跟踪集名称 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| AuditName | String | 跟踪集名称。|
| AuditStatus | Integer | 跟踪集状态，1：开启，0：停止。|
| CmqQueueName | String | 队列名称。|
| CmqRegion | String | 队列所在地域。|
| CosBucketName | String | cos存储桶名称。|
| CosRegion | String | cos存储桶所在地域。|
| IsEnableCmqNotify | Integer | 是否开启cmq消息通知。1：是，0：否。|
| IsEnableKmsEncry | Integer | 是否开启kms加密。1：是，0：否。如果开启KMS加密，数据在投递到cos时，会将数据加密。|
| KeyId | String | CMK的全局唯一标识符。|
| KmsAlias | String | CMK别名。|
| KmsRegion | String | kms地域。|
| LogFilePrefix | String | 日志前缀。|
| ReadWriteAttribute | Integer | 管理事件读写属性，1：只读，2：只写，3：全部|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询跟踪集详情

查询跟踪集详情

#### 输入示例

```
https://cloudaudit.tencentcloudapi.com/?Action=DescribeAudit
&AuditName=xxxxx_cloudaudit_2
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "AuditName": "xxxxx_cloudaudit_2",
    "CmqQueueName": "xxxxx-cloudaudit-2",
    "CmqRegion": "hk",
    "CosBucketName": "xxxxx-cloudaudit-2",
    "CosRegion": "ap-hongkong",
    "IsEnableCmqNotify": 1,
    "LogFilePrefix": "xxx2312",
    "ReadWriteAttribute": 1,
    "AuditStatus": 1,
    "RequestId": "e23ee347-d011-482a-83fa-12e7d318dd9f"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=DescribeAudit)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](https://intl.cloud.tencent.com/document/api/1021/34195#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError.DescribeAuditError | 查看跟踪集详情错误，请联系开发人员 |
| ResourceNotFound.AuditNotExist | 跟踪集不存在 |
