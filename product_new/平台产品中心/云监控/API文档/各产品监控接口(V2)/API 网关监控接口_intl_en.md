## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 
API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.
This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.
To query the monitoring data of an API gateway, use the following input parameters:
`QCE/APIGATEWAY` supports querying monitoring data based on the following combinations of dimensions. The values for input parameters are as follows:

### 1.1. Values of input parameters in environment dimension

&Namespace=QCE/APIGATEWAY
&Instances.N.Dimensions.0.Name=serviceId
&Instances.N.Dimensions.0.Value=serviceId value
&Instances.N.Dimensions.1.Name=environmentName
&Instances.N.Dimensions.1.Value=environmentname

### 1.2. Values of input parameters in API dimension

&Namespace=QCE/APIGATEWAY
&Instances.N.Dimensions.0.Name=serviceId
&Instances.N.Dimensions.0.Value=serviceId value
&Instances.N.Dimensions.1.Name=environmentName
&Instances.N.Dimensions.1.Value=environmentname
&Instances.N.Dimensions.2.Name=apiid
&Instances.N.Dimensions.2.Value=API ID

### 1.3. Values of input parameters in key pair dimension (whitelisted users only)

&Namespace=QCE/APIGATEWAY
&Instances.N.Dimensions.0.Name=serviceId
&Instances.N.Dimensions.0.Value=serviceId value
&Instances.N.Dimensions.1.Name=environmentName
&Instances.N.Dimensions.1.Value=environmentname
&Instances.N.Dimensions.2.Name=key
&Instances.N.Dimensions.2.Value=secretid of key pair

## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/APIGATEWAY`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------- | --------------- | -------------------- | ---------------------------------------- |
| &Instances.N.Dimensions.0.Name | serviceId | API gateway ID | String-type dimension name: serviceId |
| &Instances.N.Dimensions.0.Value | serviceId | API gateway ID | Specific IP address |
| &Instances.N.Dimensions.1.Name | environmentName | Environment name | String-type dimension name: environmentName |
| &Instances.N.Dimensions.1.Value | environmentName | Environment name | Environment name. Valid values: release, test, repub |
| &Instances.N.Dimensions.2.Name | apiid/key | API ID or key pair | String-type dimension name: apiid/key |
| &Instances.N.Dimensions.2.Value | apiid/secretid | API ID or public key of key pair | Specific `apiid` or `secretid` (in key dimension) |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit |
| ---------------------- | -------------- | ---- |
| ResponseTime | Response time | ms |
| ClientError | Frontend errors | - |
| ServerError | Backend errors | - |
| ConcurrentConnections | Concurrent connections | - |
| OutTraffic | Layer-7 public network outbound traffic | MB |
| NumOfReq | Requests | - |
| ApiServerError404 | Backend 404 errors | - |
| ApiServerError502 | Backend 502 errors | - |

## 3. Output Parameters

| Parameter Name | Type | Description |
| ---------- | --------------------- | ------------------------------------------------------------ |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues |

## 4. Error Codes

| Error Code | Error Description | Error Message |
| -------- | -------------- | ------------------------------------ |
| -502 | The resource does not exist. | OperationDenied.SourceNotExists |
| -503 | Incorrect request parameter. | InvalidParameter |
| -505 | Missing parameter. | InvalidParameter.MissingParameter |
| -507 | Limit exceeded. | OperationDenied.ExceedLimit |
| -509 | Incorrect combination of dimensions. | InvalidParameter.DimensionGroupError |
| -513 | Database operation failed. | InternalError.DBoperationFail |

## 5. Samples

#### Sample 1 

This example shows you how to get the response time data of one API gateway using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/APIGATEWAY
&MetricName=ResponseTime
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=serviceId
&Instances.0.Dimensions.0.Value=service-12345jy
&Instances.0.Dimensions.1.Name=environmentName
&Instances.0.Dimensions.1.Value=release
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-29 15:00:00",
"EndTime": "2019-05-29 15:05:00",
"Period": 60,
"MetricName": "ResponseTime",
"DataPoints": [
{
"Dimensions": [
{
"Name": "environmentName",
"Value": "release"
},
{
"Name": "serviceId",
"Value": "service-12345jy"
}
],
"Timestamps": [
1559113200,
1559113260,
1559113320,
1559113380,
1559113440,
1559113500
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
"RequestId": "ba03fcf5-1dc9-483d-9b6b-86d6cb49be44"
}
}
```

#### Sample 2

This example shows you how to get the response time data of multiple API gateways using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/APIGATEWAY
&MetricName=ResponseTime
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=serviceId
&Instances.0.Dimensions.0.Value=service-12345jy
&Instances.0.Dimensions.1.Name=environmentName
&Instances.0.Dimensions.1.Value=release1
&Instances.1.Dimensions.0.Name=serviceId
&Instances.1.Dimensions.0.Value=service-12345cd
&Instances.1.Dimensions.0.Name=environmentName
&Instances.1.Dimensions.0.Value=release2
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-29 15:00:00",
"EndTime": "2019-05-29 15:05:00",
"Period": 60,
"MetricName": "ResponseTime",
"DataPoints": [
{
"Dimensions": [
{
"Name": "environmentName",
"Value": "release1"
},
{
"Name": "serviceId",
"Value": "service-12345jy"
}
],
"Timestamps": [
1559113200,
1559113260,
1559113320,
1559113380,
1559113440,
1559113500
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
"Name": "environmentName",
"Value": "release2"
},
{
"Name": "serviceId",
"Value": "service-12345cd"
}
],
"Timestamps": [
1559113200,
1559113260,
1559113320,
1559113380,
1559113440,
1559113500
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
"RequestId": "4edabba1-69f1-471b-ab04-695aeb23dc7a"
}
}
```