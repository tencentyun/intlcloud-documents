## 1. 接口描述

接口：GetMonitorData
接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 
接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。
若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。
查询 API 网关产品监控数据，入参取值如下：
QCE/APIGATEWAY 支持以下几种维度组合的查询方式，入参取值如下：

### 1.1 环境维度，入参取值

&Namespace=QCE/APIGATEWAY
&Instances.N.Dimensions.0.Name=serviceId
&Instances.N.Dimensions.0.Value=serviceId 的值
&Instances.N.Dimensions.1.Name=environmentName
&Instances.N.Dimensions.1.Value=为环境名

### 1.2 API 维度，入参取值

&Namespace=QCE/APIGATEWAY
&Instances.N.Dimensions.0.Name=serviceId
&Instances.N.Dimensions.0.Value=serviceId 的值
&Instances.N.Dimensions.1.Name=environmentName
&Instances.N.Dimensions.1.Value=为环境名
&Instances.N.Dimensions.2.Name=apiid
&Instances.N.Dimensions.2.Value= 为 API 的 ID

### 1.3 密钥对维度，入参取值（需要开启白名单）

&Namespace=QCE/APIGATEWAY
&Instances.N.Dimensions.0.Name=serviceId
&Instances.N.Dimensions.0.Value=serviceId 的值
&Instances.N.Dimensions.1.Name=environmentName
&Instances.N.Dimensions.1.Value=为环境名
&Instances.N.Dimensions.2.Name=key
&Instances.N.Dimensions.2.Value=为密钥对的 secretid

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1 输入参数

#### 2.1.1 输入参数总览

| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如： QCE/APIGATEWAY |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间， endTime 不能小于 startTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------------------- | --------------- | -------------------- | ---------------------------------------- |
| &Instances.N.Dimensions.0.Name | serviceId | API 网关服务 ID | String 类型维度名称：serviceId |
| &Instances.N.Dimensions.0.Value | serviceId | API 网关服务 ID | 具体 IP 地址 |
| &Instances.N.Dimensions.1.Name | environmentName | 环境名称 | String 类型维度名称：environmentName |
| &Instances.N.Dimensions.1.Value | environmentName | 环境名称 | 环境名称，release、test、repub |
| &Instances.N.Dimensions.2.Name | apiid/key | APIid 或者密钥对 | String类型维度名称： apiid/key |
| &Instances.N.Dimensions.2.Value | apiid/secretid | APIid 或者密钥对公钥 | 具体的 apiid 或者 secretid（维度为 key） |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度 (dimension) 可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882 接口获取每个指标支持的统计粒度及维度信息。

| 指标名称（metricName） | 含义 | 单位 |
| ---------------------- | -------------- | ---- |
| ResponseTime | 响应时间数据 | ms |
| ClientError | 前台错误数 | 次 |
| ServerError | 后台错误数 | 次 |
| ConcurrentConnections | 并发链接数 | 条 |
| OutTraffic | 七层外网出流量 | MB |
| NumOfReq | 请求次数 | 次 |
| ApiServerError404 | 后台404错误数 | 次 |
| ApiServerError502 | 后台502错误数 | 次 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
| ---------- | --------------------- | ------------------------------------------------------------ |
| MetricName | String | 监控指标 |
| StartTime | Timestamp | 数据点起始时间 |
| EndTime | Timestamp | 数据点结束时间 |
| Period | Integer | 数据统计周期 |
| DataPoints | Array of PointsObject | 监控数据列表 |
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId |

## 4. 错误码表

| 错误代码 | 错误描述 | 英文描述 |
| -------- | -------------- | ------------------------------------ |
| -502 | 资源不存在 | OperationDenied.SourceNotExists |
| -503 | 请求参数有误 | InvalidParameter |
| -505 | 参数缺失 | InvalidParameter.MissingParameter |
| -507 | 超出限制 | OperationDenied.ExceedLimit |
| -509 | 错误的维度组合 | InvalidParameter.DimensionGroupError |
| -513 | DB操作失败 | InternalError.DBoperationFail |

## 5. 示例

#### 示例1 

拉取某个 API 网关某段时间内统计周期为60秒的响应时间数据监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/APIGATEWAY
&MetricName=ResponseTime
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=serviceId
&Instances.0.Dimensions.0.Value=service-12345jy
&Instances.0.Dimensions.1.Name=environmentName
&Instances.0.Dimensions.1.Value=release
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-29 15:00:00",
"EndTime": "2019-05-29 15:05:00",
"Period": 60,
"MetricName": "ResponseTime",
"DataPoints": [
{
"Dimensions": [
{
"Name": "environmentName",
"Value": "release"
},
{
"Name": "serviceId",
"Value": "service-12345jy"
}
],
"Timestamps": [
1559113200,
1559113260,
1559113320,
1559113380,
1559113440,
1559113500
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
"RequestId": "ba03fcf5-1dc9-483d-9b6b-86d6cb49be44"
}
}
```

#### 示例2

拉取多个 API 网关某段时间内统计周期为60秒的响应时间数据监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/APIGATEWAY
&MetricName=ResponseTime
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=serviceId
&Instances.0.Dimensions.0.Value=service-12345jy
&Instances.0.Dimensions.1.Name=environmentName
&Instances.0.Dimensions.1.Value=release1
&Instances.1.Dimensions.0.Name=serviceId
&Instances.1.Dimensions.0.Value=service-12345cd
&Instances.1.Dimensions.0.Name=environmentName
&Instances.1.Dimensions.0.Value=release2
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-29 15:00:00",
"EndTime": "2019-05-29 15:05:00",
"Period": 60,
"MetricName": "ResponseTime",
"DataPoints": [
{
"Dimensions": [
{
"Name": "environmentName",
"Value": "release1"
},
{
"Name": "serviceId",
"Value": "service-12345jy"
}
],
"Timestamps": [
1559113200,
1559113260,
1559113320,
1559113380,
1559113440,
1559113500
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
"Name": "environmentName",
"Value": "release2"
},
{
"Name": "serviceId",
"Value": "service-12345cd"
}
],
"Timestamps": [
1559113200,
1559113260,
1559113320,
1559113380,
1559113440,
1559113500
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
"RequestId": "4edabba1-69f1-471b-ab04-695aeb23dc7a"
}
}
```