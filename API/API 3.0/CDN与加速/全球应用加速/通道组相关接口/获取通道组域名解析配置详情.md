## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（DescribeGroupDomainConfig）用于获取通道组域名解析配置详情。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeGroupDomainConfig |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| GroupId | 是 | String | 通道组ID。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| AccessRegionList | Array of [DomainAccessRegionDict](/document/api/608/37023#DomainAccessRegionDict) | 域名解析就近接入配置列表。|
| DefaultDnsIp | String | 默认访问Ip。|
| GroupId | String | 通道组ID。|
| AccessRegionCount | Integer | 接入地域的配置的总数。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 获取通道组域名解析配置详情

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=DescribeGroupDomainConfig
&GroupId=lg-b7h4d02f
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "DefaultDnsIp": "lg-na2d00jf",
    "AccessRegionCount": 2,
    "RequestId": "74b5f95c-e976-4f78-b2ee-aad49eb844c4",
    "AccessRegionList": [
      {
        "NationCountryInnerList": [
          {
            "NationCountryName": "North China",
            "NationCountryInnerCode": "101001"
          },
          {
            "NationCountryName": "East China",
            "NationCountryInnerCode": "101002"
          },
          {
            "NationCountryName": "South China",
            "NationCountryInnerCode": "101003"
          },
          {
            "NationCountryName": "West China",
            "NationCountryInnerCode": "101004"
          }
        ],
        "ContinentInnerCode": "100000",
        "RegionId": "EastChina",
        "GeographicalZoneInnerCode": "101000",
        "ProxyList": [
          {
            "ProxyId": "link-4lzfc73l"
          }
        ],
        "RegionName": "East China"
      },
      {
        "NationCountryInnerList": [
          {
            "NationCountryName": "Australia",
            "NationCountryInnerCode": "401000"
          },
          {
            "NationCountryName": "New Zealand",
            "NationCountryInnerCode": "401001"
          }
        ],
        "ContinentInnerCode": "400000",
        "RegionId": "SL_Australia",
        "GeographicalZoneInnerCode": "401000",
        "ProxyList": [
          {
            "ProxyId": "link-ozvhjhp1"
          }
        ],
        "RegionName": "Australia (Sydney)"
      }
    ],
    "GroupId": "lg-na2d00jf"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=DescribeGroupDomainConfig)

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
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| ResourceUnavailable | 资源不可用 |
| UnauthorizedOperation | 未授权操作 |
| UnknownParameter | 未知参数错误 |
