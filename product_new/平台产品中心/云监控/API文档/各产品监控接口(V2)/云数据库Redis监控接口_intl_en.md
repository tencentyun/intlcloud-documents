## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a TencentDB for Redis instance, use the following input parameters:

&Namespace= QCE/REDIS

&Instances.N.Dimensions.0.Name=redis_uuid

&Instances.N.Dimensions.0.Value=instance uuid


## 2. Input Parameters


The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters
#### 2.1.1. Overview of input parameters
| Parameter Name | Required | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
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
| Instances.N.Dimensions.0.Name | redis_uuid | Instance ID | String-type dimension name: redis_uuid |
| Instances.N.Dimensions.0.Value | redis_uuid | Specific instance ID | Specific TencentDB for Redis instance ID, such as crs-123456 |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Parameter | Calculation Method (on Linux) | Statistical Method | Unit |
| ----------- | ---------------- | ---------------------------------------- | ------------------------- | ----- |
| Cache hit rate | CacheHitRatio | This is calculated by taking the values of `keyspace_misses` and `keyspace_hits` in a single minute to use in the formula `(1 - keyspace_misses/keyspace_hits) * 100%.` This metric has been disused | This metric is counted once every minute, and its value at the 5-minute granularity is the average in the last 5 minutes | % |
| GET commands | CmdstatGet | Number of GET command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| GETBIT commands | CmdstatGetbit | Number of GETBIT command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| GETRANGE commands | CmdstatGetrange | Number of GETRANGE command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| HGET commands | CmdstatHget | Number of HGET command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| HGETALL commands | CmdstatHgetall | Number of HGETALL command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| HMGET commands | CmdstatHmget | Number of HMGET command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| HMSET commands | CmdstatHmset | Number of HMSET command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| HSET commands | CmdstatHset | Number of HSET command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| HSETNX commands | CmdstatHsetnx | Number of HSETNX command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| LSET commands | CmdstatLset | Number of LSET command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| MGET commands | CmdstatMget | Number of MGET command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| MSET commands | CmdstatMset | Number of MSET command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| MSETNX commands | CmdstatMsetnx | Number of MSETNX command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| SET commands | CmdstatSet | Number of SET command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| SETBIT commands | CmdstatSetbit | Number of SETBIT command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| SETEX commands | CmdstatSetex | Number of SETEX command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| SETRANGE commands | CmdstatSetrange | Number of SETRANGE command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| Commands executed per second | Qps | Total number of commands in 1 minute / 60 | This metric is counted once every minute, and its value at the 5-minute granularity is the average in the last 5 minutes | Commands/sec |
| Connections | Connections | Sum of connections in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | - |
| CPU utilization | CpuUs | Percentage of CPU in non-idle state calculated based on the `/proc/stat` data | This metric is counted once every minute, and its value at the 5-minute granularity is the average in the last 5 minutes | % |
| Private network inbound traffic | InFlow | Sum of private network inbound traffic in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | MB/min |
| Keys | Keys | Maximum number of keys in one minute | This metric is counted once every minute, and its value at the 5-minute granularity is the maximum in the last 5 minutes | - |
| Private network outbound traffic | OutFlow | Sum of private network outbound traffic in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | MB/min |
| All GET commands | StatGet | Number of GET, HGET, HGETALL, HMGET, MGET, GETBIT, and GETRANGE command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| All SET commands | StatSet | Number of SET, HSET, HMSET, HSETNX, LSET, MSET, MSETNX, SETBIT, SETEX, SETRANGE, and SETNX command requests in 1 minute | This metric is counted once every minute, and its value at the 5-minute granularity is the sum in the last 5 minutes | Commands/min |
| Used capacity | Storage | Maximum value of used capacity in one minute | This metric is counted once every minute, and its value at the 5-minute granularity is the maximum in the last 5 minutes | MB/min |
| Capacity utilization | StorageUs | Maximum percentage of used capacity in one minute | This metric is counted once every minute, and its value at the 5-minute granularity is the maximum in the last 5 minutes | % |



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
| ---- | ------- | ------------------------------------ |
| -502 | The resource does not exist. | OperationDenied.SourceNotExists |
| -503 | Incorrect request parameter. | InvalidParameter |
| -505 | Missing parameter. | InvalidParameter.MissingParameter |
| -507 | Limit exceeded. | OperationDenied.ExceedLimit |
| -509 | Incorrect combination of dimensions. | InvalidParameter.DimensionGroupError |
| -513 | Database operation failed. | InternalError.DBoperationFail |

## 5. Samples

### Sample 1
This example shows you how to get the number of connections of one TencentDB for Redis instance using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/REDIS
&MetricName=Connections
&Period=60
&StartTime=2019-06-04T00:00:00+08:00
&EndTime=2019-06-04T00:05:00+08:00
&Instances.0.Dimensions.0.Name=redis_uuid
&Instances.0.Dimensions.0.Value=crs-123456
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-06-04 00:00:00",
"EndTime": "2019-06-04 00:05:00",
"Period": 60,
"MetricName": "Connections",
"DataPoints": [
{
"Dimensions": [
{
"Name": "redis_uuid",
"Value": "crs-123456"
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
3,
3,
4.5,
3,
3
]
}
],
"RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
}
}
```
### Sample 2 
This example shows you how to get the number of connections of multiple TencentDB for Redis instances using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/REDIS
&MetricName=Connections
&Period=60
&StartTime=2019-06-04T00:00:00+08:00
&EndTime=2019-06-04T00:05:00+08:00
&Instances.0.Dimensions.0.Name=redis_uuid
&Instances.0.Dimensions.0.Value=crs-123456
&Instances.1.Dimensions.0.Name=redis_uuid
&Instances.1.Dimensions.0.Value=crs-1234567
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-06-04 00:00:00",
"EndTime": "2019-06-04 00:05:00",
"Period": 60,
"MetricName": "Connections",
"DataPoints": [
{
"Dimensions": [
{
"Name": "redis_uuid",
"Value": "crs-123456"
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
3,
3,
4.5,
3,
3
]
},
{
"Dimensions": [
{
"Name": "redis_uuid",
"Value": "crs-1234567"
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
3,
3,
4.5,
3,
3
]
}
],
"RequestId": "0ea9aeee-3bf8-46a0-b594-c2b9e1b7f0bf"
}
}
```