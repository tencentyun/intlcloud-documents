## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a TencentDB for SQL Server instance, use the following input parameters:

&Namespace=QCE/SQLSERVER

&Instances.N.Dimensions.0.Name=resourceId 

&Instances.N.Dimensions.0.Value=instance resource ID


## 2. Input Parameters


The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters
#### 2.1.1. Overview of input parameters
| Parameter Name | Required | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/SQLSERVER`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | resourceId | Instance `resourceId` | String-type dimension name: resourceId |
| Instances.N.Dimensions.0.Value | resourceId | Specific instance resource ID | Specific instance name, such as mssql-dh0123456 |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit |
| ---------------------- | --------------------- | ---- |
| Cpu | Instance CPU utilization | % |
| Transactions | Average transactions per second | Transactions/sec |
| Connections | Average user connections to database per second | - |
| Requests | Requests per second | Requests/sec |
| Logins | Logins per second | Logins/sec |
| Logouts | Logouts per second | Logouts/sec |
| Storage | Total storage capacity used by instance database files and log files | GB |
| InFlow | Total incoming packets of all connections | MB/s |
| OutFlow | Total outgoing packets of all connections | MB/s |
| Iops | Disk reads/writes | Operations/sec |
| DiskReads | Disk reads per second | Reads/sec |
| DiskWrites | Disk writes per second | Writes/sec |
| SlowQueries | Queries with an execution duration of more than 1 second | - |
| BlockedProcesses | Current blocked processes | - |
| LockRequests | Average lock requests per second | Requests/sec |
| UserErrors | Average errors per second | Errors/sec |
| SqlCompilations | Average SQL compilations per second | Compilations/sec |
| SqlRecompilations | Average SQL recompilations per second | Recompilations/sec |
| FullScans | Unrestricted full scans per second | Scans/sec |
| BufferCacheHitRatio | Data cache (memory) hit rate | % |
| LatchWaits | Latch waits per second | Waits/sec |
| LockWaits | Average wait time for each lock request that causes a wait | Ms |
| NetworkIoWaits | Average network IO delay | Ms |
| PlanCacheHitRatio | Hit rate of execution plan of each SQL | % |



## 3. Output Parameters

| Parameter Name | Type | Description |
| ---------- | --------------------- | ------------------------------------------------------------ |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues |

## 4. Error Codes

| Error Code | Error Description | Error Message |
| ---- | ------- | ------------------------------------ |
| -502 | The resource does not exist. | OperationDenied.SourceNotExists |
| -503 | Incorrect request parameter. | InvalidParameter |
| -505 | Missing parameter. | InvalidParameter.MissingParameter |
| -507 | Limit exceeded. | OperationDenied.ExceedLimit |
| -509 | Incorrect combination of dimensions. | InvalidParameter.DimensionGroupError |
| -513 | Database operation failed. | InternalError.DBoperationFail |

## 5. Samples

### Sample 1 
This example shows you how to get the instance CPU utilization of one TencentDB for SQL Server instance using a statistical period of 300 seconds for a specified length of time.

#### Input sample code

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

#### Output sample code

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
This example shows you how to get the instance CPU utilization of multiple TencentDB for SQL Server instances using a statistical period of 300 seconds for a specified length of time.

#### Input sample code

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

#### Output sample code

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