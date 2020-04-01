## 1. 接口描述

接口：GetMonitorData

接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询分布式数据库 DCDB V3 监控数据，入参取值如下：

&Namespace=QCE/DCDB

&Instances.N.Dimensions.0.Name=uuid

&Instances.N.Dimensions.0.Value=实例 ID


## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1 输入参数

#### 2.1.1 输入参数总览

| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据，支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如： QCE/DCDB |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 endTime 不能小于 startTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------------------ | -------- | ------------------------------------------------------------ | ---------------------------------------- |
| Instances.N.Dimensions.0.Name | uuid | 实例的 uuId | String 类型维度名称：uuId |
| Instances.N.Dimensions.0.Value | uuid | 实例具体的 uuid | 输入实例的具体uuid，如 dcdbt-0gfryg60 |
| Instances.N.Dimensions.1.Name | shardId | 入参为实例具体的分片 ID，在需要查询分片的监控数据时传递，不传则查询汇总的实例监控数据 | String 类型维度名称：shardId |
| Instances.N.Dimensions.1.Value | shardId | 实例具体的 shardId | 输入实例的具体分片 ID，如 shard-0mzlzl89 |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度 (dimension) 可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标名称 | 含义 | 单位 | 统计粒度（period） |
| ---------------------------- | ----------------------- | ----- | ------------------ |
| CpuUsageRate | CPU 使用率 | % | 60s、300s |
| MemHitRate | 缓存命中率 | % | 60s、300s |
| DataDiskUsedRate | 磁盘空间利用率 | % | 60s、300s |
| MemAvailable | 可用缓存空间 | GB | 60s、300s |
| DataDiskAvailable | 可用磁盘空间 | GB | 60s、300s |
| BinlogUsedDisk | 已用日志磁盘空间 | GB | 60s、300s |
| DiskIops | IO 利用率 | % | 60s、300s |
| ConnActive | 总连接数 | 次/秒 | 60s、300s |
| ConnRunning | 活跃连接数 | 次/秒 | 60s、300s |
| TotalOrigSql | SQL 总数 | 次/秒 | 60s、300s |
| TotalErrorSql | SQL 错误数 | 次/秒 | 60s、300s |
| TotalSuccessSql | SQL 成功数 | 次/秒 | 60s、300s |
| LongQuery | 慢查询数 | 次/秒 | 60s、300s |
| TimeRange0 | 耗时(1~5ms)请求数 | 次/秒 | 60s、300s |
| TimeRange1 | 耗时(5~20ms)请求数 | 次/秒 | 60s、300s |
| TimeRange2 | 耗时(20~30ms)请求数 | 次/秒 | 60s、300s |
| TimeRange3 | 耗时(大于30ms)请求数 | 次/秒 | 60s、300s |
| RequestTotal | 总请求数(QPS) | 次/秒 | 60s、300s |
| SelectTotal | 查询数 | 次/秒 | 60s、300s |
| UpdateTotal | 更新数 | 次/秒 | 60s、300s |
| InsertTotal | 插入数 | 次/秒 | 60s、300s |
| ReplaceTotal | 覆盖数 | 次/秒 | 60s、300s |
| DeleteTotal | 删除数 | 次/秒 | 60s、300s |
| MasterSwitchedTotal | 主从切换 | 次/秒 | 60s、300s |
| SlaveDelay | 主从延迟 | Ms | 60s、300s |
| InnodbBufferPoolReads | innodb 磁盘读页次数 | 次/秒 | 60s、300s |
| InnodbBufferPoolReadRequests | innodb 缓冲池读页次数 | 次/秒 | 60s、300s |
| InnodbBufferPoolReadAhead | innodb 缓冲池预读页次数 | 次/秒 | 60s、300s |
| InnodbRowsDeleted | innodb 执行 DELETE 行数 | 次/秒 | 60s、300s |
| InnodbRowsInserted | innodb 执行 INSERT 行数 | 次/秒 | 60s、300s |
| InnodbRowsRead | innodb 执行 UPDATE 行数 | 次/秒 | 60s、300s |
| InnodbRowsUpdated | innodb 执行 UPDATE 行数 | 次/秒 | 60s、300s |



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

### 示例1 

拉取某个分布式数据库 DCDB 某段时间内统计周期为60秒的 CPU 使用率监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/DCDB
&MetricName=CpuUsageRate
&Period=60
&StartTime=2019-05-29T15:00:00+08:00
&EndTime=2019-05-29T15:05:00+08:00
&Instances.0.Dimensions.0.Name=uuid
&Instances.0.Dimensions.0.Value=dcdbt-123456asc
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-29 15:00:00",
"EndTime": "2019-05-29 15:05:00",
"Period": 60,
"MetricName": "CpuUsageRate",
"DataPoints": [
{
"Dimensions": [
{
"Name": "uuid",
"Value": "dcdbt-123456asc"
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
20,
12,
11,
10,
10,
19
]
}
],
"RequestId": "d7b1c977-490b-46c0-96cb-9b6a9f178f5f"
}
}
```

### 示例2 

拉取多个分布式数据库 DCDB 某段时间内统计周期为60秒的 CPU 使用率监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/DCDB
&MetricName=CpuUsageRate
&Period=60
&StartTime=2019-05-29T15:00:00+08:00
&EndTime=2019-05-29T15:05:00+08:00
&Instances.0.Dimensions.0.Name=uuid
&Instances.0.Dimensions.0.Value=dcdbt-123456asc
&Instances.1.Dimensions.0.Name=uuid
&Instances.1.Dimensions.0.Value=dcdbt-123456ascd
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-29 15:00:00",
"EndTime": "2019-05-29 15:05:00",
"Period": 60,
"MetricName": "CpuUsageRate",
"DataPoints": [
{
"Dimensions": [
{
"Name": "uuid",
"Value": "dcdbt-123456asc"
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
20,
12,
11,
10,
10,
19
]
},
{
"Dimensions": [
{
"Name": "uuid",
"Value": "dcdbt-123456ascd"
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
20,
12,
11,
10,
10,
19
]
}
],
"RequestId": "d7b1c977-490b-46c0-96cb-9b6a9f178f5f"
}
}
```