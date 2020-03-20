## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of an SCF function, use the following input parameters:

&Namespace=QCE/SCF_V2

&Instances.N.Dimensions.0.Name=functionName

&Instances.N.Dimensions.0.Value=test


## 2. Input Parameters


The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters
#### 2.1.1. Overview of input parameters
| Parameter Name | Required | Type | Description |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/SCF_V2`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `EndTime` cannot be earlier than `StartTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | functionName | Function name | String-type dimension name: functionName |
| Instances.N.Dimensions.0.Value | functionName | Specific function name | Specific instance name, such as test |
| Instances.N.Dimensions.0.Name | version | Function version | String-type dimension name: functionName |
| Instances.N.Dimensions.0.Value | version | Specific function version | Specific instance version, such as $latest |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit |
|---------|---------|---------|
| Duration | Execution duration | ms |
| Invocation | Invocations | - |
| Error | Invocation errors | - |
| ConcurrentExecutions | Concurrent executions | - |
| ConfigMem | Configured memory | MB |
| FunctionErrorPercentage | Function error rate | % |
| Http2xx | Correct invocations | - |
| Http432 | Errors where resource limit is exceeded | - |
| Http433 | Errors where function execution timed out | - |
| Http434 | Errors where memory limit is exceeded | - |
| Http4xx | Function errors | - |
| Invocation | Function invocations | - |
| Mem | Operating memory | MB |
| MemDuration | Time memory | MB/ms |
| OutFlow | Public network outbound traffic | - |
| ServerErrorPercentage | Platform error rate | % |
| Syserr | Internal system errors | - |
| Throttle | Throttled function executions | - |


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

### Sample 1. Getting the execution duration monitoring data of one function
This example shows you how to get the execution duration data of one function using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/SCF_V2
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=functionName
&Instances.0.Dimensions.0.Value=test1
&Instances.0.Dimensions.1.Name=version
&Instances.0.Dimensions.1.Value=$latest
&[<Common request parameters>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-08 16:40:00",
"EndTime": "2019-05-08 16:45:00",
"Period": 60,
"MetricName": "Duration",
"DataPoints": [
{
"Dimensions": [
{
"Name": "functionName",
"Value": "test"
},
{
"Name": "version",
"Value": "$latest"
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
0.105,
0.1,
0.071,
0.295,
0.096,
0.098
]
}
],
"RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
}
}
```
### Sample 2. Getting the execution duration monitoring data of multiple functions
This example shows you how to get the execution duration data of multiple functions using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/SCF_V2
&MetricName=Duration
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=functionName
&Instances.0.Dimensions.0.Value=test1
&Instances.0.Dimensions.1.Name=version
&Instances.0.Dimensions.1.Value=$latest
&Instances.1.Dimensions.0.Name=functionName
&Instances.1.Dimensions.0.Value=test2
&Instances.1.Dimensions.1.Name=version
&Instances.1.Dimensions.1.Value=$latest

&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-08 16:40:00",
"EndTime": "2019-05-08 16:45:00",
"Period": 60,
"MetricName": "Duration",
"DataPoints": [
{
"Dimensions": [
{
"Name": "functionName",
"Value": "test"
},
{
"Name": "version",
"Value": "$latest"
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
0.105,
0.1,
0.071,
0.295,
0.096,
0.098
]
}，
{
"Dimensions": [
{
"Name": "functionName",
"Value": "test2"
},
{
"Name": "version",
"Value": "$latest"
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
0.105,
0.1,
0.071,
0.295,
0.096,
0.098
]
}
],
"RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
}
}
```