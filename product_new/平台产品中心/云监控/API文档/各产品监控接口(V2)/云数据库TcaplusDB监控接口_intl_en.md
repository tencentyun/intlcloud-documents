## 1. API Description

API: GetMonitorData
Domain name for API request: monitor.tencentcloudapi.com

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend that you spread the call requests over time.

To query the monitoring data of TcaplusDB, use the following input parameters:
&Namespace=QCE/TCAPLUS
&Instances.N.Dimensions.0.Name=TableInstanceId
&Instances.N.Dimensions.0.Value=database ID
&Instances.N.Dimensions.1.Name=ApplicationId
&Instances.N.Dimensions.1.Value=application ID

## 2. Input Parameters

The list below contains only API request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1. Input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region      | No    | String                                   | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [region list](https://intl.cloud.tencent.com/document/product/1016/35019) supported by TcaplusDB |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/TCAPLUS` |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime   | No    | Datetime | Start time, such as "2018-09-22T19:51:23+08:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `EndTime` cannot be earlier than `StartTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :---------------- | :--------------- | :---------------------------------- |
| Instances.N.Dimensions.0.Name  | TableInstanceId              | Database instance ID       | String-type dimension name: TableInstanceId             |
| Instances.N.Dimensions.0.Value | tcaplus-123abc456              | Specific database ID      | Specific instance name, such as tcaplus-123abc456        |
| Instances.N.Dimensions.1.Name  | ApplicationId              | Specific application ID       | String-type dimension name: ApplicationId              |
| Instances.N.Dimensions.1.Value | 123456789              |  Specific application ID     | Specific application ID, such as 123456789  |

### 2.2. Metric name

The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the period supported by each API.

#### 2.2.1. Monitoring metrics whose data can be obtained with no installation of monitor agent required

| Metric Name | Description | Unit |
| :----------- | :------------- | :----- |
| Avgerror | Average error rate | % |
| Writelatency  | Average write latency | Milliseconds |
| Comerror     | Common error rate | %  |
| Readlatency      | Average read latency | Milliseconds  |
| Volume | Storage capacity | KBytes |
| Syserror  | System error rate | % |
| Writecu | Actual write capacity unit | Units/sec   |
| Readcu     | Actual read capacity unit | Units/sec |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique request ID, which is returned in each request. The `RequestId` is required to troubleshoot issues |

## 4. Samples

### Sample 1. Getting the monitoring data of one instance

#### Scenario description

This example shows you how to get the monitoring data for the average error rate of one TcaplusDB instance using a statistical period of 5 minutes for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/TCAPLUS
&MetricName=Avgerror
&Period=300
&StartTime=2018-08-24T10:40:23+08:00
&EndTime=2018-08-24T10:50:23+08:00
&Instances.0.Dimensions.0.Name=TableInstanceId
&Instances.0.Dimensions.0.Value=tcaplus-123abc456
&Instances.0.Dimensions.1.Name=ApplicationId
&Instances.0.Dimensions.1.Value=123456789

&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "TableInstanceId",
            "Value": "tcaplus-123abc456"
          },
          {
            "Name": "ApplicationId",
            "Value": "123456789"
          }
        ],
        "Timestamps": [
          1535079000,
          1535079300,
          1535079600
        ],
        "Values": [
          2.566,
          2.283,
          6.316
        ]
      }
    ],
    "EndTime": "2018-08-24 10:50:00",
    "MetricName": "Avgerror",
    "Period": 300,
    "RequestId": "d96ec542-6547-4af2-91ac-fee85c1b8b85",
    "StartTime": "2018-08-24 10:40:00"
  }
}
```

### Sample 2. Getting the monitoring data of multiple instances

#### Scenario description

This example shows you how to get the monitoring data for the average error rate of multiple TcaplusDB instances using a statistical period of 5 minutes for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/TCAPLUS
&MetricName=Avgerror
&Period=300
&StartTime=2018-09-22T10:40:23+08:00
&EndTime=2018-09-22T10:50:23+08:00
&Instances.0.Dimensions.0.Name=TableInstanceId
&Instances.0.Dimensions.0.Value=tcaplus-123abc456
&Instances.0.Dimensions.1.Name=ApplicationId
&Instances.0.Dimensions.1.Value=123456789
&Instances.1.Dimensions.0.Name=TableInstanceId
&Instances.1.Dimensions.0.Value=tcaplus-123abc789
&Instances.1.Dimensions.1.Name=ApplicationId
&Instances.1.Dimensions.1.Value=987654321
&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "TableInstanceId",
            "Value": "tcaplus-123abc456"
          },
          {
            "Name": "ApplicationId",
            "Value": "123456789"
          }
        ],
        "Timestamps": [
          1535079000,
          1535079300,
          1535079600
        ],
        "Values": [
          2,
          2,
          6
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "TableInstanceId",
            "Value": "tcaplus-123abc789"
          },
          {
            "Name": "ApplicationId",
            "Value": "987654321"
          }
        ],
        "Timestamps": [
          1535079000,
          1535079300,
          1535079600
        ],
        "Values": [
          3,
          3,
          6
        ]
      }
    ],
    "EndTime": "2018-09-22 10:50:00",
    "MetricName": "Avgerror",
    "Period": 300,
    "RequestId": "9ac53ccc-fbab-483d-980b-b763bcc2f83f",
    "StartTime": "2018-09-22 11:00:00"
  }
}
```