## 1. 接口描述

接口：GetMonitorData

接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

负载均衡（Cloud Load Balancer）是对多台云服务器进行流量分发的服务。具体介绍请参考 负载均衡简介 页面。
当前负载均衡支持三种命名空间 qce/lb_public、qce/lb_private 和 qce/lb_rs_private。

QCE/LB_PUBLIC：公网负载均衡命名空间，包括负载均衡维度和后端机器维度。
QCE/LB_PRIVATE：内网负载均衡命名空间，包括负载均衡维度监控数据。
QCE/LB_RS_PRIVATE：内网负载均衡命名空间，包括后端服务器维度的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

QCE/LB_PRIVATE是内网负载均衡负载均衡维度的命名空间，您可以在此空间查询到内网负载均衡维度相关监控数据。
QCE/LB_PRIVATE支持以下2种维度组合的查询方式，四种入参取值如下：


### 1.1 内网负载均衡维度，入参取值
&Namespace=QCE/LB_PRIVATE

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value为 IP 地址

&Instances.N.Dimensions.1.Name=vpcId

&Instances.N.Dimensions.1.Value为负载均衡所在私有网络的 ID


### 1.2 内网负载均衡端口维度，入参取值
&Namespace=QCE/LB_PRIVATE

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value为 IP 地址

&Instances.N.Dimensions.1.Name=vpcId

&Instances.N.Dimensions.1.Value为负载均衡所在私有网络的 ID

&Instances.N.Dimensions.2.Name=loadBalancerPort

&Instances.N.Dimensions.2.Value为端口号 

&Instances.N.Dimensions.3.Name=protocol

&Instances.N.Dimensions.3.Value为协议类型


## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1 输入参数
#### 2.1.1 输入参数
| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如： QCE/LB_PRIVATE |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 endTime 不能小于 startTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| &Instances.N.Dimensions.0.name | vip | 负载均衡 VIP | String 类型维度名称：vip |
| &Instances.N.Dimensions.0.value | vip | 负载均衡 VIP | 具体 IP 地址，如111.111.111.11 |
| &Instances.N.Dimensions.1.name | vpcId | 负载均衡所在私有网络的 ID | String类型维度名称：vpcId |
| &Instances.N.Dimensions.1.value | vpcId | 负载均衡所在私有网络的 ID | 具体私有网络 ID，如1012345 |
| &Instances.N.Dimensions.2.name | loadBalancerPort | 负载均衡端口 | String 类型维度名称：loadBalancerPort |
| &Instances.N.Dimensions.2.value | loadBalancerPort | 负载均衡端口 | 具体端口号，如80 |
| &Instances.N.Dimensions.3.name | protocol | 协议 | String 类型维度名称：protocol |
| &Instances.N.Dimensions.3.value | protocol | 协议 | string 类型，如 http |



### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度（dimension）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标名称（metricName） | 含义 | 单位 |
| ---------------- | ----- | ---- |
| Connum | 当前连接数 | 个 |
| NewConn | 新增连接数 | 个 |
| Intraffic | 入流量 | Mbps |
| Outtraffic | 出流量 | Mbps |
| Inpkg | 入包量 | 个/s |
| Outpkg | 出包量 | 个/s |



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
| ---- | ------- | ------------------------------------ |
| -502 | 资源不存在 | OperationDenied.SourceNotExists |
| -503 | 请求参数有误 | InvalidParameter |
| -505 | 参数缺失 | InvalidParameter.MissingParameter |
| -507 | 超出限制 | OperationDenied.ExceedLimit |
| -509 | 错误的维度组合 | InvalidParameter.DimensionGroupError |
| -513 | DB操作失败 | InternalError.DBoperationFail |

## 5. 示例

### 示例1 
拉取某个内网负载均衡某段时间内统计周期为60秒的新增连接数监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/LB_PRIVATE
&MetricName=NewConn
&Period=60
&StartTime=2019-05-20T16:01:00+08:00
&EndTime=2018-05-20T16:05:00+08:00
&Instances.0.Dimensions.0.Name=vip
&Instances.0.Dimensions.0.Value=111.111.111.11
&Instances.0.Dimensions.1.Name=vpcId
&Instances.0.Dimensions.1.Value=1012345
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-20 16:01:00",
"EndTime": "2019-05-20 16:05:00",
"Period": 60,
"MetricName": "NewConn",
"DataPoints": [
{
"Dimensions": [
{
"Name": "vip",
"Value": "111.111.111.11"
},
{
"Name": "vpcId",
"Value": "1012345"
}
],
"Timestamps": [
1558339260,
1558339320,
1558339380,
1558339440,
1558339500
],
"Values": [
12,
34,
23,
45,
31
]
}
],
"RequestId": "9a6ede5f-884a-43cb-9aa6-7082f0657509"
}
}
```

### 示例2 
拉取多个内网负载均衡某段时间内统计周期为60秒的新增连接数监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/LB_PRIVATE
&MetricName=NewConn
&Period=60
&StartTime=2019-05-20T16:01:00+08:00
&EndTime=2018-05-20T16:05:00+08:00
&Instances.0.Dimensions.0.Name=vip
&Instances.0.Dimensions.0.Value=111.111.111.11
&Instances.0.Dimensions.1.Name=vpcId
&Instances.0.Dimensions.1.Value=1012345
&Instances.1.Dimensions.0.Name=vip
&Instances.1.Dimensions.0.Value=222.222.222.22
&Instances.1.Dimensions.1.Name=vpcId
&Instances.1.Dimensions.1.Value=10123456
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-20 16:01:00",
"EndTime": "2019-05-20 16:05:00",
"Period": 60,
"MetricName": "NewConn",
"DataPoints": [
{
"Dimensions": [
{
"Name": "vip",
"Value": "111.111.111.11"
},
{
"Name": "vpcId",
"Value": "1012345"
}
],
"Timestamps": [
1558339260,
1558339320,
1558339380,
1558339440,
1558339500
],
"Values": [
12,
34,
23,
45,
31
]
}，
{
"Dimensions": [
{
"Name": "vip",
"Value": "222.222.222.22"
},
{
"Name": "vpcId",
"Value": "10123456"
}
],
"Timestamps": [
1558339260,
1558339320,
1558339380,
1558339440,
1558339500
],
"Values": [
12,
34,
23,
45,
31
]
}
],
"RequestId": "9a6ede5f-884a-43cb-9aa6-7082f0657509"
}
}
```