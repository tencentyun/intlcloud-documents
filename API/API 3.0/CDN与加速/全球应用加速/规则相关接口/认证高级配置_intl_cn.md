## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（SetAuthentication）用于通道的高级认证配置，包括认证方式选择，以及各种认证方式对应的证书选择。仅支持Version3.0的通道。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：SetAuthentication |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ListenerId | 是 | String | 监听器ID。 |
| Domain | 是 | String | 需要进行高级配置的域名，该域名为监听器下的转发规则的域名。 |
| BasicAuth | 否 | Integer | 基础认证开关，其中：<br/>0，关闭基础认证；<br/>1，开启基础认证。<br/>默认为0。 |
| GaapAuth | 否 | Integer | 通道认证开关，用于源站对Gaap的认证，其中：<br/>0，关闭通道认证；<br/>1，开启通道认证。<br/>默认为0。 |
| RealServerAuth | 否 | Integer | 源站认证开关，用于Gaap对服务器的认证，其中：<br/>0，关闭源站认证；<br/>1，开启源站认证。<br/>默认为0。 |
| BasicAuthConfId | 否 | String | 基础认证配置ID，从证书管理页获取。 |
| GaapCertificateId | 否 | String | 通道SSL证书ID，从证书管理页获取。 |
| RealServerCertificateId | 否 | String | 源站CA证书ID，从证书管理页获取。 |
| RealServerCertificateDomain | 否 | String | 源站证书域名。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 认证高级配置

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=SetAuthentication
&ListenerId=0
&Domain=a.a.com
&BasicAuth=1
&BasicAuthConfId=xxx
&GaapAuth=1
&GaapCertificateId=xxx
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "c7bfcad5-3f20-472f-9afc-13a66faebad8"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=SetAuthentication)

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
| FailedOperation.ActionIsDoing | 操作正在执行中，请勿重复操作。 |
| FailedOperation.ListenerHasTask | 监听器正在操作中，请勿重复操作。 |
| FailedOperation.ListenerStatusError | 监听器当前状态无法支持该操作。 |
| FailedOperation.NotSupportOldVersionProxy | 仅支持Version2.0的通道。 |
| FailedOperation.ProxyVersionNotSupport | 不支持该版本通道。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| InvalidParameterValue.InvalidCertificateId | 证书不可用。 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| ResourceUnavailable | 资源不可用 |
| UnauthorizedOperation | 未授权操作 |
| UnknownParameter | 未知参数错误 |
