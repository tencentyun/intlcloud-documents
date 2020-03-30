## 1. 接口描述

接口：GetMonitorData

接口请求域名： `monitor.tencentcloudapi.com`

负载均衡（Cloud Load Balancer）是对多台云服务器进行流量分发的服务。具体介绍请参考 负载均衡简介 页面。
当前负载均衡支持四种命名空间 QCE/LB_PUBLIC、QCE/LB_PRIVATE、QCE/LB_RS_PRIVATE 和 QCE/LOADBALANCE。


QCE/LB_PUBLIC：公网负载均衡命名空间，包括负载均衡维度和后端机器维度。

QCE/LB_PRIVATE：内网负载均衡命名空间，包括负载均衡维度监控数据。

QCE/LB_RS_PRIVATE：内网负载均衡命名空间，包括后端服务器维度的监控数据。 

QCE/LOADBALANCE：负载均衡七层数据空间。


接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询公网负载均衡监控数据，是公网负载均衡对应的命名空间，您可以在此空间查询到公网负载均衡的所有监控数据。
支持以下4种维度组合的查询方式，四种入参取值如下：

### 1.1 公网负载均衡维度，入参取值如下：
&Namespace: QCE/LB_PUBLIC

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value 为 IP 地址


### 1.2 公网负载均衡端口维度，入参取值

&Namespace: QCE/LB_PUBLIC

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value 为 IP 地址

&Instances.N.Dimensions.1.Name=loadBalancerPort

&Instances.N.Dimensions.1.Value 为端口号

&Instances.N.Dimensions.2.Name=protocol

&Instances.N.Dimensions.2.Value 为协议类型


### 1.3 公网负载均衡后端服务器维度，入参取值

&Namespace: QCE/LB_PUBLIC

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value 为 IP 地址

&Instances.N.Dimensions.1.Name=loadBalancerPort

&Instances.N.Dimensions.1.Value 为端口号

&Instances.N.Dimensions.2.Name=protocol

&Instances.N.Dimensions.2.Value 为协议类型

&Instances.N.Dimensions.3.Name= vpcId

&Instances.N.Dimensions.3.Value 为负载均衡所在私有网络的 ID

&Instances.N.Dimensions.4.Name=lanIp

&Instances.N.Dimensions.4.Value 为负载均衡绑定机器的 IP




### 1.4 公网负载均衡后端服务器端口维度，入参取值

&Namespace: QCE/LB_PUBLIC

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value为 IP 地址

&Instances.N.Dimensions.1.Name=loadBalancerPort

&Instances.N.Dimensions.1.Value 为端口号

&Instances.N.Dimensions.2.Name=protocol

&Instances.N.Dimensions.2.Value 为协议类型

&Instances.N.Dimensions.3.Name=vpcId

&Instances.N.Dimensions.3.Value 为负载均衡所在私有网络的 ID

&Instances.N.Dimensions.4.Name=lanIp

&Instances.N.Dimensions.4.Value=为负载均衡绑定机器的 IP

&Instances.N.Dimensions.5.Name=port

&Instances.N.Dimensions.5.Value 为负载均衡绑定机器的端口号


## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共请求参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1 输入参数

#### 2.1.1 输入参数总览

| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如：QCE/LB_PUBLIC |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 EndTime 不能小于 StartTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| &Instances.N.Dimensions.0.name | vip | 负载均衡 VIP | String类型维度名称：vip |
| &Instances.N.Dimensions.0.value | vip | 负载均衡 VIP | 具体ip地址，如111.111.111.11 |
| &Instances.N.Dimensions.1.name | loadBalancerPort | 负载均衡端口 | String类型维度名称：loadBalancerPort |
| &Instances.N.Dimensions.1.value | loadBalancerPort | 负载均衡端口 | 具体端口号，如80 |
| &Instances.N.Dimensions.2.name | protocol | 协议 | String类型维度名称：protocol |
| &Instances.N.Dimensions.2.value | protocol | 协议 | string类型，如http |
| &Instances.N.Dimensions.3.name | vpcId | 负载均衡所在私有网络的 ID | String类型维度名称：vpcId |
| &Instances.N.Dimensions.3.value | vpcId | 负载均衡所在私有网络的 ID | 具体私有网络 ID，如1111 |
| &Instances.N.Dimensions.4.name | lanIp | 负载均衡绑定机器的 IP | String类型维度名称：lanIp |
| &Instances.N.Dimensions.4.value | lanIp | 负载均衡绑定机器的 IP | 具体ip地址，如111.222.111.22 |
| &Instances.N.Dimensions.5.name | port | 负载均衡绑定机器的端口号 | String类型维度名称：port |
| &Instances.N.Dimensions.5.value | port | 负载均衡绑定机器的端口号 | 具体端口号，如80 |

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
拉取某个公网负载均衡某段时间内统计周期为60秒的入流量监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/LB_PUBLIC
&MetricName=Intraffic
&Period=60
&StartTime=2019-05-20T16:40:00+08:00
&EndTime=2019-05-20T16:45:00+08:00
&Instances.0.Dimensions.0.Name=vip
&Instances.0.Dimensions.0.Value=111.111.111.11
&Instances.0.Dimensions.1.Name=loadBalancerPort
&Instances.0.Dimensions.1.Value=8088
&Instances.0.Dimensions.2.Name=protocol
&Instances.0.Dimensions.2.Value=http
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-20 16:40:00",
"EndTime": "2019-05-20 16:45:00",
"Period": 60,
"MetricName": "Intraffic",
"DataPoints": [
{
"Dimensions": [
{
"Name": "loadBalancerPort",
"Value": "8088"
},
{
"Name": "protocol",
"Value": "http"
},
{
"Name": "vip",
"Value": "111.111.111.11"
}
],
"Timestamps": [
1558341600,
1558341660,
1558341720,
1558341780,
1558341840,
1558341900
],
"Values": [
12,
34,
23,
45,
31,
24
]
}
],
"RequestId": "b3f5d456-643d-404d-8edb-12345678910"
}
}

```

### 示例2 
拉取多个公网负载均衡某段时间内统计周期为60秒的入流量监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/LB_PUBLIC
&MetricName=Intraffic
&Period=60
&StartTime=2019-05-20T16:40:00+08:00
&EndTime=2019-05-20T16:45:00+08:00
&Instances.0.Dimensions.0.Name=vip
&Instances.0.Dimensions.0.Value=111.111.111.11
&Instances.0.Dimensions.1.Name=loadBalancerPort
&Instances.0.Dimensions.1.Value=8088
&Instances.0.Dimensions.2.Name=protocol
&Instances.0.Dimensions.2.Value=http
&Instances.1.Dimensions.0.Name=vip
&Instances.1.Dimensions.0.Value=222.222.222.2
&Instances.1.Dimensions.1.Name=loadBalancerPort
&Instances.1.Dimensions.1.Value=8088
&Instances.1.Dimensions.2.Name=protocol
&Instances.1.Dimensions.2.Value=http
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-20 16:40:00",
"EndTime": "2019-05-20 16:45:00",
"Period": 60,
"MetricName": "Intraffic",
"DataPoints": [
{
"Dimensions": [
{
"Name": "loadBalancerPort",
"Value": "8088"
},
{
"Name": "protocol",
"Value": "http"
},
{
"Name": "vip",
"Value": "111.111.111.11"
}
],
"Timestamps": [
1558341600,
1558341660,
1558341720,
1558341780,
1558341840,
1558341900
],
"Values": [
12,
34,
23,
45,
31,
24
]
},
{
"Dimensions": [
{
"Name": "loadBalancerPort",
"Value": "8088"
},
{
"Name": "protocol",
"Value": "http"
},
{
"Name": "vip",
"Value": "222.222.222.22"
}
],
"Timestamps": [
1558341600,
1558341660,
1558341720,
1558341780,
1558341840,
1558341900
],
"Values": [
12,
34,
23,
45,
31,
24
]
}
],
"RequestId": "b3f5d456-643d-404d-8edb-12345678910"
}
}

```

