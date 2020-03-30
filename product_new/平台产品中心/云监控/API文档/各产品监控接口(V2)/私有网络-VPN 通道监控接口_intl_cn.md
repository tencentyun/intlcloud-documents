## 1. 接口描述

接口：GetMonitorData

接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询私有网络VPN通道监控数据，入参取值如下：

&Namespace=QCE/VPNX

&Instances.N.Dimensions.0.Name=vpnConnId

&Instances.N.Dimensions.0.Value 为 VPN 通道 ID


## 2. 输入参数


以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1输入参数
#### 2.1.1 输入参数总览
| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如：QCE/VPNX |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 EndTime 不能小于 StartTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | vpnConnId | 入参为 VPN 通道ID | String 类型维度名称：vpnConnId |
| Instances.N.Dimensions.0.Value | vpnConnId | 具体的 VPN 通道ID | 具体实例名称，如 vpnx-12345678 |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度（dimension）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标名称 | 含义 | 单位 | 维度 |
| ------------ | ----- | ---- | --------- |
| Outbandwidth | 外网出带宽 | Mbps | vpnConnId |
| Inbandwidth | 外网入带宽 | Mbps | vpnConnId |
| Outpkg | 出包量 | 个/秒 | vpnConnId |
| Inpkg | 入包量 | 个/秒 | vpnConnId |
| Pkgdrop | 丢包率 | 百分比 | vpnConnId |
| Delay | 时延 | 秒 | vpnConnId |



## 3. 输出参数

| 参数名称 | 类型 | 描述 |
| ---------- | --------------------- | ------------------------------------------------------------ |
| MetricName | String | 监控指标 |
| StartTime | Timestamp | 数据点起始时间 |
| EndTime | Timestamp | 数据点结束时间 |
| Period | Integer | 数据统计周期 |
| DataPoints | Array of PointsObject | 监控数据列表 |
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的RequestId |

## 4. 错误码表

| 错误代码 | 错误描述 | 英文描述 |
| -------- | -------------- | ------------------------------------ |
| -502 | 资源不存在 | OperationDenied.SourceNotExists |
| -503 | 请求参数有误 | InvalidParameter |
| -505 | 参数缺失 | InvalidParameter.MissingParameter |
| -507 | 超出限制 | OperationDenied.ExceedLimit |
| -509 | 错误的维度组合 | InvalidParameter.DimensionGroupError |
| -513 | DB 操作失败 | InternalError.DBoperationFail |

## 5. 示例

### 示例1 
拉取某个私有网络 VPN 通道某段时间内统计周期为60秒的外网出带宽监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/VPNX
&MetricName=Outbandwidth
&Period=60
&StartTime=2019-06-11T00:00:00+08:00
&EndTime=2019-06-11T00:05:00+08:00
&Instances.0.Dimensions.0.Name=vpnConnId
&Instances.0.Dimensions.0.Value=vpnx-12345678
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-11 00:00:00",
"EndTime": "2019-06-11 00:05:00",
"Period": 60,
"MetricName": "Outbandwidth",
"DataPoints": [
{
"Dimensions": [
{
"Name": "vpnConnId",
"Value": "vpnx-12345678"
}
],
"Timestamps": [
1560182400,
1560182460,
1560182520,
1560182580,
1560182640,
1560182700
],
"Values": [
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "f8f999f9-9778-4678-82f2-cc1445c3356e"
}
}
```
### 示例2 
拉取多个私有网络 VPN 通道某段时间内统计周期为60秒的外网出带宽监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/VPNX
&MetricName=Outbandwidth
&Period=60
&StartTime=2019-06-11T00:00:00+08:00
&EndTime=2019-06-11T00:05:00+08:00
&Instances.0.Dimensions.0.Name=vpnConnId
&Instances.0.Dimensions.0.Value=vpnx-12345678
&Instances.1.Dimensions.0.Name=vpnConnId
&Instances.1.Dimensions.0.Value=vpnx-123456789
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-11 00:00:00",
"EndTime": "2019-06-11 00:05:00",
"Period": 60,
"MetricName": "Outbandwidth",
"DataPoints": [
{
"Dimensions": [
{
"Name": "vpnConnId",
"Value": "vpnx-12345678"
}
],
"Timestamps": [
1560182400,
1560182460,
1560182520,
1560182580,
1560182640,
1560182700
],
"Values": [
0,
0,
0,
0,
0,
0
]
},
{
"Dimensions": [
{
"Name": "vpnConnId",
"Value": "vpnx-123456789"
}
],
"Timestamps": [
1560182400,
1560182460,
1560182520,
1560182580,
1560182640,
1560182700
],
"Values": [
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "f8f999f9-9778-4678-82f2-cc1445c3356e"
}
}
```