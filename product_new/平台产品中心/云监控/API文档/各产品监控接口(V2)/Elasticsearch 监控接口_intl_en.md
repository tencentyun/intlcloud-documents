## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metrics.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of Elasticsearch Service, use the following input parameters:
&Namespace=QCE/CES
&Instances.N.Dimensions.0.Name=uInstanceId
&Instances.N.Dimensions.0.Value=es-example

## 2. Input Parameters

The list below contains only the API request parameters and some common request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. Value: GetMonitorData |
| Version | Yes | String | Common parameter. Value: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, see the [list of regions](https://intl.cloud.tencent.com/document/product/845/32206) supported by Elasticsearch Service |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/CES for Elasticsearch Service. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :---------- | :----------- | :-------------------------------------- |
| Instances.N.Dimensions.0.Name | uInstanceId | Elasticsearch Service instance ID | Enter a string-type dimension name, such as uInstanceId |
| Instances.N.Dimensions.0.Value | uInstanceId | Elasticsearch Service instance ID | Enter a specific instance ID, such as es-example |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Calculation Method | Meaning | Unit | Statistical Granularity (Period) |
| :----------------------------- | :------------------------- | :------------------------------------------------------- | :----------------------------------- | :------ | :----------------- |
| Status | Cluster health status | Latest value of the Elasticsearch Service cluster in the statistical period | Cluster health condition. 0: green. 1: yellow. 2: red | - | 60s and 300s |
| DiskUsageAvg | Average disk utilization | Average disk utilization of each node in the Elasticsearch Service cluster in the statistical period | Average disk utilization of each node in the Elasticsearch Service cluster | % | 60s and 300s |
| DiskUsageMax | Maximum disk utilization | Maximum disk utilization of each node in the Elasticsearch Service cluster in the statistical period | Maximum disk utilization of each node in the Elasticsearch Service cluster | % | 60s and 300s |
| JvmMemUsageAvg | Average JVM memory utilization | Average JVM memory utilization of each node in the Elasticsearch Service cluster in the statistical period | Average JVM memory utilization of each node in the Elasticsearch Service cluster | % | 60s and 300s |
| JvmMemUsageMax | Maximum JVM memory utilization | Maximum JVM memory utilization of each node in the Elasticsearch Service cluster in the statistical period | Maximum JVM memory utilization of each node in the Elasticsearch Service cluster | % | 60s and 300s |
| CpuUsageAvg | Average CPU utilization | Average CPU utilization of each node in the Elasticsearch Service cluster in the statistical period | Average CPU utilization of each node in the Elasticsearch Service cluster | % | 60s and 300s |
| CpuUsageMax | Maximum CPU utilization | Maximum CPU utilization of each node in the Elasticsearch Service cluster in the statistical period | Maximum CPU utilization of each node in the Elasticsearch Service cluster | % | 60s and 300s |
| CpuLoad1minAvg | Average cluster CPU load per minute | Average CPU load per minute of each node in the Elasticsearch Service cluster during the statistical period | Average CPU load per minute of each node in the Elasticsearch Service cluster  | - | 60s and 300s |
| CpuLoad1minMax | Maximum cluster CPU load per minute | Maximum CPU load per minute of each node in the Elasticsearch Service cluster during the statistical period | Maximum CPU load per minute of each node in the Elasticsearch Service cluster | - | 60s and 300s |
| IndexLatencyAvg | Average write latency | Average write latency of the Elasticsearch Service cluster in the statistical period | Average write latency of the Elasticsearch Service cluster | ms | 60s and 300s |
| IndexLatencyMax | Maximum write latency | Maximum write latency of the Elasticsearch Service cluster in the statistical period | Maximum write latency of the Elasticsearch Service cluster | ms | 60s and 300s |
| SearchLatencyAvg | Average query latency | Average query latency of the Elasticsearch Service cluster in the statistical period | Average query latency of the Elasticsearch Service cluster | ms | 60s and 300s |
| SearchLatencyMax | Maximum query latency | Maximum query latency of the Elasticsearch Service cluster in the statistical period | Maximum query latency of the Elasticsearch Service cluster | ms | 60s and 300s |
| IndexSpeed | Write speed | Average write speed of the Elasticsearch Service cluster in the statistical period | Average write speed of the Elasticsearch Service cluster | Writes/sec | 60s and 300s |
| SearchCompletedSpeed | Query speed | Average query speed of the Elasticsearch Service cluster in the statistical period | Average query speed of the Elasticsearch Service cluster | Queries/sec | 60s and 300s |
| BulkRejectedCompletedPercent | Bulk rejection rate | Percentage of rejected bulk operations to all bulk operations in the Elasticsearch Service cluster in the statistical period | Percentage of rejected bulk operations to all bulk operations | % | 60s and 300s |
| SearchRejectedCompletedPercent | Query rejection rate | Percentage of rejected query operations to all query operations in the Elasticsearch Service cluster in the statistical period | Percentage of rejected query operations to all query operations | % | 60s and 300s |
| IndexDocs | Documents | Average number of documents in the Elasticsearch Service cluster during the statistical period | Number of documents in the Elasticsearch Service cluster | - | 60s and 300s |
| AutoSnapshotStatus | Running status of the automatic backup task in the Elasticsearch Service cluster | Status of the last executed automatic backup task in the Elasticsearch Service cluster in the statistical period | Running status of the automatic backup task in the Elasticsearch Service cluster | - | 300s |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique request ID. Each request returns a unique ID. RequestId is required to troubleshoot issues |

## 4. Samples

### Sample 1

This example shows you how to get the monitoring data for the average disk utilization of one ES cluster using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



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

#### Sample output code



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

This example shows you how to get the monitoring data for the average disk utilization of multiple ES clusters using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



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

#### Sample output code



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