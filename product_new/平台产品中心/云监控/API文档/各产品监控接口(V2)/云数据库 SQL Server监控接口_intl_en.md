## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metrics.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend spreading call requests across a period of time.

This API is used to query the monitoring data of TencentDB for SQL Server. The values of input parameters are as follows:
&Namespace=QCE/SQLSERVER
&Instances.N.Dimensions.0.Name=resourceId
&Instances.N.Dimensions.0.Value=Instance resource ID

## 2. Input Parameters

The list below contains only the API request parameters and some common request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1 Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. Value: GetMonitorData |
| Version | Yes | String | Common parameter. Value: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, see the [list of regions](https://intl.cloud.tencent.com/document/product/238/32088) supported by TencentDB for SQL Server |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/SQLSERVER for TencentDB for SQL Server. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :--------- | :---------------- | :-------------------------------------------- |
| Instances.N.Dimensions.0.Name | resourceId | Instance resourceId | Enter a string-type dimension name, such as resourceId |
| Instances.N.Dimensions.0.Value | resourceId | Specific instance resource ID | Enter a specific instance resource ID, such as mssql-dh0123456 |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit |
| :------------------ | :---------------------------------------- | :---- |
| Cpu | Percentage of CPU resources consumed by the instance | % |
| Transactions | Average number of transactions per second | Times/sec |
| Connections | Average number of user connections to the database per second | - |
| Requests | Number of requests per second | Times/sec |
| Logins | Number of logins per second | Times/sec |
| Logouts | Number of logouts per second | Times/sec |
| Storage | Total amount of storage occupied by instance database files and log files | GB |
| InFlow | Total size of all inbound packages | MB/sec |
| OutFlow | Total size of all outbound packages | MB/sec |
| Iops | Disk reads and writes | Times/sec |
| DiskReads | Disk reads per second | Times/sec |
| DiskWrites | Disk writes per second | Times/sec |
| SlowQueries | Queries with an execution time greater than 1 second | - |
| BlockedProcesses | Current blocks | - |
| LockRequests | Average number of lock requests per second | Times/sec |
| UserErrors | Average number of errors per second | Times/sec |
| SqlCompilations | Average number of SQL compilations per second | Times/sec |
| SqlRecompilations | Average number of SQL recompilations per second | Times/sec |
| FullScans | Unrestricted full scans per second | Times/sec |
| BufferCacheHitRatio | Data cache (memory) hit rate | % |
| LatchWaits | Number of latch waits per second | Times/sec |
| LockWaits | Average waiting time for each lock request that causes waiting | ms |
| NetworkIoWaits | Average network I/O delay | ms |
| PlanCacheHitRatio | Hit rate of the execution plan (each SQL task has an execution plan) | % |

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
| -502 | Resource does not exist | OperationDenied.SourceNotExists |
| -503 | Incorrect request parameter | InvalidParameter |
| -505 | Missing parameter | InvalidParameter.MissingParameter |
| -507 | Limit exceeded | OperationDenied.ExceedLimit |
| -509 | Incorrect dimension combination | InvalidParameter.DimensionGroupError |
| -513 | DB operation failed | InternalError.DBoperationFail |

## 5. Samples

### Sample 1

This example shows you how to get the monitoring data for the instance CPU utilization of one TencentDB for SQL Server instance using a statistical period of 300 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/SQLSERVER
&MetricName=Cpu
&Period=300
&StartTime=2019-05-29T15:00:00+08:00
&EndTime=2019-05-29T15:05:00+08:00
&Instances.0.Dimensions.0.Name=resourceId
&Instances.0.Dimensions.0.Value=mssql-12345
&<Common request parameters>
```

#### Sample output code



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

### Sample 2

This example shows you how to get the monitoring data for the instance CPU utilization of multiple TencentDB for SQL Server instances using a statistical period of 300 seconds for a specified length of time.

#### Sample input code



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
&<Common request parameters>
```

#### Sample output code



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