## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metrics.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a CKafka topic, use the following input parameters:
&Namespace=QCE/CKAFKA
&Instances.N.Dimensions.0.Name=instanceId
&Instances.N.Dimensions.0.Value=Instance ID
&Instances.N.Dimensions.1.Name=topicId
&Instances.N.Dimensions.1.Value=Topic ID

## 2. Input Parameters

The list below contains only the API request parameters and some common request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1 Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. Value: GetMonitorData |
| Version | Yes | String | Common parameter. Value: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, see the [list of regions](https://intl.cloud.tencent.com/document/product/597/35335#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by Ckafka |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/CKAFKA for Ckafka topics. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :--------- | :---------------- | :-------------------------------------- |
| Instances.N.Dimensions.0.Name | instanceId | instanceId | Enter a string-type dimension name, such as instanceId |
| Instances.N.Dimensions.0.Value | instanceId | CKafka instance ID | Enter a specific instance ID, such as ckafka-test |
| Instances.N.Dimensions.1.Name | topicId | topicId | Enter a string-type dimension name, such as topicId |
| Instances.N.Dimensions.1.Value | topicId | Instance topic ID | Enter a specific topic ID, such as topic-test |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit | Dimension |
| :---------------- | :----------------- | :--- | :----------------- |
| CtopicProFlow | Production traffic in the topic | MB | instanceId, topicId |
| CtopicConFlow | Consumption traffic in the topic | MB | instanceId, topicId |
| CtopicMsgHeap | Message heap in the topic | MB | instanceId, topicId |
| CtopicProCount | Messages produced by the topic | - | instanceId, topicId |
| CtopicProReqCount | Production requests in the topic | - | instanceId, topicId |
| CtopicConReqCount | Consumption requests in the topic | - | instanceId, topicId |
| CtopicMsgCount | Persistent messages in the topic | - | instanceId, topicId |
| CtopicConCount | Messages consumed by the topic | - | instanceId, topicId |

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

This example shows you how to get the monitoring data for the production traffic of one CKafka topic using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CKAFKA
&MetricName=CtopicProFlow
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=instanceId
&Instances.0.Dimensions.0.Value=ckafka-test
&Instances.0.Dimensions.1.Name=topicId
&Instances.0.Dimensions.1.Value=topic-test
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-08 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 60,
    "MetricName": "CtopicProFlow",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "instanceId",
            "Value": "ckafka-test"
          },
          {
            "Name": "topicId",
            "Value": "topic-test"
          }
        ],
        "Timestamps": [
          1558429200,
          1558429260,
          1558429320,
          1558429380,
          1558429440,
          1558429500
        ],
        "Values": [
          18.213,
          18.219,
          17.911,
          18.243,
          17.916,
          17.939
        ]
      }
    ],
    "RequestId": "68a1ffe1-b314-4da8-8f8c-cdcfcff1d3fd"
  }
}
```

### Sample 2

This example shows you how to get the monitoring data for the production traffic of multiple CKafka topics using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CKAFKA
&MetricName=CtopicProFlow
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=instanceId
&Instances.0.Dimensions.0.Value=ckafka-test1
&Instances.0.Dimensions.1.Name=topicId
&Instances.0.Dimensions.1.Value=topic-test1
&Instances.1.Dimensions.0.Name=instanceId
&Instances.1.Dimensions.0.Value=ckafka-test2
&Instances.1.Dimensions.1.Name=topicId
&Instances.1.Dimensions.1.Value=topic-test2
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-08 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 60,
    "MetricName": "CtopicProFlow",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "instanceId",
            "Value": "ckafka-test1"
          },
          {
            "Name": "topicId",
            "Value": "topic-test1"
          }
        ],
        "Timestamps": [
          1558429200,
          1558429260,
          1558429320,
          1558429380,
          1558429440,
          1558429500
        ],
        "Values": [
          18.213,
          18.219,
          17.911,
          18.243,
          17.916,
          17.939
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "instanceId",
            "Value": "ckafka-test2"
          },
          {
            "Name": "topicId",
            "Value": "topic-test2"
          }
        ],
        "Timestamps": [
          1558429200,
          1558429260,
          1558429320,
          1558429380,
          1558429440,
          1558429500
        ],
        "Values": [
          18.213,
          18.219,
          17.911,
          18.243,
          17.916,
          17.939
        ]
      }
    ],
    "RequestId": "68a1ffe1-b314-4da8-8f8c-cdcfcff1d3fd"
  }
}
```