## 1. 接口描述

接口请求域名： cloudaudit.tencentcloudapi.com 。

参数要求：
1、如果IsCreateNewBucket的值存在的话，cosRegion和cosBucketName都是必填参数。
2、如果IsEnableCmqNotify的值是1的话，IsCreateNewQueue、CmqRegion和CmqQueueName都是必填参数。
3、如果IsEnableCmqNotify的值是0的话，IsCreateNewQueue、CmqRegion和CmqQueueName都不能传。
4、如果IsEnableKmsEncry的值是1的话，KmsRegion和KeyId属于必填项

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](https://intl.cloud.tencent.com/document/api/1021/34192)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：CreateAudit。 |
| Version | 是 | String | 公共参数，本接口取值：2019-03-19。 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| AuditName | 是 | String | 跟踪集名称。3-128字符，只能包含 ASCII 编码字母 a-z，A-Z，数字 0-9，下划线 _。 |
| CosBucketName | 是 | String | cos的存储桶名称。仅支持小写英文字母和数字即[a-z，0-9]、中划线“-”及其组合。用户自定义的字符串支持1 - 40个字符。存储桶命名不能以“-”开头或结尾。如果不是新创建的存储桶，云审计不会去校验该存储桶是否真的存在，请谨慎填写，避免日志投递不成功，导致您的数据丢失。 |
| CosRegion | 是 | String | cos地域。目前支持的地域可以使用ListCosEnableRegion来获取。 |
| IsCreateNewBucket | 是 | Integer | 是否创建新的cos存储桶。1：是，0：否。 |
| IsEnableCmqNotify | 是 | Integer | 是否开启cmq消息通知。1：是，0：否。目前仅支持cmq的队列服务。如果开启cmq消息通知服务，云审计会将您的日志内容实时投递到您指定地域的指定队列中。 |
| ReadWriteAttribute | 是 | Integer | 管理事件的读写属性。1：只读，2：只写，3：全部。 |
| CmqQueueName | 否 | String | 队列名称。队列名称是一个不超过64个字符的字符串，必须以字母为首字符，剩余部分可以包含字母、数字和横划线(-)。如果IsEnableCmqNotify值是1的话，此值属于必填字段。如果不是新创建的队列，云审计不会去校验该队列是否真的存在，请谨慎填写，避免日志通知不成功，导致您的数据丢失。 |
| CmqRegion | 否 | String | 队列所在的地域。可以通过ListCmqEnableRegion获取支持的cmq地域。如果IsEnableCmqNotify值是1的话，此值属于必填字段。 |
| IsCreateNewQueue | 否 | Integer | 是否创建新的队列。1：是，0：否。如果IsEnableCmqNotify值是1的话，此值属于必填字段。 |
| IsEnableKmsEncry | 否 | Integer | 是否开启kms加密。1：是，0：否。如果开启KMS加密，数据在投递到cos时，会将数据加密。 |
| KeyId | 否 | String | CMK的全局唯一标识符，如果不是新创建的kms，该值是必填值。可以通过ListKeyAliasByRegion来获取。云审计不会校验KeyId的合法性，请您谨慎填写，避免给您的数据造成损失。 |
| KmsRegion | 否 | String | kms地域。目前支持的地域可以使用ListKmsEnableRegion来获取。必须要和cos的地域保持一致。 |
| LogFilePrefix | 否 | String | 日志文件前缀。3-40个字符，只能包含 ASCII 编码字母 a-z，A-Z，数字 0-9。可以不填，默认以账号ID作为日志前缀。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| IsSuccess | Integer | 是否创建成功。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 创建跟踪集

创建跟踪集

#### 输入示例

```
https://cloudaudit.tencentcloudapi.com/?Action=CreateAudit
&AuditName=auditTest_1
&CmqQueueName=cmq-01
&CmqRegion=sh
&CosBucketName=cos-01
&CosRegion=ap-shanghai
&IsCreateNewBucket=1
&IsCreateNewQueue=1
&IsEnableCmqNotify=1
&LogFilePrefix=akshsb1j
&ReadWriteAttribute=2
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "IsSuccess": 1,
    "RequestId": "e9501707-784a-474c-b524-67ed9d3a6b50"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=CreateAudit)

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
| InternalError.CmqError | 创建cmq时发生异常，可能您准备创建的cmq队列已经存在，也有可能您没有权限或者欠费。 |
| InternalError.CreateAuditError | 创建跟踪集错误，请联系开发人员。 |
| InvalidParameterValue.AuditNameError | 跟踪集名称不符合规则 |
| InvalidParameterValue.CmqRegionError | 云审计目前不支持输入的cmq地域 |
| InvalidParameterValue.CosNameError | 输入的cos存储桶名称不符合规范 |
| InvalidParameterValue.CosRegionError | 云审计目前不支持输入的cos地域 |
| InvalidParameterValue.IsCreateNewBucketError | IsCreateNewBucket的有效取值范围是0和1，0代表不创建新的存储桶，1代表创建新的存储桶。 |
| InvalidParameterValue.IsCreateNewQueueError | IsCreateNewQueue的有效取值范围是0和1，0代表不新创建，1代表新创建。 |
| InvalidParameterValue.IsEnableCmqNotifyError | IsEnableCmqNotify的有效取值范围是0和1，0代表不开启投递cmq,1代表开启cmq投递。 |
| InvalidParameterValue.LogFilePrefixError | 日志前缀格式错误 |
| InvalidParameterValue.QueueNameError | 输入的队列名称不符合规范 |
| InvalidParameterValue.ReadWriteAttributeError | 读写属性值仅支持：1,2,3。1代表只读，2代表只写，3代表全部。 |
| LimitExceeded.OverAmount | 超过跟踪集的最大值 |
| MissingParameter.MissAuditName | 缺少跟踪集名称 |
| MissingParameter.MissCosBucketName | 缺少cos存储桶参数 |
| MissingParameter.MissCosRegion | 缺少cos地域参数 |
| MissingParameter.cmq | IsEnableCmqNotify输入1的话，IsCreateNewQueue、CmqQueueName和CmqRegion都是必须参数。 |
| ResourceInUse.AlreadyExistsSameAudit | 已经存在相同名称的跟踪集 |
| ResourceInUse.AlreadyExistsSameAuditCmqConfig | 已经存在相同cmq投递配置的跟踪集 |
| ResourceInUse.AlreadyExistsSameAuditCosConfig | 已经存在相同cos投递配置的跟踪集 |
| ResourceInUse.CosBucketExists | cos存储桶已经存在 |
