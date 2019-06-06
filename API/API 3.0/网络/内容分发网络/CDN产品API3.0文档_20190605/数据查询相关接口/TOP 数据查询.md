## 1. 接口描述

接口请求域名： cdn.tencentcloudapi.com 。

ListTopData 通过入参 Metric 和 Filter 组合不同，可以查询以下排序数据：

+ 依据总流量、总请求数对访问 URL 排序，从大至小返回 TOP 1000 URL
+ 依据总流量、总请求数对客户端省份排序，从大至小返回省份列表
+ 依据总流量、总请求数对客户端运营商排序，从大至小返回运营商列表
+ 依据总流量、峰值带宽、总请求数、平均命中率、2XX/3XX/4XX/5XX 状态码对域名排序，从大至小返回域名列表
+ 依据总回源流量、回源峰值带宽、总回源请求数、平均回源失败率、2XX/3XX/4XX/5XX 回源状态码对域名排序，从大至小返回域名列表

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见[公共请求参数](/document/api/228/30977)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：ListTopData |
| Version | 是 | String | 公共参数，本接口取值：2018-06-06 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| StartTime | 是 | Timestamp | 查询起始日期，如：2018-09-09 00:00:00 |
| EndTime | 是 | Timestamp | 查询结束日期，如：2018-09-10 00:00:00 |
| Metric | 是 | String | 排序对象，支持以下几种形式：<br/>Url：访问 URL 排序，带参数统计，支持的 Filter 为 flux、request（白名单功能）<br/>Path：访问 URL 排序，不带参数统计，支持的 Filter 为 flux、request<br/>District：省份排序，支持的 Filter 为 flux、request<br/>Isp：运营商排序，支持的 Filter 为 flux、request<br/>Host：域名访问数据排序，支持的 Filter 为：flux, request, bandwidth, fluxHitRate, 2XX, 3XX, 4XX, 5XX，具体状态码统计<br/>originHost：域名回源数据排序，支持的 Filter 为 flux， request，bandwidth，origin_2XX，origin_3XX，oringin_4XX，origin_5XX，具体回源状态码统计 |
| Filter | 是 | String | 排序使用的指标名称：<br/>flux：Metric 为 host 时指代访问流量，originHost 时指代回源流量<br/>bandwidth：Metric 为 host 时指代访问带宽，originHost 时指代回源带宽<br/>request：Metric 为 host 时指代访问请求数，originHost 时指代回源请求数<br/>fluxHitRate：平均流量命中率<br/>2XX：访问 2XX 状态码<br/>3XX：访问 3XX 状态码<br/>4XX：访问 4XX 状态码<br/>5XX：访问 5XX 状态码<br/>origin_2XX：回源 2XX 状态码<br/>origin_3XX：回源 3XX 状态码<br/>origin_4XX：回源 4XX 状态码<br/>origin_5XX：回源 5XX 状态码<br/>statusCode：指定访问状态码统计，在 Code 参数中填充指定状态码<br/>OriginStatusCode：指定回源状态码统计，在 Code 参数中填充指定状态码 |
| Domains.N | 否 | Array of String | 指定查询域名列表，最多可一次性查询 30 个加速域名明细 |
| Project | 否 | Integer | 指定要查询的项目 ID，[前往查看项目 ID](https://console.cloud.tencent.com/project)<br/>未填充域名情况下，指定项目查询，若填充了具体域名信息，以域名为主 |
| Detail | 否 | Boolean | 多域名查询时，默认（false)返回所有域名汇总排序结果<br/>Metric 为 Url、Path、District、Isp，Filter 为 flux、reqeust 时，可设置为 true，返回每一个 Domain 的排序数据 |
| Code | 否 | String | Filter 为 statusCode、OriginStatusCode 时，填充指定状态码查询排序结果 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| Data | Array of [TopData](/document/api/228/30987#TopData) | 各个资源的Top 访问数据详情。|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询Top Url访问数据

#### 输入示例

```
https://cdn.tencentcloudapi.com/?Action=ListTopData
&StartTime=2018-09-04 00:00:00
&EndTime=2018-09-04 12:00:00
&Metric=Url
&Filter=flux
&Domains.0=www.test.com
&Domains.1=www.test.com
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "123",
    "Data": [
      {
        "Resource": "www.test1.com",
        "DetailData": [
          {
            "Name": "www.test1.com/1.jpg?abc=123",
            "Value": 13838
          }
        ]
      },
      {
        "Resource": "www.test2.com",
        "DetailData": [
          {
            "Name": "http://www.test2.com/1.jpg?abc=123",
            "Value": 2501
          }
        ]
      }
    ]
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdn&Version=2018-06-06&Action=ListTopData)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见[公共错误码](/document/api/228/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError.CdnDbError | 内部数据错误，请联系腾讯云工程师进一步排查 |
| InternalError.CdnSystemError | 系统错误，请联系腾讯云工程师进一步排查 |
| InvalidParameter.CdnHostInvalidParam | 域名格式不合法，请确认后重试 |
| InvalidParameter.CdnInterfaceError | 内部接口错误，请联系腾讯云工程师进一步排查 |
| InvalidParameter.CdnParamError | 参数错误，请参考文档中示例参数填充 |
| InvalidParameter.CdnStatInvalidDate | 日期不合法，请参考文档中日期示例 |
| InvalidParameter.CdnStatInvalidFilter | 统计维度不合法，请参考文档中统计分析示例。 |
| InvalidParameter.CdnStatInvalidMetric | 统计类型不合法，请参考文档中统计分析示例 |
| InvalidParameter.CdnStatInvalidProjectId | 项目ID错误，请确认后重试 |
| InvalidParameter.CdnStatTooManyDomains | 查询的域名数量超过限制。 |
| LimitExceeded.CdnHostOpTooOften | 域名操作过于频繁。 |
| ResourceNotFound.CdnHostNotExists | 账号下无此域名，请确认后重试 |
| ResourceNotFound.CdnUserNotExists | 未开通CDN服务，请开通后使用此接口 |
| UnauthorizedOperation.CdnAccountUnauthorized | 子账号禁止查询整体数据。 |
| UnauthorizedOperation.CdnUserIsSuspended | 加速服务已停服，请重启加速服务后重试 |
| UnauthorizedOperation.CdnUserNoWhitelist | 非内测白名单用户，无该功能使用权限 |
