## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（InquiryPriceCreateProxy）用于创建加速通道询价。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：InquiryPriceCreateProxy |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| AccessRegion | 是 | String | 加速区域名称。 |
| Bandwidth | 是 | Integer | 通道带宽上限，单位：Mbps。 |
| DestRegion | 否 | String | （旧参数，请切换到RealServerRegion）源站区域名称。 |
| Concurrency | 否 | Integer | （旧参数，请切换到Concurrent）通道并发量上限，表示同时在线的连接数，单位：万。 |
| RealServerRegion | 否 | String | （新参数）源站区域名称。 |
| Concurrent | 否 | Integer | （新参数）通道并发量上限，表示同时在线的连接数，单位：万。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| ProxyDailyPrice | Float | 通道基础费用价格，单位：元/天。|
| BandwidthUnitPrice | Array of [BandwidthPriceGradient](/document/api/608/37023#BandwidthPriceGradient) | 通道带宽费用梯度价格。|
| DiscountProxyDailyPrice | Float | 通道基础费用折扣价格，单位：元/天。|
| Currency | String | 价格使用的货币，支持人民币，美元等。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 创建加速通道询价

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=InquiryPriceCreateProxy
&AccessRegion=EastChina
&RealServerRegion=SouthChina
&Bandwidth=10
&Concurrency=2
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "ProxyDailyPrice": 80.64,
    "DiscountProxyDailyPrice": 56.84,
    "Currency": "CNY",
    "BandwidthUnitPrice": [
      {
        "BandwidthRange": [
          0,
          20
        ],
        "BandwidthUnitPrice": 130
      },
      {
        "BandwidthRange": [
          20,
          100
        ],
        "BandwidthUnitPrice": 90
      },
      {
        "BandwidthRange": [
          100,
          500
        ],
        "BandwidthUnitPrice": 70
      },
      {
        "BandwidthRange": [
          500,
          2000
        ],
        "BandwidthUnitPrice": 60
      },
      {
        "BandwidthRange": [
          2000,
          -1
        ],
        "BandwidthUnitPrice": 50
      }
    ],
    "RequestId": "81370460-5826-4c6f-a864-9b825a4a04b9"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=InquiryPriceCreateProxy)

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
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| InvalidParameterValue.InvalidBandwidth | 带宽值不在可选范围内。 |
| InvalidParameterValue.InvalidConcurrency | 并发量值不在可选范围内。 |
| InvalidParameterValue.UnknownAccessRegion | 未知或无权限访问的加速区域。 |
| InvalidParameterValue.UnknownDestRegion | 未知或无权限访问的源站区域。 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| ResourceUnavailable | 资源不可用 |
| UnauthorizedOperation | 未授权操作 |
| UnknownParameter | 未知参数错误 |
