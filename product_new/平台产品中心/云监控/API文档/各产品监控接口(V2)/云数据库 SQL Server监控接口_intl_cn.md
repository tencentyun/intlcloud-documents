## 1. 接口描述

接口：GetMonitorData

接口请求域名： `monitor.tencentcloudapi.com`

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询云数据库 SQL Server监控数据，入参取值如下：

&Namespace=QCE/SQLSERVER

&Instances.N.Dimensions.0.Name=resourceId 

&Instances.N.Dimensions.0.Value 为实例的资源 ID


## 2. 输入参数


以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，详情请参见 [公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478) 文档。

### 2.1输入参数
#### 2.1.1 输入参数总览
| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的 [地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如： QCE/SQLSERVER |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 endTime 不能小于 startTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | resourceId | 实例的resourceId | String类型维度名称：resourceId |
| Instances.N.Dimensions.0.Value | resourceId | 实例具体的资源 Id | 具体实例名称，如mssql-dh0123456 |

### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度（dimension）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度及维度信息。

| 指标名称 | 含义 | 单位 |
| ---------------------- | --------------------- | ---- |
| Cpu | 实例 CPU 消耗的百分比 | % |
| Transactions | 平均每秒的事务数 | 次/秒 |
| Connections | 平均每秒用户连接数据库的个数 | 个 |
| Requests | 每秒请求次数 | 次/秒 |
| Logins | 每秒登录次数 | 次/秒 |
| Logouts | 每秒登出次数 | 次/秒 |
| Storage | 实例数据库文件和日志文件占用的空间总和 | GB |
| InFlow | 所有连接输入包大小总和 | MB/s |
| OutFlow | 所有连接输出包大小总和 | MB/s |
| Iops | 磁盘读写次数 | 次/秒 |
| DiskReads | 每秒读取磁盘次数 | 次/秒 |
| DiskWrites | 每秒写入磁盘次数 | 次/秒 |
| SlowQueries | 运行时间超过1秒的查询数量 | 个 |
| BlockedProcesses | 当前阻塞数量 | 个 |
| LockRequests | 平均每秒锁请求的次数 | 次/秒 |
| UserErrors | 平均每秒错误数 | 次/秒 |
| SqlCompilations | 平均每秒 SQL 编译次数 | 次/秒 |
| SqlRecompilations | 平均每秒 SQL 重编译次数 | 次/秒 |
| FullScans | 每秒不受限制的完全扫描数 | 次/秒 |
| BufferCacheHitRatio | 数据缓存（内存）命中率 | % |
| LatchWaits | 每秒闩锁等待数量 | 次/秒 |
| LockWaits | 每个导致等待的锁请求的平均等待时间 | Ms |
| NetworkIoWaits | 平局网络 IO 延迟时间 | Ms |
| PlanCacheHitRatio | 每个 SQL 有一个执行计划，执行计划的命中率 | % |



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
拉取某个云数据库 SQL Server 某段时间内统计周期为300秒的实例 CPU 消耗的百分比监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/SQLSERVER
&MetricName=Cpu
&Period=300
&StartTime=2019-05-29T15:00:00+08:00
&EndTime=2019-05-29T15:05:00+08:00
&Instances.0.Dimensions.0.Name=resourceId
&Instances.0.Dimensions.0.Value=mssql-12345
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-29 15:00:00",
"EndTime": "2019-05-29 15:05:00",
"Period": 300,
"MetricName": "Cpu",
"DataPoints": [
{
"Dimensions": [
{
"Name": "resourceId",
"Value": "mssql-12345"
}
],
"Timestamps": [
1559113200,
1559113500
],
"Values": [
0,
0
]
}
],
"RequestId": "2e3f486c-d0c2-4c6b-8adc-db0df6e426fb"
}
}
```
### 示例2 
拉取多个云数据库 SQL Server某段时间内统计周期为300秒的实例 CPU 消耗的百分比监控数据。

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/SQLSERVER
&MetricName=Cpu
&Period=300
&StartTime=2019-05-29T15:00:00+08:00
&EndTime=2019-05-29T15:05:00+08:00
&Instances.0.Dimensions.0.Name=resourceId
&Instances.0.Dimensions.0.Value=mssql-12345
&Instances.1.Dimensions.0.Name=resourceId
&Instances.1.Dimensions.0.Value=mssql-123456
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-05-29 15:00:00",
"EndTime": "2019-05-29 15:05:00",
"Period": 300,
"MetricName": "Cpu",
"DataPoints": [
{
"Dimensions": [
{
"Name": "resourceId",
"Value": "mssql-12345"
}
],
"Timestamps": [
1559113200,
1559113500
],
"Values": [
0,
0
]
},
{
"Dimensions": [
{
"Name": "resourceId",
"Value": "mssql-123456"
}
],
"Timestamps": [
1559113200,
1559113500
],
"Values": [
0,
0
]
}
],
"RequestId": "2e3f486c-d0c2-4c6b-8adc-db0df6e426fb"
}
}
```