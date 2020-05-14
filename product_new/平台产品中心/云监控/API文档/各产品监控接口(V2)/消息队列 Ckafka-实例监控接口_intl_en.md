## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metrics.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a CKafka instance, use the following input parameters:
&Namespace=QCE/CKAFKA
&Instances.N.Dimensions.0.Name=instanceId
&Instances.N.Dimensions.0.Value=instance ID

## 2. Input Parameters

The list below contains only the API request parameters and some common request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1 Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. Value: GetMonitorData |
| Version | Yes | String | Common parameter. Value: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, see the [list of regions](https://intl.cloud.tencent.com/document/product/597/35335#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by Ckafka |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/CKAFKA for CKafka instances. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :--------- | :--------------- | :-------------------------------------- |
| Instances.N.Dimensions.0.Name | instanceId | CKafka instance ID | Enter a string-type dimension name, such as instanceId |
| Instances.N.Dimensions.0.Value | instanceId | CKafka instance ID | Enter a specific instance ID, such as ckafka-test |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit | Dimension |
| :------------------ | :----------------- | :----------------------------------------------- | :--------- |
| InstanceMsgHeap | Message heap in the instance | MB | instanceId |
| InstanceProCount | Messages produced by the instance | - | instanceId |
| InstanceConCount | Messages consumed by the instance | - | instanceId |
| InstanceProReqCount | Production requests in the instance | - | instanceId |
| InstanceConReqCount | Consumption requests in the instance | - | instanceId |
| InstanceMsgCount | Persistent messages in the instance | - | instanceId |
| InstanceProFlow | Production traffic in the instance | MB/min | instanceId |
| InstanceConFlow | Consumption traffic in the instance | MB/min | instanceId |
| InstanceDiskUsage | Instance disk utilization | None. This metric indicates the ratio of the currently used disk capacity to the total disk capacity | instanceId |
| InstanceMaxConFlow | Maximum consumption traffic in the instance | MB/s | instanceId |
| InstanceMaxProFlow | Maximum production traffic in the instance | MB/s | instanceId |

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

This example shows you how to get the monitoring data for the maximum production traffic of one CKafka instance using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CKAFKA
&MetricName=InstanceMaxProFlow
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=instanceId
&Instances.0.Dimensions.0.Value=ckafka-test
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-09 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 60,
    "MetricName": "InstanceMaxProFlow",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "instanceId",
            "Value": "ckafka-test"
          }
        ],
        "Timestamps": [
          1558339260,
          1558339320,
          1558339380,
          1558339440,
          1558339500
        ],
        "Values": [
          10,
          20,
          30,
          40,
          50
        ]
      }
    ],
    "RequestId": "9867f161-c919-4dac-84b4-2e069bd5cd90"
  }
}
```

### Sample 2

This example shows you how to get the monitoring data for the maximum production traffic of multiple CKafka instances using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CKAFKA
&MetricName=InstanceMaxProFlow
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=instanceId
&Instances.0.Dimensions.0.Value=ckafka-test1
&Instances.1.Dimensions.0.Name=instanceId
&Instances.1.Dimensions.0.Value=ckafka-test2
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-08 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 60,
    "MetricName": "InstanceMaxProFlow",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "instanceId",
            "Value": "ckafka-test1"
          }
        ],
        "Timestamps": [
          1558339260,
          1558339320,
          1558339380,
          1558339440,
          1558339500
        ],
        "Values": [
          10,
          20,
          30,
          40,
          50
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "instanceId",
            "Value": "ckafka-test2"
          }
        ],
        "Timestamps": [
          1558339260,
          1558339320,
          1558339380,
          1558339440,
          1558339500
        ],
        "Values": [
          10,
          20,
          30,
          40,
          50
        ]
      }
    ],
    "RequestId": "9867f161-c919-4dac-84b4-2e069bd5cd90"
  }
}
```