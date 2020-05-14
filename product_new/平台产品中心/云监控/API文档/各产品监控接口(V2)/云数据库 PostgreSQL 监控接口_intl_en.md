## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metrics.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of PostgreSQL, use the following input parameters:
&Namespace=QCE/POSTGRES
&Instances.N.Dimensions.0.Name=resourceId
&Instances.N.Dimensions.0.Value=Instance resourceId

## 2. Input Parameters

The list below contains only the API request parameters and some common request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1 Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. Value: GetMonitorData |
| Version | Yes | String | Common parameter. Value: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, see the [list of regions](https://intl.cloud.tencent.com/document/product/409/16764) supported by PostgreSQL |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/POSTGRES for PostgreSQL. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :--------- | :------------------- | :-------------------------------------------- |
| Instances.N.Dimensions.0.Name | resourceId | Instance resourceId | Enter a string-type dimension name, such as resourceId |
| Instances.N.Dimensions.0.Value | resourceId | Specific instance resourceId | Enter a specific instance resourceId, such as postgres-123456 |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit |
| :------------- | :----------------- | :------ |
| Connections | Connections | - |
| Cpu | CPU utilization | % |
| HitPercent | Buffer cache hit rate | % |
| InFlow | Inbound traffic | KB/sec |
| OutFlow | Outbound traffic | KB/sec |
| Iops | Disk IOPS | Times/sec |
| Memory | Memory usage | KB |
| OtherCalls | Other requests | Times/min |
| Qps | Queries per second | Times/sec |
| WriteCalls | Write requests | Times/min |
| ReadCalls | Read requests | Times/min |
| ReadWriteCalls | Read and write requests | Times/min |
| RemainXid | Remaining XIDs | - |
| SqlRuntimeAvg | Average execution latency | ms |
| SqlRuntimeMax | 10 longest execution latencies | ms |
| SqlRuntimeMin | 10 shortest execution latencies | ms |
| Storage | Used storage capacity | GB |
| XlogDiff | Master/Slave XLOG synchronization difference | Bytes |

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

This example shows you how to get the monitoring data for the number of connections of one PostgreSQL instance using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/POSTGRES
&MetricName=Connections
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=resourceId
&Instances.0.Dimensions.0.Value=postgres-123456
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-08 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 60,
    "MetricName": "Connections",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "resourceId",
            "Value": "postgres-123456"
          }
        ],
        "Timestamps": [
          1559011200,
          1559011260,
          1559011320,
          1559011380,
          1559011440,
          1559011500
        ],
        "Values": [
          10,
          10,
          10,
          10,
          10,
          10
        ]
      }
    ],
    "RequestId": "d2141cc8-74e2-4e55-905e-3780d7d654df"
  }
}
```

### Sample 2

This example shows you how to get the monitoring data for the number of connections of multiple PostgreSQL instances using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/BLOCK_STORAGE
&MetricName=Connections
&Period=60
&StartTime=2019-05-28T10:40:00+08:00
&EndTime=2019-05-28T10:45:00+08:00
&Instances.0.Dimensions.0.Name=resourceId
&Instances.0.Dimensions.0.Value=postgres-123456
&Instances.1.Dimensions.0.Name=resourceId
&Instances.1.Dimensions.0.Value=postgres-654321
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-28 10:40:00",
    "EndTime": "2019-05-28 10:45:00",
    "Period": 60,
    "MetricName": "Connections",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "resourceId",
            "Value": "postgres-123456"
          }
        ],
        "Timestamps": [
          1559011200,
          1559011260,
          1559011320,
          1559011380,
          1559011440,
          1559011500
        ],
        "Values": [
          10,
          10,
          10,
          10,
          10,
          10
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "resourceId",
            "Value": "postgres-654321"
          }
        ],
        "Timestamps": [
          1559011200,
          1559011260,
          1559011320,
          1559011380,
          1559011440,
          1559011500
        ],
        "Values": [
          10,
          10,
          10,
          10,
          10,
          10
        ]
      }
    ],
    "RequestId": "d2141cc8-74e2-4e55-905e-3780d7d654df"
  }
}
```