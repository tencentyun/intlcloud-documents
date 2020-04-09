## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a CMQ topic subscription, use the following input parameters:

&Namespace= QCE/CMQTOPIC

&Instances.N.Dimensions.0.Name=topicId

&Instances.N.Dimensions.0.Value=CMQ topic ID


## 2. Input Parameters


The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters
#### 2.1.1. Overview of input parameters
| Parameter Name | Required | Type | Description |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace such as `QCE/CMQTOPIC`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | topicId | CMQ topic ID | String-type dimension name: topicId |
| Instances.N.Dimensions.0.Value | topicId | Specific CMQ topic ID | Specific topic name, such as topic-i4p4k0u0 |
| Instances.N.Dimensions.1.Name | subscriptionId | CMQ subscription ID | String-type dimension name: subscriptionId |
| Instances.N.Dimensions.1.Value | subscriptionId | The input parameter is CMQ subscription ID, which is required if the dimension corresponding to the metric in [Metric name](#Metric name) is `topicId` or `subscriptionId` | Specific `subscriptionId`, such as test1 |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit | Dimension |
| ------------------------ | ----------- | ---- | ---------------------- |
| NumOfMsgPublished | Published messages | - | topicId |
| NumOfMsgBatchPublished | Batch published messages | - | topicId |
| CountOfMsgPublished | Requests for published messages | - | topicId |
| CountOfMsgBatchPublished | Requests for batch published messages | - | topicId |
| PublishSize | Size of published messages | MB | topicId |
| BatchPublishSize | Size of batch published messages | MB | topicId |
| MsgHeapNum | Backlogged messages | - | topicId |
| LanOuttraffic | Outbound traffic of private network requests | MB | topicId |
| WanOuttraffic | Outbound traffic of public network requests | MB | topicId |
| NumOfNotify | Total delivered messages | - | topicId, subscriptionId |
| NumOfSuccNotify | Successfully delivered messages | - | topicId, subscriptionId |


## 3. Output Parameters

| Parameter Name | Type | Description |
| ---------- | --------------------- | ---------------------------------------- |
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

### Sample 1. Getting the number of published messages in one CMQ topic subscription
This example shows you how to get the number of published messages in one CMQ topic subscription using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/CMQTOPIC
&MetricName=NumOfMsgPublished
&Period=60
&StartTime=2019-05-28T10:40:00+08:00
&EndTime=2019-05-28T10:45:00+08:00
&Instances.0.Dimensions.0.Name=topicId
&Instances.0.Dimensions.0.Value=topic-abcd1234
&[<Common request parameters>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-28 10:40:00",
"EndTime": "2019-05-28 10:45:00",
"Period": 60,
"MetricName": "NumOfMsgPublished",
"DataPoints": [
{
"Dimensions": [
{
"Name": "topicId",
"Value": "topic-abcd1234"
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
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "651034c3-b1ea-4ca4-993d-da91bbd70b61"
}
}
```
### Sample 2. Getting the number of published messages in multiple CMQ topic subscriptions
This example shows you how to get the number of published messages in multiple CMQ topic subscriptions using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CMQTOPIC
&MetricName=NumOfMsgPublished
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=topicId
&Instances.0.Dimensions.0.Value=topic-abcd1234
&Instances.1.Dimensions.0.Name=topicId
&Instances.1.Dimensions.0.Value=topic-abcd12345
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-28 10:40:00",
"EndTime": "2019-05-28 10:45:00",
"Period": 60,
"MetricName": "NumOfMsgPublished",
"DataPoints": [
{
"Dimensions": [
{
"Name": "topicId",
"Value": "topic-abcd1234"
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
0,
0,
0,
0,
0,
0
]
},
{
"Dimensions": [
{
"Name": "topicId",
"Value": "topic-abcd12345"
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
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "651034c3-b1ea-4ca4-993d-da91bbd70b61"
}
}
```