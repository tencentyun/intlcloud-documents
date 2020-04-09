## 1. API Description

API: GetMonitorData

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 50 calls/second (500 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a CFS file system, use the following input parameters:
&Namespace：QCE/CFS

&Instances.N.Dimensions.0.Name=cfsId

&Instances.N.Dimensions.0.Value=CFS file system ID


## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters
#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace such as `QCE/CFS`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `EndTime` cannot be earlier than `StartTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | cfsId | CFS file system ID | String-type dimension name: cfsId |
| Instances.N.Dimensions.0.Value | cfsId | Specific CFS file system ID | Specific CFS file system ID, such as cfs-fjojeogej |


### 2.2. Metric name

The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` supported by each API.

| Metric Name | Description | Meaning | Unit |
| ------------------|---- | --------- | ---- |
| Storage | CFS file system storage capacity | Current storage capacity of CFS file system | GB |
| DataReadIoBytes | Read bandwidth | Average volume of data read from CFS file system per second | KB/s |
| DataWriteIoBytes | Write bandwidth | Average volume of data written to CFS file system per second | KB/s |
| DataReadIoCount | Read IOPS | Average number of reads from CFS file system per second | Reads/sec |
| DataWriteIoCount | Write IOPS | Average number of writes to CFS file system per second | Writes/sec |

## 3. Output Parameters

| Parameter Name | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of Float | Monitoring data list |
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

### Sample 1 

This example shows you how to get the read bandwidth of one CFS file system using a statistical period of 5 minutes for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CFS
&MetricName=DataReadIoBytes
&Period=300
&StartTime=2019-04-16 20:00:00
&EndTime=2019-04-16 20:05:00
&Instances.0.Dimensions.0.Name=cfsId
&Instances.0.Dimensions.0.Value=cfs-foaejoigr
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-06-05 00:00:00",
"EndTime": "2019-06-05 00:05:00",
"Period": 300,
"MetricName": "DataReadIoBytes",
"DataPoints": [
{
"Dimensions": [
{
"Name": "cfsId",
"Value": "cfs-foaejoigr"
}
],
"Timestamps": [
1555416000,
1559664300
],
"Values": [
1.2,
1.3
]
}
],
"RequestId": "f37c03ce-0f54-492b-a378-78aa268e5d54"
}
}
```



## Sample 2 


This example shows you how to get the read bandwidth of multiple CFS file systems using a statistical period of 5 minutes for a specified length of time.

### Request parameters

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CFS
&MetricName=DataReadIoBytes
&Period=300
&StartTime=2019-06-05T00:00:00+08:00
&EndTime=2019-06-05T00:05:00+08:00
&Instances.0.Dimensions.0.Name=cfsId
&Instances.0.Dimensions.0.Value=cfs-foaejoigr
&Instances.1.Dimensions.0.Name=cfsId
&Instances.1.Dimensions.0.Value=cfs-esasd12da
&<Common request parameters>
```

### Response parameters

```
{
"Response": {
"StartTime": "2019-06-05 00:00:00",
"EndTime": "2019-06-05 00:05:00",
"Period": 300,
"MetricName": "DataReadIoBytes",
"DataPoints": [
{
"Dimensions": [
{
"Name": "cfsId",
"Value": "cfs-foaejoigr"
}
],
"Timestamps": [
1555416000,
1559664300
],
"Values": [
1.2,
1.3
]
},
{
"Dimensions": [
{
"Name": "cfsId",
"Value": "cfs-esasd12da"
}
],
"Timestamps": [
1555416000,
1559664300
],
"Values": [
1.2,
1.3
]
}
],
"RequestId": "f37c03ce-0f54-492b-a378-78aa268e5d54"
}
}
```