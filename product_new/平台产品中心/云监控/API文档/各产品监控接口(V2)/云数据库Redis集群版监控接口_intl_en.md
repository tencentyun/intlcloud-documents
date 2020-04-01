## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a TencentDB for Redis instance, use the following input parameters:

&Namespace=QCE/REDIS

&Instances.N.Dimensions.0.Name=instanceid

&Instances.N.Dimensions.0.Value=instance ID


## 2. Input Parameters


The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters
#### 2.1.1. Overview of input parameters
| Parameter Name | Required | Type | Description |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/REDIS`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | instanceid | Instance ID | String-type dimension name: instanceid |
| Instances.N.Dimensions.0.Value | instanceid | Specific instance ID | Specific TencentDB for Redis instance ID such as tdsql-123456, i.e., instance serial number such as crs-ifmymj41, which can be queried through the [DescribeRedis](https://intl.cloud.tencent.com/document/api/239/1384) API |
| Instances.N.Dimensions.1.Name | clusterid | Shard ID | String-type dimension name: clusterid. If the overall information is to be pulled, do not pass in this value. If the shard information is to be pulled, the input parameter must be `clusterid` |
| Instances.N.Dimensions.1.Value | clusterid | Specific shard ID | Shard ID such as tdsql-123456, which can be obtained through commands like `cluster nodes` |


### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

#### 2.2.1. Overall instance information metric names
| Metric Name | Description | Unit |
| --------------------- | ------------ | ---- |
| CmdstatGetMin | GET commands | Commands /min |
| CmdstatGetbitMin | GETBIT commands | Commands /min |
| CmdstatGetrangeMin | GETRANGE commands | Commands /min |
| CmdstatHgetMin | HGET commands | Commands /min |
| CmdstatHgetallMin | HGETALL commands | Commands /min |
| CmdstatHmgetMin | HMGET commands | Commands /min |
| CmdstatHmsetMin | HMSET commands | Commands /min |
| CmdstatHsetMin | HSET commands | Commands /min |
| CmdstatHsetnxMin | HSETNX commands | Commands /min |
| CmdstatLsetMin | LSET commands | Commands /min |
| CmdstatMgetMin | MGET commands | Commands /min |
| CmdstatMsetMin | MSET commands | Commands /min |
| CmdstatMsetnxMin | MSETNX commands | Commands /min |
| CmdstatSetMin | SET commands | Commands /min |
| CmdstatSetbitMin | SETBIT commands | Commands /min |
| CmdstatSetexMin | SETEX commands | Commands /min |
| CmdstatSetnxMin | SETNX commands | Commands /min |
| CmdstatSetrangeMin | SETRANGE commands | Commands /min |
| QpsMin | Commands executed per minute | Commands/min |
| ConnectionsMin | Connections | - |
| CpuUsMin | CPU utilization | % |
| InFlowMin | Private network inbound traffic | MB/min |
| KeysMin | Keys | - |
| OutFlowMin | Private network outbound traffic | MB/min |
| StatGetMin | All GET commands | Commands/min |
| StatSetMin | All SET commands | Commands/min |
| StorageMin | Used capacity | MB/min |
| StorageUsMin | Capacity utilization | % |

#### 2.2.1. Instance shard information metric names
| Metric Name | Description | Unit |
| --------------------- | ------------ | ---- |
| CmdstatGetNodeMin | GET commands | Commands /min |
| CmdstatGetbitNodeMin | GETBIT commands | Commands /min |
| CmdstatGetrangeNodeMin | GETRANGE commands | Commands /min |
| CmdstatHgetNodeMin | HGET commands | Commands /min |
| CmdstatHgetallNodeMin | HGETALL commands | Commands /min |
| CmdstatHmgetNodeMin | HMGET commands | Commands /min |
| CmdstatHmsetNodeMin | HMSET commands | Commands /min |
| CmdstatHsetNodeMin | HSET commands | Commands /min |
| CmdstatHsetnxNodeMin | HSETNX commands | Commands /min |
| CmdstatLsetNodeMin | LSET commands | Commands /min |
| CmdstatMgetNodeMin | MGET commands | Commands /min |
| CmdstatMsetNodeMin | MSET commands | Commands /min |
| CmdstatMsetnxNodeMin | MSETNX commands | Commands /min |
| CmdstatSetNodeMin | SET commands | Commands /min |
| CmdstatSetbitNodeMin | SETBIT commands | Commands /min |
| CmdstatSetexNodeMin | SETEX commands | Commands /min |
| CmdstatSetnxNodeMin | SETNX commands | Commands /min |
| CmdstatSetrangeNodeMin | SETRANGE commands | Commands /min |
| QpsNodeMin | Commands executed per minute | Commands/min |
| ConnectionsNodeMin | Connections | - |
| CpuUsNodeMin | CPU utilization | % |
| InFlowNodeMin | Private network inbound traffic | MB/min |
| KeysNodeMin | Keys | - |
| OutFlowNodeMin | Private network outbound traffic | MB/min |
| StatGetNodeMin | All GET commands | Commands /min |
| StatSetNodeMin | All SET commands | Commands /min |
| StorageNodeMin | Used capacity | MB/min |
| StorageUsNodeMin | Capacity utilization | % |


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

### Sample 1. Getting the number of GET commands of one TencentDB for Redis instance
This example shows you how to get the number of GET commands of one TencentDB for Redis instance using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-1234567
&[<Common request parameters>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-06-04 00:35:00",
"EndTime": "2019-06-04 00:40:00",
"Period": 60,
"MetricName": "CmdstatGetMin",
"DataPoints": [
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-miv64oan"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
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
"RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
}
}
```
### Sample 2. Getting the number of GET commands of multiple TencentDB for Redis instances
This example shows you how to get the number of GET commands of multiple TencentDB for Redis instances using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-123456
&Instances.1.Dimensions.0.Name=instanceid
&Instances.1.Dimensions.0.Value=crs-1234567
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-06-04 00:35:00",
"EndTime": "2019-06-04 00:40:00",
"Period": 60,
"MetricName": "CmdstatGetMin",
"DataPoints": [
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-123456"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
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
"Name": "instanceid",
"Value": "crs-1234567"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
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
"RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
}
}
```


### Sample 3. Getting the number of GET commands of one TencentDB for Redis instance at shard-level
This example shows you how to get the number of GET commands of one TencentDB for Redis instance at shard-level using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetNodeMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-1234567
&Instances.0.Dimensions.1.Name=clusterid
&Instances.0.Dimensions.1.Value=tdsql-1234567
&[<Common request parameters>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-06-04 00:35:00",
"EndTime": "2019-06-04 00:40:00",
"Period": 60,
"MetricName": "CmdstatGetNodeMin",
"DataPoints": [
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-1234567"
},{
"Name": "clusterid",
"Value": "tdsql-1234567"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
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
"RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
}
}
```
### Sample 4. Getting the number of GET commands of multiple TencentDB for Redis instances at shard-level
This example shows you how to get the number of GET commands of multiple TencentDB for Redis instances at shard-level using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetNodeMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-123456
&Instances.0.Dimensions.1.Name=clusterid
&Instances.0.Dimensions.1.Value=tdsql-123456
&Instances.1.Dimensions.0.Name=instanceid
&Instances.1.Dimensions.0.Value=crs-1234567
&Instances.1.Dimensions.1.Name=clusterid
&Instances.1.Dimensions.1.Value=tdsql-1234567
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-06-04 00:35:00",
"EndTime": "2019-06-04 00:40:00",
"Period": 60,
"MetricName": "CmdstatGetNodeMin",
"DataPoints": [
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-1234567"
},{
"Name": "clusterid",
"Value": "tdsql-1234567"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
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
"Name": "instanceid",
"Value": "crs-123456"
},{
"Name": "clusterid",
"Value": "tdsql-123456"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
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
"RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
}
}
```