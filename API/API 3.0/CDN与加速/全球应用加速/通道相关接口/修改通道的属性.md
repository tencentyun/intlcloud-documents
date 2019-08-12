## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（ModifyProxiesAttribute）用于修改实例的属性（目前只支持修改通道的名称）。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：ModifyProxiesAttribute |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| InstanceIds.N | 否 | Array of String | （旧参数，请切换到ProxyIds）一个或多个待操作的通道ID。 |
| ProxyName | 否 | String | 通道名称。可任意命名，但不得超过30个字符。 |
| ClientToken | 否 | String | 用于保证请求幂等性的字符串。该字符串由客户生成，需保证不同请求之间唯一，最大值不超过64个ASCII字符。若不指定该参数，则无法保证请求的幂等性。<br/>更多详细信息请参阅：如何保证幂等性。 |
| ProxyIds.N | 否 | Array of String | （新参数）一个或多个待操作的通道ID。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 修改通道的属性

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=ModifyProxiesAttribute
&ProxyIds.0=link-11112222
&ProxyIds.1=link-11113333
&ProxyName=test
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "04d1af8f-5c76-4053-acbc-62bdf0541c15"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=ModifyProxiesAttribute)

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
| FailedOperation.ResourceCanNotAccess | 该资源不可访问。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| InvalidParameterValue.ProjectIdNotBelong | 项目不属于该用户。 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| ResourceUnavailable | 资源不可用 |
| UnknownParameter | 未知参数错误 |
