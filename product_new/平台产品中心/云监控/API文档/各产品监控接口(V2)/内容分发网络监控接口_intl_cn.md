## 1. 接口描述

接口：GetMonitorData

接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询内容分发网络监控数据，入参取值如下：

&Namespace= QCE/CDN

&Instances.N.Dimensions.0.Name=projectId

&Instances.N.Dimensions.0.Value 为项目 ID

&Instances.N.Dimensions.1.Name=domain

&Instances.N.Dimensions.1.Value 为域名


## 2. 输入参数


以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1输入参数
#### 2.1.1 输入参数总览
| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如： |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 endTime 不能小于 startTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------ | --------- | ---- | ---------------------- |
| Instances.N.Dimensions.0.Name | projectId | 项目 | String 类型维度名称：projectId |
| Instances.N.Dimensions.0.Value | projectId | 项目 | 具体项目 ID，如1 |
| Instances.N.Dimensions.0.Name | domain | 域名 | String 类型维度名称：domain |
| Instances.N.Dimensions.0.Value | domain | 域名 | 具体域名，如`www.qq.com` |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度（dimension）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标名称（metricName） | 含义 | 单位 |
| ---------------- | ---- | ---- |
| Bandwidth | 带宽 | Bps |
| Requests | 请求数 | 个 |



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
拉取某个内容分发网络某段时间内统计周期为60秒的带宽监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/CDN
&MetricName=Bandwidth
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=projectId
&Instances.0.Dimensions.0.Value=0
&Instances.0.Dimensions.1.Name=domain
&Instances.0.Dimensions.1.Value=www.tencent.com
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-04 00:00:00",
"EndTime": "2019-06-04 00:05:00",
"Period": 60,
"MetricName": "Bandwidth",
"DataPoints": [
{
"Dimensions": [
{
"Name": "domain",
"Value": "www.tencent.com"
},
{
"Name": "projectId",
"Value": "0"
}
],
"Timestamps": [
1559577600,
1559577660,
1559577720,
1559577780,
1559577840,
1559577900
],
"Values": [
0.024,
0.022,
0.027,
0.024,
0.025,
0.025
]
}
],
"RequestId": "c36ea090-ebd9-4176-a88f-f88d6795e4f2"
}
}
```
### 示例2
拉取多个内容分发网络某段时间内统计周期为60秒的带宽监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/BLOCK_STORAGE
&MetricName=DiskUtil
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=projectId
&Instances.0.Dimensions.0.Value=0
&Instances.0.Dimensions.1.Name=domain
&Instances.0.Dimensions.1.Value=www.tencent.com
&Instances.1.Dimensions.0.Name=projectId
&Instances.1.Dimensions.0.Value=0
&Instances.1.Dimensions.1.Name=domain
&Instances.1.Dimensions.1.Value=www.qcloud.com
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-04 00:00:00",
"EndTime": "2019-06-04 00:05:00",
"Period": 60,
"MetricName": "Bandwidth",
"DataPoints": [
{
"Dimensions": [
{
"Name": "domain",
"Value": "www.tencent.com"
},
{
"Name": "projectId",
"Value": "0"
}
],
"Timestamps": [
1559577600,
1559577660,
1559577720,
1559577780,
1559577840,
1559577900
],
"Values": [
0.024,
0.022,
0.027,
0.024,
0.025,
0.025
]
},
{
"Dimensions": [
{
"Name": "domain",
"Value": "www.qcloud.com"
},
{
"Name": "projectId",
"Value": "0"
}
],
"Timestamps": [
1559577600,
1559577660,
1559577720,
1559577780,
1559577840,
1559577900
],
"Values": [
0.024,
0.022,
0.027,
0.024,
0.025,
0.025
]
}
],
"RequestId": "c36ea090-ebd9-4176-a88f-f88d6795e4f2"
}
}
```