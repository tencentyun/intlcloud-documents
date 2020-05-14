## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend that you distribute call requests across a period of time.

To query the monitoring data of a COS bucket, use the following input parameters:
&Namespace=QCE/COS
&Instances.N.Dimensions.0.Name=appid
&Instances.N.Dimensions.0.Value=APPID of the root account
&Instances.N.Dimensions.1.Name=bucket
&Instances.N.Dimensions.1.Value=Bucket name

## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1 Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/product/436/6224) supported by COS |
| Namespace | Yes | String | Namespace. Each Tencent Cloud service has a namespace, such as QCE/COS for COS. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :------------------------------ | :------- | :----------- | :------------------------------------------------ |
| &Instances.N.Dimensions.0.Name | appid | Root account `APPID` | Enter a string-type dimension name, such as appid |
| &Instances.N.Dimensions.0.Value | appid | Root account `APPID` | Enter the root account `APPID`, such as 1250000000 |
| &Instances.N.Dimensions.1.Name | bucket | Bucket name | Enter a string-type dimension name, such as bucket |
| &Instances.N.Dimensions.1.Value | bucket | Bucket name | Enter a specific bucket name, such as examplebucket-1250000000 |

### 2.2. Metric names

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

#### Storage metrics

The minimum statistical period supported by storage metrics is 300. Metric data can be pulled in a duration of 3600 or 86400.

| Metric Name | Description | Unit |
| :--------------------- | :---------------- | :--- |
| StdStorage | Standard storage capacity | MB |
| SiaStorage | Standard_IA storage capacity | MB |
| NelStorage | Nearline storage capacity | MB |
| ArcStorage | Archive storage capacity | MB |

#### Traffic metrics

The minimum statistical period supported by traffic metrics is 60. Metric data can be pulled in a duration of 300, 3600, or 86400.

| Metric Name | Description | Unit |
| :--------------------- | :----------- | :--- |
| InternetTraffic | Public traffic | B |
| InternalTraffic | Private traffic | B |
| CdnOriginTraffic | CDN origin-pull traffic | B |
| InboundTraffic | Upload traffic | B |

#### Data retrieval metrics

The minimum statistical period supported by data retrieval metrics is 60. Metric data can be pulled in a duration of 300, 3600, or 86400.

| Metric Name | Description | Unit |
| :--------------------- | :----------- | :--- |
| StdRetrieval | Standard data retrieval | B |
| IaRetrieval | Standard_IA data retrieval | B |
| NlRetrieval | Nearline data retrieval | B |

#### Request metrics

The minimum statistical period supported by request metrics is 60. Metric data can be pulled in a duration of 300, 3600, or 86400.

| Metric Name | Description | Unit |
| :--------------------- | :------------- | :--- |
| StdReadRequests | Standard storage read requests | - |
| StdWriteRequests | Standard storage write requests | - |
| IaReadRequests | Standard_IA storage read requests | - |
| IaWriteRequests | Standard_IA storage write requests | - |
| NlReadRequests | Nearline storage read requests | - |
| NlWriteRequests | Nearline storage write requests | - |

#### Return code metrics

| Metric Name | Description | Unit |
| :--------------------- | :--------- | :--- |
| 2xxResponse | 2xx status codes | - |
| 3xxResponse | 3xx status codes | - |
| 4xxResponse | 4xx status codes | - |
| 5xxResponse | 5xx status codes | - |

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
| -502 | The resource does not exist | OperationDenied.SourceNotExists |
| -503 | Incorrect request parameter | InvalidParameter |
| -505 | Missing parameter | InvalidParameter.MissingParameter |
| -507 | Limit exceeded | OperationDenied.ExceedLimit |
| -509 | Incorrect combination of dimensions | InvalidParameter.DimensionGroupError |
| -513 | Database operation failed | InternalError.DBoperationFail |

## 5. Samples

### Sample 1

This example shows you how to get the monitoring data for the standard storage capacity of one COS bucket using a statistical period of 300 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/COS
&MetricName=StdStorage
&Period=300
&StartTime=2019-05-22T16:40:00+08:00
&EndTime=2019-05-22T16:45:00+08:00
&Instances.0.Dimensions.0.Name=appid
&Instances.0.Dimensions.0.Value=1250000000
&Instances.0.Dimensions.1.Name=bucket
&Instances.0.Dimensions.1.Value=examplebucket-1250000000 
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-22 16:40:00",
    "EndTime": "2019-05-22 16:45:00",
    "Period": 300,
    "MetricName": "StdStorage",
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

This example shows you how to get the monitoring data for the standard storage capacity of multiple COS buckets using a statistical period of 300 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/COS
&MetricName=StdStorage
&Period=300
&StartTime=2019-05-22T16:40:00+08:00
&EndTime=2019-05-22T16:45:00+08:00
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

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-22 16:40:00",
    "EndTime": "2019-05-22 16:45:00",
    "Period": 300,
    "MetricName": "StdStorage",
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