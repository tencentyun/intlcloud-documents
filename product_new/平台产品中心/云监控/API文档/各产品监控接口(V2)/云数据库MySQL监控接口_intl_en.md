## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a TencentDB for MySQL instance, use the following input parameters:

&Namespace=QCE/CDB

&Instances.N.Dimensions.0.Name=InstanceId

&Instances.N.Dimensions.0.Value=specific database ID


## 2. Input Parameters

The list below contains only the API request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://cloud.tencent.com/document/api/248/4478).

### 2.1.1. Input parameters

| Parameter Name | Required | Type | Description |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://cloud.tencent.com/document/api/236/15833) supported by TencentDB |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/CDB` |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://cloud.tencent.com/document/product/248/30354) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |


#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | Database instance ID | String-type dimension name: topicId |
| Instances.N.Dimensions.0.Value | InstanceId | Specific database ID | Specific instance name, such as topic-i4p4k0u0 |
| Instances.N.Dimensions.1.Name | InstanceType | Database instance type | String-type dimension name: InstanceType |
| Instances.N.Dimensions.1.Value | InstanceType | Database instance type. The default value is 1, indicating to get the monitoring data of the master. If you want to get the `SlaveIoRunning`, `SlaveSqlRunning`, `MasterSlaveSyncDistance`, or `SecondsBehindMaster` monitoring data of the slave, you need to set the value of `InstanceType` to 2 | Instance type. Default value: 1 |


### 2.2. Metric name

The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` supported by each API.

| Metric Name | Description | Unit |
| ----------------------------- | -------------- | ------ |
|CPUUseRate| CPU utilization |%|
|MemoryUseRate| Memory utilization |%|
|MemoryUse| Used memory |MB|
|VolumeRate| Disk utilization |%|
|RealCapacity| Used disk capacity (by data only) | MB |
|Capacity| Used disk capacity (by data and logs) | MB |
|BytesSent| Private network outbound traffic | Bytes/sec |
|BytesReceived| Private network inbound traffic | Bytes/sec |
|QPS| Queries per second | Queries/sec |
|TPS| Transactions executed per second | Transactions/sec |
|MaxConnections| Maximum connections | - |
|ThreadsConnected| Active connections | - |
|ConnectionUseRate| Connection utilization |%|
|SlowQueries| Slow queries | Queries/min |
|SelectScan| Full table scans | Scans/sec |
|SelectCount| Queries | Queries/sec |
|ComUpdate| Updates | Updates/sec |
|ComDelete| Deletions | Deletions/sec |
|ComInsert| Insertions | Insertions/sec |
|ComReplace| Replacements | Replacements/sec |
|Queries| Requests | Requests/sec |
|QueryRate| Query utilization | % |
|CreatedTmpTables| Temporary tables | Tables/sec |
|TableLocksWaited| Table lock waits | Waits/sec |
|InnodbCacheUseRate| InnoDB cache utilization | % |
|InnodbCacheHitRate| InnoDB cache hit rate | % |
|InnodbOsFileReads| InnoDB disk reads | Reads/sec |
|InnodbOsFileWrites| InnoDB disk writes | Writes/sec |
|InnodbOsFsyncs| InnoDB Fsyncs | Fsyncs/sec |
|InnodbNumOpenFiles| Opened InnoDB tables | - |
|KeyCacheUseRate| MyISAM cache utilization | % |
|KeyCacheHitRate| MyISAM cache hit rate | % |
|ComCommit| Commits | Commits/sec |
|ComRollback| Rollbacks | Rollbacks/sec |
|ThreadsCreated| Established threads | - |
|ThreadsRunning| Running threads | - |
|CreatedTmpDiskTables| Temporary tables in disk | Tables/sec |
|CreatedTmpFiles| Temporary files | Files/sec |
|HandlerReadRndNext| Read-next-row requests | Requests/sec |
|HandlerRollback| Internal rollbacks | Rollbacks/sec |
|HandlerCommit| Internal commits | Commits/sec |
|InnodbBufferPoolPagesFree| Empty InnoDB pages | - |
|InnodbBufferPoolPagesTotal| InnoDB pages | - |
|InnodbBufferPoolReadRequests| InnoDB logical reads | Reads/sec |
|InnodbBufferPoolReads| InnoDB physical reads | Reads/sec |
|InnodbDataReads| InnoDB reads | Reads/sec |
|InnodbDataRead| InnoDB data read | Bytes/sec |
|InnodbDataWrites| InnoDB writes | Writes/sec |
|InnodbDataWritten| InnoDB data written | Bytes/sec |
|InnodbRowsDeleted| InnoDB row deletions | Deletions/sec |
|InnodbRowsInserted| InnoDB row insertions | Insertions/sec |
|InnodbRowsUpdated| InnoDB row updates | Updates/sec |
|InnodbRowsRead| InnoDB row reads | Reads/sec |
|InnodbRowLockTimeAvg| Average InnoDB row lock wait time | Milliseconds |
|InnodbRowLockWaits| InnoDB row lock waits | Waits/sec |
|KeyBlocksUnused| Unused blocks in key cache | - |
|KeyBlocksUsed| Used blocks in key cache | - |
|KeyReadRequests| Data block reads from key cache | Reads/sec |
|KeyReads| Data block reads from disk | Reads/sec |
|KeyWriteRequests| Data block writes to key cache | Writes/sec |
|KeyWrites| Data block writes to disk | Writes/sec |
|OpenedTables| Opened tables | - |
|TableLocksImmediate| Immediately released table locks | - |
|OpenFiles| Opened files | - |
|LogCapacity| Used log capacity | MB |
|SlaveIoRunning| IO thread status | - |
|SlaveSqlRunning| SQL thread status | - |
|MasterSlaveSyncDistance| Master/slave delay distance | MB |
|SecondsBehindMaster| Master/slave delay time | Seconds |


## 3. Output Parameters

| Parameter Name | Type | Description |
| ---------- | --------------------- | ---------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues |

## 4. Samples

### Sample 1. Getting the monitoring data of one instance

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CDB
&MetricName=SlowQueries
&Period=300
&StartTime=2018-08-24T10:50:00+08:00
&EndTime=2018-08-24T11:00:00+08:00
&Instances.0.Dimensions.0.Name=InstanceId
&Instances.0.Dimensions.0.Value=cdb-e242adzf
&<Common request parameters>
```

#### Output sample code

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

### Sample 2. Getting the monitoring data of multiple instances

#### Scenario description

This example shows you how to get the number of slow queries of multiple TencentDB for MySQL instances using a statistical period of 5 minutes for a specified length of time.

#### Request parameters

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
&<Common request parameters>
```

#### Response parameters

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
