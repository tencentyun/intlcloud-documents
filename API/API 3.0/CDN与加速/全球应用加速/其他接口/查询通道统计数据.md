## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

该接口用于查询监听器统计数据，包括出入带宽，出入包量，并发，丢包和时延数据。支持300, 3600和86400的细粒度，取值为细粒度范围内最大值。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeProxyStatistics |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ProxyId | 是 | String | 通道ID |
| StartTime | 是 | Timestamp | 起始时间(2019-03-25 12:00:00) |
| EndTime | 是 | Timestamp | 结束时间(2019-03-25 12:00:00) |
| MetricNames.N | 是 | Array of String | 统计指标名称列表，支持: 入带宽:InBandwidth, 出带宽:OutBandwidth, 并发:Concurrent, 入包量:InPackets, 出包量:OutPackets, 丢包率:PacketLoss, 延迟:Latency |
| Granularity | 是 | Integer | 监控粒度，目前支持60，300，3600，86400，单位：秒。<br/>当时间范围不超过1天，支持最小粒度60秒；<br/>当时间范围不超过7天，支持最小粒度3600秒；<br/>当时间范围不超过30天，支持最小粒度86400秒。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| StatisticsData | Array of [MetricStatisticsInfo](/document/api/608/37023#MetricStatisticsInfo) | 通道统计数据|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 查询通道统计数据

查询通道统计数据

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=DescribeProxyStatistics
&ProxyId=link-rfgt56hy
&MetricNames.0=Concurrent
&StartTime=2019-03-25 12:00:00
&EndTime=2019-03-26 12:00:00
&Granularity=300
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "StatisticsData": [
      {
        "MetricName": "Concurrent",
        "MetricData": [
          {
            "Time": 1564734780,
            "Data": 2000
          },
          {
            "Time": 1564734720,
            "Data": 2001
          }
        ]
      }
    ],
    "RequestId": "5c680029-66b2-4be8-9630-7bd316ce70dd"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=DescribeProxyStatistics)

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
| FailedOperation.ResourceCanNotAccess | 该资源不可访问。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| UnauthorizedOperation | 未授权操作 |
