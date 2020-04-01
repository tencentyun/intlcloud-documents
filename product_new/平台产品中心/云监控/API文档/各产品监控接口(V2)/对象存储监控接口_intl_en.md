## 1. API Description

API: GetMonitorData<br>
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of COS, use the following input parameters:<br>
&Namespace=QCE/COS<br>
&Instances.N.Dimensions.0.Name=appid<br>
&Instances.N.Dimensions.0.Value=root account `APPID`<br>
&Instances.N.Dimensions.1.Name=bucket<br>
&Instances.N.Dimensions.1.Value=bucket name<br>

## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/248/4478#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/zh/document/product/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/COS`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------- | -------- | ------------ | --------------------------------------- |
| &Instances.N.Dimensions.0.Name  | appid    | Root account `APPID` | String type                             |
| &Instances.N.Dimensions.0.Value | appid    | Root account `APPID` | Root account `APPID`, such as 1250000000             |
| &Instances.N.Dimensions.1.Name  | bucket   | Bucket name    | String type                             |
| &Instances.N.Dimensions.1.Value | bucket   | Bucket name   | Bucket name, such as examplebucket-1250000000 |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

#### Storage

The minimum statistical period supported by storage metrics is 300. Metric data can be pulled in a duration of 3600 or 86400.

| Metric Name | Meaning | Unit |
| ---------------------- | ----------------- | ---- |
| StdStorage | Standard storage - storage capacity | MB |
| SiaStorage | Standard_IA storage - storage capacity | MB |
| NelStorage | Nearline storage - storage capacity | MB |
| arc_storage | Archive storage - storage capacity | MB |

#### Traffic

The minimum statistical period supported by traffic metrics is 60. Metric data can be pulled in a duration of 300, 3600, or 86400.

| Metric Name | Description | Unit |
| ---------------------- | ------------- | ---- |
| InternetTraffic | Public network traffic | B |
| InternalTraffic | Private network traffic | B |
| CdnOriginTraffic | CDN origin-pull traffic | B |
| InboundTraffic | Upload traffic | B |

#### Data reads

The minimum statistical period supported by data read metrics is 60. Metric data can be pulled in a duration of 300, 3600, or 86400.

| Metric Name | Meaning | Unit |
| ---------------------- | ------------ | ---- |
| StdRetrieval | Standard data reads | B |
| IaRetrieval | Standard_IA data reads | B |
| NlRetrieval | Nearline data reads | B |

#### Requests

The minimum statistical period supported by request metrics is 60. Metric data can be pulled in a duration of 300, 3600, or 86400.

| Metric Name | Meaning | Unit |
| ---------------------- | -------------- | ---- |
| StdReadRequests | Standard storage read requests | - |
| StdWriteRequests | Standard storage write requests | - |
| IaReadRequests | Standard_IA storage read requests | - |
| IaWriteRequests | Standard_IA storage write requests | - |
| NlReadRequests | Nearline storage read requests | - |
| NlWriteRequests | Nearline storage write requests | - |

#### Return codes

| Metric Name | Description | Unit |
| ---------------------- | ----------- | ---- |
| 2xxResponse            | 2xx status code | - |
| 3xxResponse            | 3xx status code | - |
| 4xxResponse            | 4xx status code | - |
| 5xxResponse            | 5xx status code | - |

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

### Sample 1

This example shows you how to get the standard storage capacity monitoring data of one COS bucket using a statistical period of 300 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/COS
&MetricName=StdStorage
&Period=300
&StartTime=2019-05-22T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=appid
&Instances.0.Dimensions.0.Value=1250000000
&Instances.0.Dimensions.1.Name=bucket
&Instances.0.Dimensions.1.Value=examplebucket-1250000000 
&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "StartTime": "2019-05-22 16:40:00",
    "EndTime": "2019-05-22 16:45:00",
    "Period": 300,
    "MetricName": "5xxResponse",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "appid",
            "Value": "1250000000"
          },
          {
            "Name": "bucket",
            "Value": "examplebucket-1250000000"
          }
        ],
        "Timestamps": [
          1558459800,
          1558460100
        ],
        "Values": [
          0,
          0
        ]
      }
    ],
    "RequestId": "23a38f36-5c73-43fb-ae46-022d10eb91fc"
  }
}
```

### Sample 2 

This example shows you how to get the standard storage capacity monitoring data of multiple COS buckets using a statistical period of 300 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/COS
&MetricName=StdStorage
&Period=300
&StartTime=2019-05-22T16:40:00+08:00
&EndTime=2018-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=appid
&Instances.0.Dimensions.0.Value=1250000000
&Instances.0.Dimensions.1.Name=bucket
&Instances.0.Dimensions.1.Value=examplebucket-1250000000
&Instances.1.Dimensions.0.Name=appid
&Instances.1.Dimensions.0.Value=1250000001
&Instances.1.Dimensions.1.Name=bucket
&Instances.1.Dimensions.1.Value=examplebucket-1250000001 
&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "StartTime": "2019-05-22 16:40:00",
    "EndTime": "2019-05-22 16:45:00",
    "Period": 300,
    "MetricName": "5xxResponse",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "appid",
            "Value": "1250000000"
          },
          {
            "Name": "bucket",
            "Value": "examplebucket-1250000000"
          }
        ],
        "Timestamps": [
          1558459800,
          1558460100
        ],
        "Values": [
          0,
          0
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "appid",
            "Value": "1250000001"
          },
          {
            "Name": "bucket",
            "Value": "examplebucket-1250000001"
          }
        ],
        "Timestamps": [
          1558459800,
          1558460100
        ],
        "Values": [
          0,
          0
        ]
      }
    ],
    "RequestId": "23a38f36-5c73-43fb-ae46-022d10eb91fc"
  }
}
```