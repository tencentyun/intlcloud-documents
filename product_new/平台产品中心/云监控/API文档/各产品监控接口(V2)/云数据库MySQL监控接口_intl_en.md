## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension description, and monitoring metrics.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the monitoring data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend that you distribute call requests across a period of time.

To query the monitoring data of TencentDB for MySQL, use the following input parameters:
&Namespace=QCE/CDB
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=Specific database ID

## 2. Input Parameters

The list below contains only the API request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1.1. Input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, see the [list of regions](https://intl.cloud.tencent.com/document/product/236/15833) supported by TencentDB for MySQL |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/CDB for TencentDB for MySQL. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Dimension parameters

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :----------- | :----------------------------------------------------------- | :--------------------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | Database instance ID | Enter a string-type dimension name, such as: topicId |
| Instances.N.Dimensions.0.Value | InstanceId | Specific database ID | Enter a specific instance ID, such as topic-i4p4k0u0 |
| Instances.N.Dimensions.1.Name | InstanceType | Database instance type | Enter a string-type dimension name, such as: InstanceType |
| Instances.N.Dimensions.1.Value | InstanceType | Database instance type. The default value is 1, which indicates to get the monitoring data of the master. To obtain the `SlaveIoRunning`, `SlaveSqlRunning`, `MasterSlaveSyncDistance`, or `SecondsBehindMaster` monitoring data of the slave, configure the value of `InstanceType` to 2 | Instance type. Default value: 1 |

### 2.2. Metric names

The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

| Metric Name | Description | Unit |
| :--------------------------- | :--------------------------------------- | :------ |
| CPUUseRate | CPU utilization | % |
| MemoryUseRate | Memory utilization | % |
| MemoryUse | Memory usage | MB |
| VolumeRate | Disk utilization | % |
| RealCapacity | Used disk capacity (only includes the data capacity usage) | MB |
| Capacity | Used disk capacity (includes the data and log capacity usage) | MB |
| BytesSent | Private network outbound traffic | Bytes/second |
| BytesReceived | Private network inbound traffic | Bytes/second |
| QPS | Operations per second | Times/second |
| TPS | Transactions per second | Times/second |
| MaxConnections | Max number of connections | - |
| ThreadsConnected | Currently established connections | - |
| SlowQueries | Slow queries | Times/minute |
| SelectScan | Full-table scans | Times/second |
| SelectCount | Queries | Times/second |
| ComUpdate | Updates | Times/second |
| ComDelete | Deletions | Times/second |
| ComInsert | Insertions | Times/second |
| ComReplace | Overwrites | Times/second |
| Queries | Total requests | Times/second |
| QueryRate | Query utilization | % |
| CreatedTmpTables | Temporary tables | Times/second |
| TableLocksWaited | Waiting table locks | Times/second |
| InnodbCacheUseRate | InnoDB cache utilization | % |
| InnodbCacheHitRate | InnoDB cache hit rate | % |
| InnodbOsFileReads | InnoDB disk reads | Times/second |
| InnodbOsFileWrites | InnoDB disk writes | Times/second |
| InnodbOsFsyncs | InnoDB fsync count | Times/second |
| InnodbNumOpenFiles | Currently opened tables by InnoDB | - |
| KeyCacheUseRate | MyISAM cache utilization | % |
| KeyCacheHitRate | MyISAM cache hit rate | % |
| ComCommit | Submissions | Times/second |
| ComRollback | Rollbacks | Times/second |
| ThreadsCreated | Created threads | - |
| threads_running | Running threads | - |
| CreatedTmpDiskTables | Temporary disk tables | Times/second |
| CreatedTmpFiles | Temporary files | Times/second |
| HandlerReadRndNext | Next-line read requests | Times/second |
| HandlerRollback | Internal rollbacks | Times/second |
| HandlerCommit | Internal submissions | Times/second |
| InnodbBufferPoolPagesFree | Empty pages in InnoDB | - |
| InnodbBufferPoolPagesTotal | Total pages in InnoDB | - |
| InnodbBufferPoolReadRequests | InnoDB logical reads | Times/second |
| InnodbBufferPoolReads | InnoDB physical reads | Times/second |
| InnodbDataReads | InnoDB total reads | Times/second |
| InnodbDataRead | InnoDB read amount | Bytes/second |
| InnodbDataWrites | InnoDB total writes | Times/second |
| InnodbDataWritten | InnoDB write amount | Bytes/second |
| InnodbRowsDeleted | InnoDB line deletions | Times/second |
| InnodbRowsInserted | InnoDB line insertions | Times/second |
| InnodbRowsUpdated | InnoDB line updates | Times/second |
| InnodbRowsRead | InnoDB line reads | Times/second |
| InnodbRowLockTimeAvg | Average time of acquiring row locks by InnoDB | Millisecond |
| InnodbRowLockWaits | InnoDB row lock waits | Times/second |
| KeyBlocksUnused | Unused blocks in the key cache | - |
| KeyBlocksUsed | Used blocks in the key cache | - |
| KeyReadRequests | Data block reads by the key cache | Times/second |
| KeyReads | Data block reads by disks | Times/second |
| KeyWriteRequests | Data block writes to the key cache | Times/second |
| KeyWrites | Data block writes to disks | Times/second |
| OpenedTables | Opened tables | - |
| InnodbNumOpenFiles | Table locks released immediately | - |
| OpenFiles | Total opened files | - |
| LogCapacity | Log usage | MB |
| SlaveIoRunning | I/O thread status | - |
| SlaveSqlRunning | SQL thread status | - |
| MasterSlaveSyncDistance | Master-slave delay distance | MB |
| SecondsBehindMaster | Master-slave delay time | MB |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime  | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. RequestId is required to troubleshoot issues |

## 4. Samples

### Sample 1. Getting the monitoring data of a single instance

#### Sample input code



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

#### Sample output code



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

#### Description

This example shows you how to get the monitoring data for the number of slow queries of multiple TencentDB for MySQL instances using a statistical period of 5 minutes for a specified length of time.

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
    "EndTime": "2018-09-22 11:00:00",
    "MetricName": "SlowQueries",
    "Period": 300,
    "RequestId": "9ac53ccc-fbab-483d-980b-b763bcc2f83f",
    "StartTime": "2018-09-22 10:50:00"
  }
}
```