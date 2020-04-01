## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the health monitoring data of a GAAP acceleration origin server, use the following input parameters:

&Namespace=QCE/QAAP 

&Instances.N.Dimensions.0.Name=channelId 

&Instances.N.Dimensions.0.Value=channel ID 


## 2. Input Parameters


The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters
#### 2.1.1. Overview of input parameters
| Parameter Name | Required | Type | Description |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/QAAP`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | channelId | Acceleration channel ID | String-type dimension name: channelId |
| Instances.N.Dimensions.0.Value | channelId | Acceleration channel ID | Specific channel ID, such as link-abcd1234 |
| Instances.N.Dimensions.1.Name | listenerId | Listener ID | String-type dimension name: listenerId |
| Instances.N.Dimensions.1.Value | listenerId | Listener ID | Specific listener ID, such as listener-1234abcd |
| Instances.N.Dimensions.2.Name | originServerInfo | Origin server information | String-type dimension name: originServerInfo |
| Instances.N.Dimensions.2.Value | originServerInfo | Origin server information | Origin server IP or domain name, such as www.test.com |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit |
| --- | --- | ---|
| ListenerRsStatus | Origin server health status from the listener (0: exceptional, 1: normal) | - |



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

### Sample 1. Getting the health monitoring data of one GAAP origin server from the listener
This example shows you how to get the health monitoring data of one GAAP origin server from the listener using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/QAAP 
&MetricName=ListenerRsStatus
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=channelId
&Instances.0.Dimensions.0.Value=link-6qmx1234
&Instances.0.Dimensions.1.Name=listenerId
&Instances.0.Dimensions.1.Value=listener-00ABCD12
&Instances.0.Dimensions.2.Name=originServerInfo
&Instances.0.Dimensions.2.Value=11.110.111.111
&[<Common request parameters>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-08 16:40:00",
"EndTime": "2019-05-08 16:45:00",
"Period": 60,
"MetricName": "ListenerRsStatus",
"DataPoints": [
{
"Dimensions": [
{
"Name": "channelId",
"Value": "link-6qmx1234"
},
{
"Name": "listenerId",
"Value": "listener-00ABCD12"
},
{
"Name": "originServerInfo",
"Value": "11.110.111.111"
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
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
}
}
```
### Sample 2. Getting the health monitoring data of multiple GAAP origin servers from the listener
This example shows you how to get the health monitoring data of multiple GAAP origin servers from the listener using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/QAAP
&MetricName=ListenerRsStatus
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=channelId
&Instances.0.Dimensions.0.Value=link-6qmx1234
&Instances.0.Dimensions.1.Name=listenerId
&Instances.0.Dimensions.1.Value=listener-00ABCD12
&Instances.0.Dimensions.2.Name=originServerInfo
&Instances.0.Dimensions.2.Value=11.110.111.111
&Instances.1.Dimensions.0.Name=channelId
&Instances.1.Dimensions.0.Value=link-6qmx12345
&Instances.1.Dimensions.1.Name=listenerId
&Instances.1.Dimensions.1.Value=listener-00ABCD45
&Instances.1.Dimensions.2.Name=originServerInfo
&Instances.1.Dimensions.2.Value=cloud.tencent.com
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-08 16:40:00",
"EndTime": "2019-05-08 16:45:00",
"Period": 60,
"MetricName": "ListenerRsStatus",
"DataPoints": [
{
"Dimensions": [
{
"Name": "channelId",
"Value": "link-6qmx1234"
},
{
"Name": "listenerId",
"Value": "listener-00ABCD12"
},
{
"Name": "originServerInfo",
"Value": "11.110.111.111"
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
0,
0,
0,
0,
0,
0
]
}，
{
"Dimensions": [
{
"Name": "channelId",
"Value": "link-6qmx12345"
},
{
"Name": "diskId",
"Value": "listener-00ABCD45"
},
{
"Name": "diskId",
"Value": "cloud.tencent.com"
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
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
}
}
```