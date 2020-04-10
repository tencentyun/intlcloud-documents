## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a CKafka consumer group, use the following input parameters:

&Namespace=QCE/CKAFKA

&Instances.N.Dimensions.0.Name=consumerGroup

&Instances.N.Dimensions.0.Value=consumer group

&Instances.N.Dimensions.1.Name=instanceId

&Instances.N.Dimensions.1.Value=instance ID

&Instances.N.Dimensions.2.Name=topicId

&Instances.N.Dimensions.2.Value=topic ID

&Instances.N.Dimensions.3.Name=topicName

&Instances.N.Dimensions.3.Value=topic name

&Instances.N.Dimensions.4.Name=partition

&Instances.N.Dimensions.4.Value=partition




## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace such as `QCE/CKAFKA`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ------------- | ------------- | ------------------------------------------------ |
| Instances.N.Dimensions.0.Name | consumerGroup | consumerGroup | String-type dimension name: consumerGroup |
| Instances.N.Dimensions.0.Value | consumerGroup | Consumer group information | Information of the consumer group to be viewed, such as perf-consumer-8330 |
| Instances.N.Dimensions.1.Name | instanceId | instanceId | String-type dimension name: instanceId |
| Instances.N.Dimensions.1.Value | instanceId | Instance ID | ID of the instance for which to view monitoring data, such as ckafka-test |
| Instances.N.Dimensions.2.Name | topicId | topicId | String-type dimension name: topicId |
| Instances.N.Dimensions.2.Value | topicId | Topic ID | ID of the topic subscribed to, such as topic-test |
| Instances.N.Dimensions.3.Name | partition | Partition | String-type dimension name: partition |
| Instances.N.Dimensions.3.Value | partition | Partition information | Partition information of topic, such as 0 |
| Instances.N.Dimensions.4.Name | topicName | topicName | String-type dimension name: topicName |
| Instances.N.Dimensions.5.Value | topicName | Topic name | Name of consumed topic, such as test |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit | Dimension |
| ------------------------ | ------------------------------------------- | ---- | ----------------------------------------------------- |
| CgroupMaxOffset | Maximum offset entries of partition corresponding to consumer group | - | consumerGroup,instanceId,topicId, partition,topicName |
| CtopicMsgOffset | Current offset entries of partition corresponding to consumer group | - | consumerGroup,instanceId,topicId, partition,topicName |
| CtopicUnconsumeMsgCount | Unconsumed messages in partition corresponding to consumer group | - | consumerGroup,instanceId,topicId, partition,topicName |
| CtopicUnconsumeMsgOffset | Size of unconsumed messages in partition corresponding to consumer group | MB | consumerGroup,instanceId,topicId, partition,topicName |



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

This example shows you how to get the size of unconsumed messages in the partition corresponding to one CKafka consumer group using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CKAFKA
&MetricName=CtopicUnconsumeMsgOffset
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=consumerGroup
&Instances.0.Dimensions.0.Value=perf-consumer-8330
&Instances.0.Dimensions.1.Name=instanceId
&Instances.0.Dimensions.1.Value=ckafka-test
&Instances.0.Dimensions.2.Name=topicId
&Instances.0.Dimensions.2.Value=topic-test
&Instances.0.Dimensions.3.Name=topicName
&Instances.0.Dimensions.3.Value=test
&Instances.0.Dimensions.4.Name=partition
&Instances.0.Dimensions.4.Value=0
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-21 20:35:00",
"EndTime": "2019-05-21 20:40:00",
"Period": 60,
"MetricName": "CtopicUnconsumeMsgOffset",
"DataPoints": [
{
"Dimensions": [
{
"Name": "consumerGroup",
"Value": "perf-consumer-8330"
},
{
"Name": "instanceId",
"Value": "ckafka-test"
},
{
"Name": "partition",
"Value": "0"
},
{
"Name": "topicId",
"Value": "topic-test"
},
{
"Name": "topicName",
"Value": "test"
}
],
"Timestamps": [
1558442100,
1558442160,
1558442220,
1558442280,
1558442340,
1558442400
],
"Values": [
906,
910,
913,
917,
921,
925
]
}
],
"RequestId": "c57cb169-606e-4617-a063-12345678910"
}
}
```

### Sample 2 

This example shows you how to get the size of unconsumed messages in the partition corresponding to multiple CKafka consumer groups using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CKAFKA
&MetricName=CtopicUnconsumeMsgOffset
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=consumerGroup
&Instances.0.Dimensions.0.Value=perf-consumer-83301
&Instances.0.Dimensions.1.Name=instanceId
&Instances.0.Dimensions.1.Value=ckafka-test1
&Instances.0.Dimensions.2.Name=topicId
&Instances.0.Dimensions.2.Value=topic-test1
&Instances.0.Dimensions.3.Name=topicName
&Instances.0.Dimensions.3.Value=test1
&Instances.0.Dimensions.4.Name=partition
&Instances.0.Dimensions.4.Value=0
&Instances.1.Dimensions.0.Name=consumerGroup
&Instances.1.Dimensions.0.Value=perf-consumer-83302
&Instances.1.Dimensions.1.Name=instanceId
&Instances.1.Dimensions.1.Value=ckafka-test2
&Instances.1.Dimensions.2.Name=topicId
&Instances.1.Dimensions.2.Value=topic-test2
&Instances.1.Dimensions.3.Name=topicName
&Instances.1.Dimensions.3.Value=test2
&Instances.1.Dimensions.4.Name=partition
&Instances.1.Dimensions.4.Value=1
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-21 20:35:00",
"EndTime": "2019-05-21 20:40:00",
"Period": 60,
"MetricName": "CtopicUnconsumeMsgOffset",
"DataPoints": [
{
"Dimensions": [
{
"Name": "consumerGroup",
"Value": "perf-consumer-83301"
},
{
"Name": "instanceId",
"Value": "ckafka-test1"
},
{
"Name": "partition",
"Value": "1"
},
{
"Name": "topicId",
"Value": "topic-test1"
},
{
"Name": "topicName",
"Value": "test1"
}
],
"Timestamps": [
1558442100,
1558442160,
1558442220,
1558442280,
1558442340,
1558442400
],
"Values": [
906,
910,
913,
917,
921,
925
]
},
{
"Dimensions": [
{
"Name": "consumerGroup",
"Value": "perf-consumer-83302"
},
{
"Name": "instanceId",
"Value": "ckafka-test2"
},
{
"Name": "partition",
"Value": "2"
},
{
"Name": "topicId",
"Value": "topic-test2"
},
{
"Name": "topicName",
"Value": "test2"
}
],
"Timestamps": [
1558442100,
1558442160,
1558442220,
1558442280,
1558442340,
1558442400
],
"Values": [
906,
910,
913,
917,
921,
925
]
}
],
"RequestId": "c57cb169-606e-4617-a063-12345678910"
}
}
```