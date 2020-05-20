## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension description, and monitoring metrics.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the monitoring data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend that you distribute call requests across a period of time.

To query the monitoring data of a Direct Connect physical connection, use the following input parameters:
&Namespace=QCE/DC
&Instances.N.Dimensions.0.Name=directConnectId
&Instances.N.Dimensions.0.Value=Direct Connect connection ID

## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | This parameter is not required for this API |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/DC for Direct Connect physical connections. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Dimension parameters

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :------------------ | :----------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.Name | directConnectConnId | Direct Connect connection ID | Enter a string-type dimension name, such as directConnectConnId |
| Instances.N.Dimensions.0.Value | Specific Direct Connect connection ID | Specific Direct Connect connection ID | Enter a specific Direct Connect connection ID. You can call the [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258) API to obtain the unInstanceId field |

### 2.2. Metric names

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit | Supported Dimension |
| :--------------------- | :----- | :--- | :------------------ |
| Inbandwidth | Inbound bandwidth | Bps | directConnectConnId |
| Outbandwidth | Outbound bandwidth | Bps | directConnectConnId |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. RequestId is required to troubleshoot issues |

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

This example shows you how to get the monitoring data for the inbound bandwidth of one Direct Connect physical connection using a statistical period of 300 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/DC
&MetricName=Inbandwidth
&Period=300
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=directConnectId
&Instances.0.Dimensions.0.Value=dc-123456abc
&<Common request parameters>
```

#### Sample output code



```shell
{
  "Response": {
    "StartTime": "2019-05-08 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 300,
    "MetricName": "Inbandwidth",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "directConnectId",
            "Value": "dc-123456abc"
          }
        ],
        "Timestamps": [
          1558459800,
          1558460100
        ],
        "Values": [
          15.6,
          17.9
        ]
      }
    ],
    "RequestId": "23a38f36-5c73-43fb-ae46-12345678"
  }
}
```

### Sample 2

This example shows you how to get the monitoring data for the inbound bandwidth of multiple Direct Connect physical connections using a statistical period of 300 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/DC
&MetricName=Inbandwidth
&Period=300
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=directConnectId
&Instances.0.Dimensions.0.Value=dc-123456abc
&Instances.1.Dimensions.0.Name=directConnectId
&Instances.1.Dimensions.0.Value=dc-123456def
&<Common request parameters>
```

#### Sample output code



```shell
{
  "Response": {
    "StartTime": "2019-05-08 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 300,
    "MetricName": "Inbandwidth",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "directConnectId",
            "Value": "dc-123456abc"
          }
        ],
        "Timestamps": [
          1558459800,
          1558460100
        ],
        "Values": [
          15.6,
          17.9
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "directConnectId",
            "Value": "dc-123456def"
          }
        ],
        "Timestamps": [
          1558459800,
          1558460100
        ],
        "Values": [
          15.6,
          17.9
        ]
      }
    ],
    "RequestId": "23a38f36-5c73-43fb-ae46-12345678"
  }
}
```