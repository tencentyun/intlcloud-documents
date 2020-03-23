## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of an ES instance, use the following input parameters:

&Namespace=QCE/CES

&Instances.N.Dimensions.0.Name=uInstanceId

&Instances.N.Dimensions.0.Value=es-example


## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. All common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/CES`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ----------- | ------------ | ------------------------------- |
| Instances.N.Dimensions.0.Name | uInstanceId | ES instance ID | String-type dimension name: uInstanceId |
| Instances.N.Dimensions.0.Value | uInstanceId | ES instance ID | Specific instance name, such as es-example |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Calculation Rule | Meaning | Unit | Period |
| ------------------------------ | -------------------------- | -------------------------------------------------------- | ------------------------------------ | ------- | ------------------ |
| Status | Cluster health status | Latest value of ES cluster in the statistical period | Cluster health status. 0: Green, 1: Yellow, 2: Red | - | 60s, 300s |
| DiskUsageAvg | Average disk utilization | Average value of disk utilization of each node in ES cluster in the statistical period | Average value of disk utilization of each node in ES cluster | % | 60s, 300s |
| DiskUsageMax | Maximum disk utilization | Maximum value of disk utilization of each node in ES cluster in the statistical period | Maximum value of disk utilization of each node in ES cluster | % | 60s, 300s |
| JvmMemUsageAvg | Average JVM memory utilization | Average value of JVM memory utilization of each node in ES cluster in the statistical period | Average value of JVM memory utilization of each node in ES cluster | % | 60s, 300s |
| JvmMemUsageMax | Maximum JVM memory utilization | Maximum value of JVM memory utilization of each node in ES cluster in the statistical period | Maximum value of JVM memory utilization of each node in ES cluster | % | 60s, 300s |
| CpuUsageAvg | Average CPU utilization | Average value of CPU utilization of each node in ES cluster in the statistical period | Average value of CPU utilization of each node in ES cluster | % | 60s, 300s |
| CpuUsageMax | Maximum CPU utilization | Maximum value of CPU utilization of each node in ES cluster in the statistical period | Maximum value of CPU utilization of each node in ES cluster | % | 60s, 300s |
| CpuLoad1minAvg | Average cluster CPU load per minute | Value of the average CPU load per minute of each node in the ES cluster during the statistical period | Value of the average CPU load per minute of each node in the ES cluster  | - | 60s, 300s |
| CpuLoad1minMax | Maximum cluster CPU load per minute | Value of the maximum CPU load per minute of each node in the ES cluster during the statistical period | Value of the maximum CPU load per minute of each node in the ES cluster | - | 60s, 300s |
| IndexLatencyAvg | Average write latency | Average value of write latency of ES cluster in the statistical period | Average value of write latency of ES cluster | ms | 60s, 300s |
| IndexLatencyMax | Maximum write latency | Maximum value of write latency of ES cluster in the statistical period | Maximum value of write latency of ES cluster | ms | 60s, 300s |
| SearchLatencyAvg | Average query latency | Average value of query latency of ES cluster in the statistical period | Average value of query latency of ES cluster | ms | 60s, 300s |
| SearchLatencyMax | Maximum query latency | Maximum value of query latency of ES cluster in the statistical period | Maximum value of query latency of ES cluster | ms | 60s, 300s |
| IndexSpeed | Write speed | Average value of write speed of ES cluster in the statistical period | Average value of write speed of ES cluster | Writes/sec | 60s, 300s |
| SearchCompletedSpeed | Query speed | Average value of query speed of ES cluster in the statistical period | Average value of query speed of ES cluster | Queries/sec | 60s, 300s |
| BulkRejectedCompletedPercent | Bulk rejection rate | Percentage of rejected bulk operations to all bulk operations in ES cluster in the statistical period | Percentage of rejected bulk operations to all bulk operations | % | 60s, 300s |
| SearchRejectedCompletedPercent | Query rejection rate | Percentage of rejected query operations to all query operations in ES cluster in the statistical period | Percentage of rejected query operations to all query operations | % | 60s, 300s |
| IndexDocs | Documents | Average number of documents in ES cluster in the statistical period | Number of documents in ES cluster | - | 60s, 300s |
| AutoSnapshotStatus | Automatic backup task execution status in ES cluster | Status of the last automatic backup task execution in ES cluster in the statistical period | Automatic backup task execution status in ES cluster | - | 300s |



## 3. Output Parameters

| Parameter Name | Type | Description |
| ---------- | --------------------- | ------------------------------------------------------------ |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues |

## 4. Samples

### Sample 1 

This example shows you how to get the average disk utilization of one ES cluster using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CES
&MetricName=DiskUsageAvg
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=uInstanceId
&Instances.0.Dimensions.0.Value=es-example
&<Common request parameters>
```

#### Output sample code

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

### Sample 2 

This example shows you how to get the average disk utilization of multiple ES clusters using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

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
&<Common request parameters>
```

#### Output sample code

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