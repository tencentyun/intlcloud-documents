## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API can be used to get the monitoring data of **Redis 2.8 Cluster Edition, CKV Standard Edition, and CKV Cluster Edition**. It is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points. This API may fail due to the rate limit if you need to call many metrics and objects. We recommend that you distribute call requests across a period of time.

To query the monitoring data of a TencentDB for Redis instance, use the following input parameters:
&Namespace= QCE/REDIS
&Instances.N.Dimensions.0.Name=redis_uuid
&Instances.N.Dimensions.0.Value=instance uuid

## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1 Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/product/239/32045) supported by TencentDB for Redis |
| Namespace | Yes | String | Namespace. Each Tencent Cloud service has a namespace, such as QCE/REDIS for TencentDB for Redis. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :--------- | :----------- | :------------------------------------- |
| Instances.N.Dimensions.0.Name | redis_uuid | Instance ID | Enter a string-type dimension name, such as redis_uuid |
| Instances.N.Dimensions.0.Value | redis_uuid | Specific instance ID | Enter a specific TencentDB for Redis instance ID, such as crs-123456 |

### 2.2. Metric names

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

| Metric | Name | Metric Collecting Method (Meaning in Linux) | Metric Statistical Method | Unit |
| :--------- | :---------- | :----------------------------------------------------------- | :----------------------------------------------- | :------ |
| Total requests | Qps | Total number of commands within 1 minute divided by 60 | This metric is collected once every minute, and its value at the 5-minute granularity is the average in the last 5 minutes | Times/sec |
| Connections | Connections | Total number of connections within 1 minute | This metric is collected once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | - |
| CPU utilization | CpuUs | Percentage of time during which the CPU is occupied, which is calculated by obtaining data /proc/stat | This metric is collected once every minute, and its value at the 5-minute granularity is the average in the last 5 minutes | % |
| Inbound traffic | InFlow | Sum of inbound traffic within 1 minute | This metric is collected once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | MB/min |
| Total keys | Keys | Maximum number of keys within 1 minute | This metric is collected once every minute, and its value at the 5-minute granularity is the maximum in the last 5 minutes| - |
| Outbound traffic | OutFlow | Sum of outbound traffic within 1 minute | This metric is collected once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | MB/min |
| Write requests | StatGet | Number of get/hget/hgetall/hmget/mget/getbit/getrange command requests within 1 minute | This metric is collected once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Times/min |
| Read requests | StatSet | Number of set/hset/hmset/hsetnx/lset/mset/msetnx/setbit/setex/setrange/setnx command requests within 1 minute | This metric is collected once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Times/min |
| Memory usage | Storage | Maximum occupied capacity within 1 minute | This metric is collected once every minute, and its value at the 5-minute granularity is the maximum in the last 5 minutes | MB/min |
| Memory utilization | StorageUs | Maximum percentage of the occupied capacity within 1 minute | This metric is collected once every minute, and its value at the 5-minute granularity is the maximum in the last 5 minutes | % |

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

## 5. Online Debugging

You can use the [online debugging tool](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=GetMonitorData&SignVersion=) to debug the API.

## 6. Samples

### Sample 1

This example shows you how to get the monitoring data for the number of connections of one TencentDB for Redis instance using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/REDIS
&MetricName=Connections
&Period=60
&StartTime=2019-06-04T00:00:00+08:00
&EndTime=2019-06-04T00:05:00+08:00
&Instances.0.Dimensions.0.Name=redis_uuid
&Instances.0.Dimensions.0.Value=crs-123456
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-06-04 00:00:00",
    "EndTime": "2019-06-04 00:05:00",
    "Period": 60,
    "MetricName": "Connections",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "redis_uuid",
            "Value": "crs-123456"
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
          3,
          3,
          4.5,
          3,
          3
        ]
      }
    ],
    "RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
  }
}
```

### Sample 2

This example shows you how to get the monitoring data for the number of connections of multiple TencentDB for Redis instances using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/REDIS
&MetricName=Connections
&Period=60
&StartTime=2019-06-04T00:00:00+08:00
&EndTime=2019-06-04T00:05:00+08:00
&Instances.0.Dimensions.0.Name=redis_uuid
&Instances.0.Dimensions.0.Value=crs-123456
&Instances.1.Dimensions.0.Name=redis_uuid
&Instances.1.Dimensions.0.Value=crs-1234567
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-06-04 00:00:00",
    "EndTime": "2019-06-04 00:05:00",
    "Period": 60,
    "MetricName": "Connections",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "redis_uuid",
            "Value": "crs-123456"
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
          3,
          3,
          4.5,
          3,
          3
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "redis_uuid",
            "Value": "crs-1234567"
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
          3,
          3,
          4.5,
          3,
          3
        ]
      }
    ],
    "RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
  }
}
```