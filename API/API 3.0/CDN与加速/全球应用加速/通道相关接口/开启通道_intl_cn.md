## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

该接口（OpenProxies）用于开启一条或者多条通道。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：OpenProxies |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| InstanceIds.N | 否 | Array of String | （旧参数，请切换到ProxyIds）通道的实例ID列表。 |
| ClientToken | 否 | String | 用于保证请求幂等性的字符串。该字符串由客户生成，需保证不同请求之间唯一，最大值不超过64个ASCII字符。若不指定该参数，则无法保证请求的幂等性。<br/>更多详细信息请参阅：如何保证幂等性。 |
| ProxyIds.N | 否 | Array of String | （新参数）通道的实例ID列表。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| InvalidStatusInstanceSet | Array of String | 非关闭状态下的通道实例ID列表，不可开启。|
| OperationFailedInstanceSet | Array of String | 开启操作失败的通道实例ID列表。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 开启通道

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=OpenProxies
&ProxyIds.0=link-11112222
&ProxyIds.1=link-11113333
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "OperationFailedInstanceSet": [],
    "RequestId": "7daaa62c-7c4b-40d9-a22e-90de42bde58d",
    "InvalidStatusInstanceSet": []
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=OpenProxies)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/608/36938#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| FailedOperation | 操作失败 |
| FailedOperation.AccountBalanceInsufficient | 账户余额不足，无法创建该通道。 |
| FailedOperation.DuplicatedRequest | 重复的请求，请检查ClientToken的值。 |
| FailedOperation.NotSupportOldVersionProxy | 仅支持Version2.0的通道。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| ResourceUnavailable | 资源不可用 |
| UnknownParameter | 未知参数错误 |
