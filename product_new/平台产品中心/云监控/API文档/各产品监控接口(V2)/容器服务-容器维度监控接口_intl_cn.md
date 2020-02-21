## 1. 接口描述

接口：GetMonitorData

接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询容器服务容器维度监控数据，入参取值如下：

&Namespace=QCE/DOCKER

&Instances.N.Dimensions.0.Name=clusterId

&Instances.N.Dimensions.0.Value 为集群 ID


## 2. 输入参数


以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1 输入参数
#### 2.1.1 输入参数总览
| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如：QCE/DOCKER |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 endTime 不能小于 startTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | clusterId | 为集群 ID | String 类型维度名称：clusterId |
| Instances.N.Dimensions.0.Value | clusterId | 具体的集群 ID，查询集群列表接口中返回的clusterId（集群的ID）字段 | 具体实例名称，如 cls-xxxxx |
| Instances.N.Dimensions.1.Name | serviceName | 为服务名称 | String类型维度名称：serviceName |
| Instances.N.Dimensions.1.Value | serviceName | 具体的集服务名称，查询服务列表接口中返回的 serviceName（服务名）字段 | 具体实例名称，如 test |
| Instances.N.Dimensions.2.Name | namespace | 为命名空间名称 | String类型维度名称：namespace |
| Instances.N.Dimensions.2.Value | namespace | 具体的空间名称，查询服务列表接口中返回的 namespace（命名空间）字段 | 具体实例名称，如 default |
| Instances.N.Dimensions.3.Name | podName | 为实例名称 | String类型维度名称：podName |
| Instances.N.Dimensions.3.Value | podName | 具体的实例名称，查询服务实例列表接口中返回的 name（实例名称）字段 | 具体实例名称，如 test-3488000495-nj6s9 |
| Instances.N.Dimensions.4.Name | containerId | 为实例名称 | String类型维度名称：containerId |
| Instances.N.Dimensions.4.Value | containerId | 具体的实例名称，查询服务实例列表接口中返回的 containerId（容器 ID）字段。注意：容器 ID 只取开头12位即可 | 具体实例名称，如01c5509d2b39 |


### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度（dimension）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 监控项 | 指标名称 | 单位 | 说明 |
| ------------------ | ------------------------------- | ----- | --------------- |
| 容器 CPU 使用情况 | ContainerCpuUsed | 核 | 容器 CPU 使用量 |
| 容器 CPU 使用率（占 主机） | ContainerCpuUsageForNode | % | 容器 CPU 使用占主机 |
| 容器 CPU 使用率（占Request） | ContainerCpuUsageForRequest | % | 容器 CPU 使用占Request |
| 容器 CPU 使用率（占 Limit） | ContainerCpuUsageForLimit | % | 容器 CPU 使用占 Limit |
| 容器内存使用情况 | ContainerMemUsed | MiB | 容器内存使用量 |
| 容器内存使用率（占主机） | ContainerMemUsageForNode | % | 容器内存使用占主机 |
| 容器内存使用率（占 Request） | ContainerMemUsageForRequest | % | 容器内存使用占 Request |
| 容器内存使用率（占 Limit） | ContainerMemUsageForLimit | % | 容器内存使用占 Limit |
| 容器磁盘读流量 | ContainerDiskReadTraffic | KB/s | 容器对磁盘读流量 |
| 容器磁盘写流量 | ContainerDiskWriteTraffic | KB/s | 容器对磁盘写流量 |
| 容器磁盘读 IOPS | ContainerDiskRead | Count | 容器对磁盘读 IOPS |
| 容器磁盘写 IOPS | ContainerDiskWrite | Count | 容器对磁盘写 IOPS |



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
拉取某个容器服务容器维度某段时间内统计周期为60秒的容器 CPU 使用情况监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/DOCKER
&MetricName=ContainerCpuUsed
&Period=60
&StartTime=2019-06-17T16:35:00+08:00
&EndTime=2019-06-17T16:40:00+08:00
&Instances.0.Dimensions.0.Name=clusterId
&Instances.0.Dimensions.0.Value=cls-12345
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=default
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=monitor
&Instances.0.Dimensions.3.Name=podName
&Instances.0.Dimensions.3.Value=monitor-68b6db4956-12345
&Instances.0.Dimensions.4.Name=containerId
&Instances.0.Dimensions.4.Value=abcd1234efg
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-17 16:35:00",
"EndTime": "2019-06-17 16:40:00",
"Period": 60,
"MetricName": "ContainerCpuUsed",
"DataPoints": [
{
"Dimensions": [
{
"Name": "clusterId",
"Value": "cls-12345"
},
{
"Name": "containerId",
"Value": "abcd1234efg"
},
{
"Name": "namespace",
"Value": "default"
},
{
"Name": "podName",
"Value": "monitor-68b6db4956-12345"
},
{
"Name": "serviceName",
"Value": "monitor"
}
],
"Timestamps": [
1560760500,
1560760560,
1560760620,
1560760680,
1560760740,
1560760800
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
"RequestId": "3a0008c9-ecc6-48aa-9033-8f37144cc816"
}
}
```
### 示例2 拉取多个容器服务容器维度容器 CPU 使用情况监控数据示例
拉取多个容器服务容器维度某段时间内统计周期为60秒的容器 CPU 使用情况监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/BLOCK_STORAGE
&MetricName=DiskUtil
&Period=60
&StartTime=2019-06-17T16:35:00+08:00
&EndTime=2019-06-17T16:40:00+08:00
&Instances.0.Dimensions.0.Name=clusterId
&Instances.0.Dimensions.0.Value=cls-12345
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=default
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=monitor
&Instances.0.Dimensions.3.Name=podName
&Instances.0.Dimensions.3.Value=monitor-68b6db4956-12345
&Instances.0.Dimensions.4.Name=containerId
&Instances.0.Dimensions.4.Value=abcd1234efg
&Instances.1.Dimensions.0.Name=clusterId
&Instances.1.Dimensions.0.Value=cls-123456
&Instances.1.Dimensions.1.Name=namespace
&Instances.1.Dimensions.1.Value=default
&Instances.1.Dimensions.2.Name=serviceName
&Instances.1.Dimensions.2.Value=monitor
&Instances.1.Dimensions.3.Name=podName
&Instances.1.Dimensions.3.Value=monitor-68b6db4956-12345
&Instances.1.Dimensions.4.Name=containerId
&Instances.1.Dimensions.4.Value=abcd1234efg
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-17 16:35:00",
"EndTime": "2019-06-17 16:40:00",
"Period": 60,
"MetricName": "ContainerCpuUsed",
"DataPoints": [
{
"Dimensions": [
{
"Name": "clusterId",
"Value": "cls-12345"
},
{
"Name": "containerId",
"Value": "abcd1234efg"
},
{
"Name": "namespace",
"Value": "default"
},
{
"Name": "podName",
"Value": "monitor-68b6db4956-12345"
},
{
"Name": "serviceName",
"Value": "monitor"
}
],
"Timestamps": [
1560760500,
1560760560,
1560760620,
1560760680,
1560760740,
1560760800
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
"Name": "clusterId",
"Value": "cls-123456"
},
{
"Name": "containerId",
"Value": "abcd1234efg"
},
{
"Name": "namespace",
"Value": "default"
},
{
"Name": "podName",
"Value": "monitor-68b6db4956-12345"
},
{
"Name": "serviceName",
"Value": "monitor"
}
],
"Timestamps": [
1560760500,
1560760560,
1560760620,
1560760680,
1560760740,
1560760800
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
"RequestId": "3a0008c9-ecc6-48aa-9033-8f37144cc816"
}
}
```