## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（CreateProxy）用于创建一个指定配置的加速通道。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：CreateProxy |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ProjectId | 是 | Integer | 通道的项目ID。 |
| ProxyName | 是 | String | 通道名称。 |
| AccessRegion | 是 | String | 接入地域。 |
| Bandwidth | 是 | Integer | 通道带宽上限，单位：Mbps。 |
| Concurrent | 是 | Integer | 通道并发量上限，表示同时在线的连接数，单位：万。 |
| RealServerRegion | 否 | String | 源站地域。当GroupId存在时，源站地域为通道组的源站地域,此时可不填该字段。当GroupId不存在时，需要填写该字段 |
| ClientToken | 否 | String | 用于保证请求幂等性的字符串。该字符串由客户生成，需保证不同请求之间唯一，最大值不超过64个ASCII字符。若不指定该参数，则无法保证请求的幂等性。<br/>更多详细信息请参阅：如何保证幂等性。 |
| GroupId | 否 | String | 通道所在的通道组ID，当在通道组中创建通道时必带，否则忽略该字段。 |
| TagSet.N | 否 | Array of [TagPair](/document/api/608/37023#TagPair) | 通道需要添加的标签列表。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| InstanceId | String | 通道的实例ID。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 创建通道

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=CreateProxy
&ProjectId=0
&ProxyName=test
&AccessRegion=SouthChina
&Bandwidth=10
&Concurrent=2
&GroupId=lg-xxxx
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "InstanceId": "link-11112222",
    "RequestId": "c7bfcad5-3f20-472f-9afc-13a66faebad8"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=CreateProxy)

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
| FailedOperation.ProxySellOut | 线路售罄或者资源不足，请提工单申请。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| InvalidParameterValue.InvalidBandwidth | 带宽值不在可选范围内。 |
| InvalidParameterValue.InvalidConcurrency | 并发量值不在可选范围内。 |
| InvalidParameterValue.InvalidTags | 非法标签，该标签不存在或无权限访问。 |
| InvalidParameterValue.ProjectIdNotBelong | 项目不属于该用户。 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| ResourceUnavailable | 资源不可用 |
| UnauthorizedOperation | 未授权操作 |
| UnknownParameter | 未知参数错误 |
