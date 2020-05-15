## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend that you distribute call requests across a period of time.

To query the monitoring data of a TencentDB for TDSQL v3 instance, use the following input parameters:
&Namespace=QCE/DCDB
&Instances.N.Dimensions.0.Name=uuid
&Instances.N.Dimensions.0.Value=Instance ID

## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/product/1042/34425) supported by TencentDB for TDSQL |
| Namespace | Yes | String | Namespace. Each Tencent Cloud service has a namespace, such as QCE/DCDB for TencentDB for TDSQL. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :------- | :----------------------------------------------------------- | :--------------------------------------- |
| Instances.N.Dimensions.0.Name | uuid | Instance uuId | Enter a string-type dimension name, such as uuId |
| Instances.N.Dimensions.0.Value | uuid | Specific instance uuid | Enter a specific instance uuid, such as dcdbt-0gfryg60 |
| Instances.N.Dimensions.1.Name | shardId | A specific instance shard ID. To query shard monitoring data, pass in this parameter. If it is not passed in, overall instance monitoring data will be queried | Enter a string-type dimension name, such as shardId |
| Instances.N.Dimensions.1.Value | shardId | Specific instance shard ID | Enter a specific instance shard ID, such as shard-0mzlzl89 |

### 2.2. Metric names

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit | Statistical Granularity (Period) |
| :--------------------------- | :---------------------- | :---- | :----------------- |
| CpuUsageRate | CPU utilization | % | 60s and 300s |
| MemHitRate | Cache hit rate | % | 60s and 300s |
| DataDiskUsedRate | Disk capacity utilization | % | 60s and 300s |
| MemAvailable | Available cache capacity | GB | 60s and 300s |
| DataDiskAvailable | Available disk capacity | GB | 60s and 300s |
| BinlogUsedDisk | Used log disk capacity | GB | 60s and 300s |
| DiskIops | I/O utilization | % | 60s and 300s |
| ConnActive | Connections | Connections/sec | 60s and 300s |
| ConnRunning | Active connections | Connections/sec | 60s and 300s |
| TotalOrigSql | SQL statements | Statements/sec | 60s and 300s |
| TotalErrorSql | SQL errors | Errors/sec | 60s and 300s |
| TotalSuccessSql | SQL successes | Successes/sec | 60s and 300s |
| LongQuery | Slow queries | Queries/sec | 60s and 300s |
| TimeRange0 | Requests consuming 1–5 ms | Requests/sec | 60s and 300s |
| TimeRange1 | Requests consuming 5–20 ms | Requests/sec | 60s and 300s |
| TimeRange2 | Requests consuming 20–30 ms | Requests/sec | 60s and 300s |
| TimeRange3 | Requests consuming over 30 ms | Requests/sec | 60s and 300s |
| RequestTotal | Requests (QPS) | Requests/sec | 60s and 300s |
| SelectTotal | Queries | Queries/sec | 60s and 300s |
| UpdateTotal | Updates | Updates/sec | 60s and 300s |
| InsertTotal | Insertions | Insertions/sec | 60s and 300s |
| ReplaceTotal | Overwrites | Overwrites/sec | 60s and 300s |
| DeleteTotal | Deletions | Deletions/sec | 60s and 300s |
| MasterSwitchedTotal | Master-slave switchovers | Times/sec | 60s and 300s |
| SlaveDelay | Master-slave switchover delay | ms | 60s and 300s |
| InnodbBufferPoolReads | InnoDB disk reads | Reads/sec | 60s and 300s |
| InnodbBufferPoolReadRequests | InnoDB buffer pool reads | Reads/sec | 60s and 300s |
| InnodbBufferPoolReadAhead | InnoDB buffer pool prefetches | Prefetches/sec | 60s and 300s |
| InnodbRowsDeleted | Deleted InnoDB rows | Rows/sec | 60s and 300s |
| InnodbRowsInserted | Inserted InnoDB rows | Rows/sec | 60s and 300s |
| InnodbRowsRead | Read InnoDB rows | Rows/sec | 60s and 300s |
| InnodbRowsUpdated | Updated InnoDB rows | Rows/sec | 60s and 300s |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique request ID. Each request returns a unique ID. RequestId is required to troubleshoot issues |

## 4. Error Codes

| Error Code | Error Description | Error Message |
| :------- | :------------- | :----------------------------------- |
| -502 | The resource does not exist | OperationDenied.SourceNotExists |
| -503 | Incorrect request parameter | InvalidParameter |
| -505 | Missing parameter | InvalidParameter.MissingParameter |
| -507 | Limit exceeded | OperationDenied.ExceedLimit |
| -509 | Incorrect combination of dimensions | InvalidParameter.DimensionGroupError |
| -513 | Database operation failed | InternalError.DBoperationFail |

## 5. Samples

### Sample 1

This example shows you how to get the monitoring data for the CPU utilization of one TencentDB for TDSQL instance using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/DCDB
&MetricName=CpuUsageRate
&Period=60
&StartTime=2019-05-29T15:00:00+08:00
&EndTime=2019-05-29T15:05:00+08:00
&Instances.0.Dimensions.0.Name=uuid
&Instances.0.Dimensions.0.Value=dcdbt-123456asc
&<Common request parameters>
```

#### Sample output code



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

### Sample 2

This example shows you how to get the monitoring data for the CPU utilization of multiple TencentDB for TDSQL instances using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



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
&<Common request parameters>
```

#### Sample output code



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