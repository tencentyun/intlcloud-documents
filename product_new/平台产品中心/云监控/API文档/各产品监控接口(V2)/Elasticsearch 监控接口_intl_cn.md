## 1. 接口描述

接口：GetMonitorData

接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询块存储监控数据，入参取值如下：

&Namespace=QCE/CES

&Instances.N.Dimensions.0.Name=uInstanceId

&Instances.N.Dimensions.0.Value=es-example


## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共请求参数，正式调用时需要加上全部公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1 输入参数

#### 2.1.1输入参数总览

| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如：QCE/CES |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 endTime 不能小于 startTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------------------ | ----------- | ------------ | ------------------------------- |
| Instances.N.Dimensions.0.Name | uInstanceId | ES 实例的 ID | String类型维度名称：uInstanceId |
| Instances.N.Dimensions.0.Value | uInstanceId | ES 实例的 ID | 具体实例名称，如 es-example |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度 （dimension） 可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标名称 | 指标中文名称 | 计算方式 | 指标含义 | 单位 | 统计粒度（period） |
| ------------------------------ | -------------------------- | -------------------------------------------------------- | ------------------------------------ | ------- | ------------------ |
| Status | 集群健康状态 | ES集群在统计周期内的最新值 | 集群健康状态:0:Green,1:Yellow,2:Red | - | 60s、300s |
| DiskUsageAvg | 平均磁盘使用率 | ES集群在统计周期内各节点磁盘使用率的平均值 | ES 集群各节点磁盘使用率的平均值 | % | 60s、300s |
| DiskUsageMax | 最大磁盘使用率 | ES集群在统计周期内各节点磁盘使用率的最大值 | ES集群各节点磁盘使用率的最大值 | % | 60s、300s |
| JvmMemUsageAvg | 平均JVM内存使用率 | ES集群在统计周期内各节点JVM内存使用率的平均值 | ES集群各节点JVM内存使用率的平均值 | % | 60s、300s |
| JvmMemUsageMax | 最大JVM内存使用率 | ES集群在统计周期内各节点JVM内存使用率的最大值 | ES集群各节点JVM内存使用率的最大值 | % | 60s、300s |
| CpuUsageAvg | 平均CPU使用率 | ES集群在统计周期内各节点CPU使用率的平均值 | ES集群各节点CPU使用率的平均值 | % | 60s、300s |
| CpuUsageMax | 最大CPU使用率 | ES集群在统计周期内各节点CPU使用率的最大值 | ES集群各节点CPU使用率的最大值 | % | 60s、300s |
| CpuLoad1minAvg | 集群1分钟CPU平均负载 | ES集群在统计周期内各节点1分钟CPU负载的平均值 | ES集群各节点CPU 1分钟CPU负载的平均值 | - | 60s、300s |
| CpuLoad1minMax | 集群1分钟CPU最大负载 | ES集群在统计周期内各节点1分钟CPU负载的最大值 | ES集群各节点CPU 1分钟负载的最大值 | - | 60s、300s |
| IndexLatencyAvg | 平均写入延迟 | ES集群在统计周期内写入延迟的平均值 | ES集群写入延迟的平均值 | ms | 60s、300s |
| IndexLatencyMax | 最大写入延迟 | ES集群在统计周期内写入延迟的最大值 | ES集群写入延迟的最大值 | ms | 60s、300s |
| SearchLatencyAvg | 平均查询延迟 | ES集群在统计周期内查询延迟的平均值 | ES集群查询延迟的平均值 | ms | 60s、300s |
| SearchLatencyMax | 最大查询延迟 | ES集群在统计周期内查询延迟的最大值 | ES集群查询延迟的最大值 | ms | 60s、300s |
| IndexSpeed | 写入速度 | ES集群单周期内写入速度的平均值 | ES集群每秒完成写入操作次数 | count/s | 60s、300s |
| SearchCompletedSpeed | 查询速度 | ES集群单周期内查询速度的平均值 | ES集群每秒完成查询操作次数 | count/s | 60s、300s |
| BulkRejectedCompletedPercent | bulk拒绝率 | ES集群在统计周期内bulk操作被拒绝次数占bulk总次数的百分比 | bulk操作被拒绝次数占总次数的百分比 | % | 60s、300s |
| SearchRejectedCompletedPercent | 查询拒绝率 | ES集群在统计周期内查询操作被拒绝次数占查询总次数的百分比 | 查询操作被拒绝次数占总次数的百分比 | % | 60s, 300s |
| IndexDocs | 文档总数 | ES集群在统计周期内文档总数的平均值 | ES集群中的文档总数 | count | 60s、300s |
| AutoSnapshotStatus | ES集群自动备份任务执行状态 | ES集群在统计周期内最后一次执行自动备份任务的状态 | ES集群自动备份任务的执行状态 | - | 300s |



## 3. 输出参数

| 参数名称 | 类型 | 描述 |
| ---------- | --------------------- | ------------------------------------------------------------ |
| MetricName | String | 监控指标 |
| StartTime | Timestamp | 数据点起始时间 |
| EndTime | Timestamp | 数据点结束时间 |
| Period | Integer | 数据统计周期 |
| DataPoints | Array of PointsObject | 监控数据列表 |
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId |

## 4. 示例

### 示例1 

拉取某个 ES 集群某段时间内统计周期为60秒的平均磁盘使用率监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CES
&MetricName=DiskUsageAvg
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=uInstanceId
&Instances.0.Dimensions.0.Value=es-example
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-08 16:40:00",
"EndTime": "2019-05-08 16:45:00",
"Period": 60,
"MetricName": "DiskUsageAvg",
"DataPoints": [
{
"Dimensions": [
{
"Name": "uInstanceId",
"Value": "es-example"
}
],
"Timestamps": [
1557304800,
1557304860,
1557304920,
1557304980,
1557305040,
1557305100
],
"Values": [
80.12,
80.132,
80.185,
80.249,
80.269,
80.316
]
}
],
"RequestId": "e7f8dd2b-4b55-4dd0-8c77-16597f02a7a4"
}
}
```

### 示例2 

拉取多个 ES 集群某段时间内统计周期为60秒的平均磁盘使用率监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CES
&MetricName=DiskUsageAvg
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=uInstanceId
&Instances.0.Dimensions.0.Value=es-example1
&Instances.1.Dimensions.0.Name=uInstanceId
&Instances.1.Dimensions.0.Value=es-example2
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-08 16:40:00",
"EndTime": "2019-05-08 16:45:00",
"Period": 60,
"MetricName": "DiskUsageAvg",
"DataPoints": [
{
"Dimensions": [
{
"Name": "uInstanceId",
"Value": "es-example1"
}
],
"Timestamps": [
1557304800,
1557304860,
1557304920,
1557304980,
1557305040,
1557305100
],
"Values": [
13.031,
13.031,
13.031,
13.031,
13.031,
13.031
]
},
{
"Dimensions": [
{
"Name": "uInstanceId",
"Value": "es-example2"
}
],
"Timestamps": [
1557304800,
1557304860,
1557304920,
1557304980,
1557305040,
1557305100
],
"Values": [
7.082,
7.082,
7.082,
7.082,
7.082,
7.082
]
}
],
"RequestId": "a9a1a9a6-c56b-4ad7-95fb-12dbf8f17f63"
}
}
```