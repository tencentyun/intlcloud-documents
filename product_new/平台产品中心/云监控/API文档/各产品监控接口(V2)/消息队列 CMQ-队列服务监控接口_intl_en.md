## 1. API Description

API: GetMonitorData
Domain name for API request: monitor.tencentcloudapi.com

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend that you spread the call requests over time.

To query the monitoring data of a CMQ queue, use the following input parameters:
&Namespace= QCE/CMQ
&Instances.N.Dimensions.0.Name=queueId
&Instances.N.Dimensions.0.Value=CMQ queue ID
&Instances.N.Dimensions.1.Name=queueName
&Instances.N.Dimensions.1.Value=CMQ queue name

## 2. Input Parameters

The list below contains only API request parameters and certain common parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Params](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [region list](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/CMQ`, which must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :-------- | :---------------------- | :---------------------------------- |
| Instances.N.Dimensions.0.Name | queueId | CMQ queue ID | String-type dimension name: queueId |
| Instances.N.Dimensions.0.Value | queueId | Specific CMQ queue ID | Specific `queueId`, such as queue-3abkyggi |
| Instances.N.Dimensions.1.Name | queueName | CMQ queue name | String-type dimension name: queueName |
| Instances.N.Dimensions.1.Value | queueName | Specific CMQ queue name | Specific `queueName`, such as test1 |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the period and dimension supported by each metric.

| Metric Name | Description | Unit | Dimension |
| :------------------- | :------------------- | :--- | :----------------- |
| InvisibleMsgNum | Invisible messages in queue | Count | queueId, queueName |
| VisibleMsgNum | Visible messages in queue | Count | queueId, queueName |
| SendMsgReqCount | Requests for sending messages | Count | queueId, queueName |
| SendMsgNum | Sent messages | Count | queueId, queueName |
| RecvMsgReqCount | Requests for receiving messages | Count | queueId, queueName |
| RecvMsgNum | Received messages | Count | queueId, queueName |
| RecvNullMsgNum | Received empty messages | Count | queueId, queueName |
| BatchRecvNullMsgNum | Batch received empty messages | Count | queueId, queueName |
| DelMsgReqCount | Requests for deleting messages | Count | queueId, queueName |
| DelMsgNum | Deleted messages | Count | queueId, queueName |
| SendMsgSize | Size of sent messages | MB | queueId, queueName |
| BatchSendMsgSize | Size of batch sent messages | MB | queueId, queueName |
| BatchSendMsgReqCount | Requests for batch sending messages | Count | queueId, queueName |
| BatchRecvMsgReqCount | Requests for batch receiving messages | Count | queueId, queueName |
| BatchDelMsgReqCount | Requests for batch deleting messages | Count | queueId, queueName |
| MsgHeapNum | Heaped messages | Count | queueId, queueName |
| LanOuttraffic | Outbound traffic of private network requests | MB | queueId, queueName |
| WanOuttraffic | Outbound traffic of public network requests | MB | queueId, queueName |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique request ID, which is returned in each request. The `RequestId` is required to troubleshoot issues |

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

### Sample 1. Getting the number of invisible messages in one CMQ queue

This example shows you how to get the monitoring data for the number of invisible messages in one CMQ queue using a statistical period of 300 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/CMQ
&MetricName=InvisibleMsgNum
&Period=300
&StartTime=2019-05-08T10:40:00+08:00
&EndTime=2018-05-08T10:50:00+08:00
&Instances.0.Dimensions.0.Name=queueId
&Instances.0.Dimensions.0.Value=queue-123456
&Instances.0.Dimensions.1.Name=queueName
&Instances.0.Dimensions.1.Value=queue_abcdef
&[<Common request parameters>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### Output sample code

```
{
  "Response": {
    "StartTime": "2019-05-08 10:40:00",
    "EndTime": "2019-05-08 10:50:00",
    "Period": 300,
    "MetricName": "InvisibleMsgNum",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "queueId",
            "Value": "queue-123456"
          },
          {
            "Name": "queueName",
            "Value": "queue_abcdef"
          }
        ],
        "Timestamps": [
          1559011200,
          1559011500,
          1559011800
        ],
        "Values": [
          0,
          0,
          0
        ]
      }
    ],
    "RequestId": "e1440ace-c2a2-4e93-8110-8dcaefdd4f1a"
  }
}
```

### Sample 2. Getting the number of invisible messages in multiple CMQ queues

This example shows you how to get the monitoring data for the number of invisible messages in multiple CMQ queues using a statistical period of 300 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CMQ
&MetricName=InvisibleMsgNum
&Period=300
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=queueId
&Instances.0.Dimensions.0.Value=queue-123456
&Instances.0.Dimensions.1.Name=queueName
&Instances.0.Dimensions.1.Value=queue_abcdef
&Instances.1.Dimensions.0.Name=queueId
&Instances.1.Dimensions.0.Value=queue-1234567
&Instances.1.Dimensions.1.Name=queueName
&Instances.1.Dimensions.1.Value=queue_abcdefg
&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "StartTime": "2019-05-08 10:40:00",
    "EndTime": "2019-05-08 10:50:00",
    "Period": 300,
    "MetricName": "InvisibleMsgNum",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "queueId",
            "Value": "queue-123456"
          },
          {
            "Name": "queueName",
            "Value": "queue_abcdef"
          }
        ],
        "Timestamps": [
          1559011200,
          1559011500,
          1559011800
        ],
        "Values": [
          0,
          0,
          0
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "queueId",
            "Value": "queue-1234567"
          },
          {
            "Name": "queueName",
            "Value": "queue_abcdefg"
          }
        ],
        "Timestamps": [
          1559011200,
          1559011500,
          1559011800
        ],
        "Values": [
          0,
          0,
          0
        ]
      }
    ],
    "RequestId": "e1440ace-c2a2-4e93-8110-8dcaefdd4f1a"
  }
}
```