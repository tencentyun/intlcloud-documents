## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend that you distribute call requests over a period of time.

To query the monitoring data of a CCN in a VPC, use the following input parameters:
&Namespace=QCE/VBC
&Instances.N.Dimensions.0.Name=CcnId
&Instances.N.Dimensions.0.Value=ccn-c889docn

## 2. Input Parameters

The list below contains only the API request parameters and some common parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/product/215/15758) supported by VPC |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/VBC for VPC CCN namespaces. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `EndTime` cannot be earlier than `StartTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :------- | :-------------- | :----------------------------------- |
| Instances.N.Dimensions.0.Name | CcnId | CCN ID | Enter a string-type dimension name, such as CcnId |
| Instances.N.Dimensions.0.Value | CcnId | Specific CCN ID | Enter a specific CCN ID, such as ccn-12345adc |
| Instances.N.Dimensions.0.Name | SRegion | Source region | Enter a string-type dimension name, such as `SRegion` |
| Instances.N.Dimensions.0.Value | SRegion | Specific source region | Enter a specific source region, such as `ap-shanghai` |
| Instances.N.Dimensions.0.Name | DRegion | Destination region | Enter a string-type dimension name, such as `DRegion` |
| Instances.N.Dimensions.0.Value | DRegion | Specific destination region | Enter a specific destination region, such as `ap-guangzhou` |

### 2.2. Metric names

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

### 2.2.1. Single-region metric names

| Metric Name | Description | Unit | Dimension |
| :----------------- | :------------- | :---- | :------------ |
| RegionOutPkg | Single-region outbound packets | Packets/sec | Single-region: CcnId |
| RegionInPkg | Single-region inbound packets | Packets/sec | Single-region: CcnId |
| RegionOutBandwidth | Single-region outbound bandwidth | Mbps | Single-region: CcnId |
| RegionInBandwidth | Single-region inbound bandwidth | Mbps | Single-region: CcnId |

### 2.2.2. Cross-region metric names

| Metric Name | Description | Unit | Dimension |
| :----------- | :----------- | :---- | :------------------------------ |
| OutPkg | Cross-region outbound packets | Packets/sec | Cross-region: CcnId, SRegion, and DRegion |
| InPkg | Cross-region inbound packets | Packets/sec | Cross-region: CcnId, SRegion, and DRegion |
| OutBandwidth | Cross-region outbound bandwidth | Mbps | Cross-region: CcnId, SRegion, and DRegion |
| InBandwidth | Cross-region inbound bandwidth | Mbps | Cross-region: CcnId, SRegion, and DRegion |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of request. Each request returns a unique ID. RequestId is required to troubleshoot issues |

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

This example shows you how to get the monitoring data for the number of single-region outbound packets of one CCN in a VPC using a statistical period of 60 seconds for a specified length of time.

#### Input sample code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/VBC
&MetricName=RegionOutPkg
&Period=60
&StartTime=2019-06-11T16:40:00+08:00
&EndTime=2019-06-11T16:45:00+08:00
&Instances.0.Dimensions.0.Name=CcnId
&Instances.0.Dimensions.0.Value=ccn-12345adc
&<Common request parameters>
```

#### Output sample code



```
{
  "Response": {
    "StartTime": "2019-06-11 16:40:00",
    "EndTime": "2019-06-11 16:45:00",
    "Period": 60,
    "MetricName": "RegionOutPkg",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "CcnId",
            "Value": "ccn-12345adc"
          }
        ],
        "Timestamps": [
          1560242400,
          1560242460,
          1560242520,
          1560242580,
          1560242640,
          1560242700
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
    "RequestId": "e3b37b87-b077-4601-9bb2-53b2fd529bea"
  }
}
```

### Sample 2

This example shows you how to get the monitoring data for the number of single-region outbound packets of multiple CCNs in a VPC using a statistical period of 60 seconds for a specified length of time.

#### Input sample code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/VBC
&MetricName=RegionOutPkg
&Period=60
&StartTime=2019-06-11T16:40:00+08:00
&EndTime=2019-06-11T16:45:00+08:00
&Instances.0.Dimensions.0.Name=CcnId
&Instances.0.Dimensions.0.Value=ccn-12345adc
&Instances.1.Dimensions.0.Name=CcnId
&Instances.1.Dimensions.0.Value=ccn-12345adcd
&<Common request parameters>
```

#### Output sample code



```
{
  "Response": {
    "StartTime": "2019-06-11 16:40:00",
    "EndTime": "2019-06-11 16:45:00",
    "Period": 60,
    "MetricName": "RegionOutPkg",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "CcnId",
            "Value": "ccn-12345adc"
          }
        ],
        "Timestamps": [
          1560242400,
          1560242460,
          1560242520,
          1560242580,
          1560242640,
          1560242700
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
            "Name": "CcnId",
            "Value": "ccn-12345adcd"
          }
        ],
        "Timestamps": [
          1560242400,
          1560242460,
          1560242520,
          1560242580,
          1560242640,
          1560242700
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
    "RequestId": "e3b37b87-b077-4601-9bb2-53b2fd529bea"
  }
}
```