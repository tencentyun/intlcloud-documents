## 1. 接口描述

接口：GetMonitorData

接口请求域名： monitor.tencentcloudapi.com

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询云数据库（MySQL）产品监控数据，入参取值如下：

&Namespace=QCE/CDB

&Instances.N.Dimensions.0.Name=InstanceId

&Instances.N.Dimensions.0.Value=数据库的具体ID


## 2. 输入参数

以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见[公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478)页面。

### 2.1.1 输入参数

| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云数据库支持的[地域列表](https://intl.cloud.tencent.com/document/api/236/15833) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间,如:QCE/CDB |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 endTime不能小于startTime |


#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | 数据库实例 ID | String类型维度名称：topicId |
| Instances.N.Dimensions.0.Value | InstanceId | 数据库的具体ID | 具体实例名称，如 topic-i4p4k0u0 |
| Instances.N.Dimensions.1.Name | InstanceType | 数据库实例类型 | String类型维度名称：InstanceType |
| Instances.N.Dimensions.1.Value | InstanceType | 数据库实例类型，默认取值为1，表示拉取master监控数据。当需要拉取slave的SlaveIoRunning、SlaveSqlRunning、MasterSlaveSyncDistance、SecondsBehindMaster的监控数据时，需将InstanceType的值设置为2. |实例类型，默认取值为1|


### 2.2 指标名称

每个指标的统计粒度（Period）可取值不一定相同，可通过[DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/338821)接口获取每个接口支持的统计粒度。

| 指标名称 | 含义 | 单位 |
| ----------------------------- | -------------- | ------ |
|CPUUseRate|CPU利用率|%|
|MemoryUseRate|内存利用率|%|
|MemoryUse|内存占用|MB|
|VolumeRate|磁盘使用率|%|
|RealCapacity|磁盘使用空间（仅包含数据空间使用量）|MB|
|Capacity|磁盘占用空间（包含数据及日志空间使用量）|MB|
|BytesSent|内网出流量|Byte/秒|
|BytesReceived|内网入流量|Byte/秒|
|QPS|每秒执行操作数|次/秒|
|TPS|每秒执行事务数|次/秒|
|MaxConnections|最大连接数|个|
|ThreadsConnected|当前打开连接数|个|
|ConnectionUseRate|连接数利用率|%|
|SlowQueries|慢查询数|次/分|
|SelectScan|全表扫描数|次/秒|
|SelectCount|查询数|次/秒|
|ComUpdate|更新数|次/秒|
|ComDelete|删除数|次/秒|
|ComInsert|插入数|次/秒|
|ComReplace|覆盖数|次/秒|
|Queries|总请求数|次/秒|
|QueryRate|查询使用率|%|
|CreatedTmpTables|临时表数量|次/秒|
|TableLocksWaited|等待表锁次数|次/秒|
|InnodbCacheUseRate|innodb缓存使用率|%|
|InnodbCacheHitRate|innodb缓存命中率|%|
|InnodbOsFileReads|innodb读磁盘数量|次/秒|
|InnodbOsFileWrites|innodb写磁盘数量|次/秒|
|InnodbOsFsyncs|innodb fsync数量|次/秒|
|InnodbNumOpenFiles|当前InnoDB打开表的数量|个|
|KeyCacheUseRate|myisam缓存使用率|%|
|KeyCacheHitRate|myisam缓存命中率|%|
|ComCommit|提交数|次/秒|
|ComRollback|回滚数|次/秒|
|ThreadsCreated|已创建的线程数|个|
|ThreadsRunning|运行的线程数|个|
|CreatedTmpDiskTables|磁盘临时表数量|次/秒|
|CreatedTmpFiles|临时文件数量|次/秒|
|HandlerReadRndNext|读下一行请求数|次/秒|
|HandlerRollback|内部回滚数|次/秒|
|HandlerCommit|内部提交数|次/秒|
|InnodbBufferPoolPagesFree|InnoDB空页数|个|
|InnodbBufferPoolPagesTotal|InnoDB总页数|个|
|InnodbBufferPoolReadRequests|InnoDB逻辑读|次/秒|
|InnodbBufferPoolReads|InnoDB物理读|次/秒|
|InnodbDataReads|InnoDB总读取量|次/秒|
|InnodbDataRead|InnoDB读取量|Byte/秒|
|InnodbDataWrites|InnoDB总写入量|次/秒|
|InnodbDataWritten|InnoDB写入量|Byte/秒|
|InnodbRowsDeleted|InnoDB行删除量|次/秒|
|InnodbRowsInserted|InnoDB行插入量|次/秒|
|InnodbRowsUpdated|InnoDB行更新量|次/秒|
|InnodbRowsRead|InnoDB行读取量|次/秒|
|InnodbRowLockTimeAvg|InnoDB平均获取行锁时间|毫秒|
|InnodbRowLockWaits|InnoDB等待行锁次数|次/秒|
|KeyBlocksUnused|键缓存内未使用的块数量|个|
|KeyBlocksUsed|键缓存内使用的块数量|个|
|KeyReadRequests|键缓存读取数据块次数|次/秒|
|KeyReads|硬盘读取数据块次数|次/秒|
|KeyWriteRequests|数据块写入键缓冲次数|次/秒|
|KeyWrites|数据块写入磁盘次数|次/秒|
|OpenedTables|已经打开的表数|个|
|TableLocksImmediate|立即释放的表锁数|个|
|OpenFiles|打开文件总数|个|
|LogCapacity|日志使用量|MB|
|SlaveIoRunning|IO线程状态| |
|SlaveSqlRunning|SQL线程状态| |
|MasterSlaveSyncDistance|主从延迟距离|MB|
|SecondsBehindMaster|主从延迟时间|秒|


## 3. 输出参数

| 参数名称 | 类型 | 描述 |
| ---------- | --------------------- | ---------------------------------------- |
| MetricName | String | 监控指标 |
| StartTime | Timestamp | 数据点起始时间 |
| EndTime | Timestamp | 数据点结束时间 |
| Period | Integer | 数据统计周期 |
| DataPoints | Array of PointsObject | 监控数据列表 |
| RequestId | String | 唯一请求ID，每次请求都会返回。定位问题时需要提供该次请求的RequestId。 |

## 4. 示例

### 示例1 拉取单个实例监控数据示例

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CDB
&MetricName=SlowQueries
&Period=300
&StartTime=2018-08-24T10:50:00+08:00
&EndTime=2018-08-24T11:00:00+08:00
&Instances.0.Dimensions.0.Name=InstanceId
&Instances.0.Dimensions.0.Value=cdb-e242adzf
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"DataPoints": [
{
"Dimensions": [
{
"Name": "InstanceId",
"Value": "cdb-e242adzf"
}
],
"Timestamps": [
1535079000,
1535079300,
1535079600
],
"Values": [
2,
2,
6
]
}
],
"EndTime": "2018-08-24 11:00:00",
"MetricName": "SlowQueries",
"Period": 300,
"RequestId": "d96ec542-6547-4af2-91ac-fee85c1b8b85",
"StartTime": "2018-08-24 10:50:00"
}
}
```

### 示例2 拉取多个实例监控数据示例

#### 场景描述

拉取多个云数据库MySQL某段时间内统计周期为5分钟的慢查询数监控数据

#### 请求参数

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CDB
&MetricName=SlowQueries
&Period=300
&StartTime=2018-08-24T10:50:00+08:00
&EndTime=2018-08-24T11:00:00+08:00
&Instances.0.Dimensions.0.Name=InstanceId
&Instances.0.Dimensions.0.Value=cdb-e242adzf
&Instances.1.Dimensions.0.Name=InstanceId
&Instances.1.Dimensions.0.Value=cdb-o8vv2w10
&<公共请求参数>
```

#### 返回参数

```
{
"Response": {
"DataPoints": [
{
"Dimensions": [
{
"Name": "InstanceId",
"Value": "cdb-e242adzf"
}
],
"Timestamps": [
1535079000,
1535079300,
1535079600
],
"Values": [
2,
2,
6
]
},
{
"Dimensions": [
{
"Name": "InstanceId",
"Value": "cdb-o8vv2w10"
}
],
"Timestamps": [
1535079000,
1535079300,
1535079600
],
"Values": [
3,
3,
6
]
}
],
"EndTime": "2018-09-22 10:50:00",
"MetricName": "SlowQueries",
"Period": 300,
"RequestId": "9ac53ccc-fbab-483d-980b-b763bcc2f83f",
"StartTime": "2018-09-22 11:00:00"
}
}
```
