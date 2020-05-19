## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension description, and monitoring metrics.

Cloud Load Balancer (CLB) is a traffic distribution service for multiple CVMs. For more information, see [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524). Currently, CLB supports four types of namespace: QCE/LB_PUBLIC, QCE/LB_PRIVATE, QCE/LB_RS_PRIVATE, and QCE/LOADBALANCE.

QCE/LB_PUBLIC: indicates the namespace for public network CLB, which includes monitoring data in the CLB and real server dimensions.
QCE/LB_PRIVATE: indicates the namespace for private network CLB, which includes monitoring data in the CLB dimension.
QCE/LB_RS_PRIVATE: indicates the namespace for private network CLB, which includes monitoring data in the real server dimension.
QCE/LOADBALANCE: indicates the namespace for CLB layer-7 data.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the monitoring data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend that you distribute call requests across a period of time.

QCE/LB_RS_PRIVATE is a namespace in the private network CLB real server dimension, and can be used to query the monitoring data in the private network CLB real server dimension. QCE/LB_RS_PRIVATE is used to query monitoring data based on the following 2 dimension groups. The values of input parameters are as follows:

### 1.1 Values of input parameters in the private network CLB real server dimension

Since the private VIP may be repeated, vpcId is also required to uniquely specify an lb:
&Namespace= QCE/LB_RS_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=VPC ID of the CLB instance
&Instances.N.Dimensions.2.Name=loadBalancerPort
&Instances.N.Dimensions.2.Value=Port number
&Instances.N.Dimensions.3.Name=protocol
&Instances.N.Dimensions.3.Value=Protocol type
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=Real server IP address of the CLB instance

### 1.2 Values of input parameters in the private network CLB real server port dimension

Since the private network VIP may be repeated, vpcId is also required to uniquely specify an lb:

&Namespace= QCE/LB_RS_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=VPC ID of the CLB instance
&Instances.N.Dimensions.2.Name=loadBalancerPort
&Instances.N.Dimensions.2.Value=Port number
&Instances.N.Dimensions.3.Name=protocol
&Instances.N.Dimensions.3.Value=Protocol type
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=Real server IP address of the CLB instance
&Instances.N.Dimensions.5.Name=port
&Instances.N.Dimensions.5.Value=Real server port number of the CLB instance

## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1 Input Parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, see the [list of regions](https://intl.cloud.tencent.com/document/product/214/33792) supported by private network CLBs. |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/LB_RS_PRIVATE for the private network CLB real server dimension. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Dimension parameters

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :--------------- | :------------------------ | :--------------------------------------------- |
| Instances.N.Dimensions.0.Name | vip | CLB VIP | Enter a string-type dimension name, such as vip |
| Instances.N.Dimensions.0.Value | vip | CLB VIP | Enter a specific IP address, such as 111.111.111.11 |
| Instances.N.Dimensions.1.Name | vpcId | VPC ID of the CLB instance | Enter a string-type dimension name, such as vpcId |
| Instances.N.Dimensions.1.Value | vpcId | VPC ID of the CLB instance | Enter a specific VPC ID, such as 1111 |
| Instances.N.Dimensions.2.Name | loadBalancerPort | CLB port | Enter a string-type dimension name, such as loadBalancerPort |
| Instances.N.Dimensions.2.Value | loadBalancerPort | CLB port | Enter a specific port number, such as 80 |
| Instances.N.Dimensions.3.Name | protocol | Protocol | Enter a string-type dimension name, such as protocol |
| Instances.N.Dimensions.3.Value | protocol | Protocol | Enter a specific protocol name, such as http |
| Instances.N.Dimensions.4.Name | lanIp | IP address of the instance bound to the CLB | Enter a string-type dimension name, such as lanIp |
| Instances.N.Dimensions.4.Value | lanIp | IP address of the instance bound to the CLB | Enter a specific IP address, such as 111.111.111.11 |
| Instances.N.Dimensions.5.Name | port | Port number of the instance bound to the CLB | Enter a string-type dimension name, such as port |
| Instances.N.Dimensions.5.Value | port | Port number of the instance bound to the CLB | Enter a specific port number, such as 80 |

### 2.2. Metric names

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit |
| :--------------------- | :--------- | :--- |
| Connum | Current connections | - |
| NewConn | New connections | Connections/second |
| Intraffic | Inbound traffic | Mbps |
| Outtraffic | Outbound traffic | Mbps |
| Inpkg | Inbound packets | Packets/second |
| Outpkg | Outbound packets | Packets/second |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime  | Timestamp | Data point start time |
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

### Sample 1. Getting the number of current connections of one private network CLB instance in the real server dimension

This example shows you how to get the monitoring data for the number of current connections of one private network CLB instance in the real server dimension using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/LB_RS_PRIVATE
&MetricName=Connum
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=vip
&Instances.0.Dimensions.0.Value=111.111.111.11
&Instances.0.Dimensions.1.Name=vpcId
&Instances.0.Dimensions.1.Value=123456
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-08 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 60,
    "MetricName": "Intraffic",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "vip",
            "Value": "111.111.111.11"
          },
          {
            "Name": "vpcId",
            "Value": "123456"
          }
        ],
        "Timestamps": [
          1558339260,
          1558339320,
          1558339380,
          1558339440,
          1558339500
          ],
        "Values": [
          10,
          20,
          30,
          40,
          50
        ]
      }
    ],
    "RequestId": "f231ae98-7985-4009-aa48-3f9d8989347d"
  }
}
```

### Sample 2

This example shows you how to get the monitoring data for the number of current connections of multiple network CLB instances in the real server dimension using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/LB_RS_PRIVATE
&MetricName=Connum
&Period=60
&StartTime=2019-05-08T16:40:00+08:00
&EndTime=2019-05-08T16:45:00+08:00
&Instances.0.Dimensions.0.Name=vip
&Instances.0.Dimensions.0.Value=111.111.111.11
&Instances.0.Dimensions.1.Name=vpcId
&Instances.0.Dimensions.1.Value=123456
&Instances.1.Dimensions.0.Name=vip
&Instances.1.Dimensions.0.Value=222.222.222.22
&Instances.1.Dimensions.1.Name=vpcId
&Instances.1.Dimensions.1.Value=1234567
&<Common request parameters>
```

#### Sample output code



```
{
  "Response": {
    "StartTime": "2019-05-08 16:40:00",
    "EndTime": "2019-05-08 16:45:00",
    "Period": 60,
    "MetricName": "Intraffic",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "vip",
            "Value": "111.111.111.11"
          },
          {
            "Name": "vpcId",
            "Value": "123456"
          }
        ],
        "Timestamps": [
          1558339260,
          1558339320,
          1558339380,
          1558339440,
          1558339500
          ],
        "Values": [
          10,
          20,
          30,
          40,
          50
        ]
      },
      {
        "Dimensions": [
          {
            "Name": "vip",
            "Value": "222.222.222.22"
          },
          {
            "Name": "vpcId",
            "Value": "1234567"
          }
        ],
        "Timestamps": [
          1558339260,
          1558339320,
          1558339380,
          1558339440,
          1558339500
          ],
        "Values": [
          10,
          20,
          30,
          40,
          50
        ]
      }
    ],
    "RequestId": "f231ae98-7985-4009-aa48-3f9d8989347d"
  }
}
```