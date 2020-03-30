## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of a CVM instance, use the following input parameters:

&Namespace=QCE/CVM

&Instances.N.Dimensions.0.Name=InstanceId

&Instances.N.Dimensions.0.Value=specific CVM instance ID


## 2. Input Parameters

The list below contains only the API request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters

| Parameter Name | Required | Type | Description |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/CVM` |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `EndTime` cannot be earlier than `StartTime` |

### 2.2. Metric name

The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

#### 2.2.1. Monitoring metrics whose data can be obtained with no installation of monitor agent required

| Metric Name | Description | Unit |
| ------------- | ----- | ---- |
| lanOuttraffic | Private network outbound bandwidth | Mbps |
| lanIntraffic | Private network inbound bandwidth | Mbps |
| lanOutpkg | Private network outbound packets | Packets/sec |
| lanInpkg | Private network inbound packets | Packets/sec |
| WanOuttraffic | Public network outbound bandwidth | Mbps |
| WanIntraffic | Public network inbound bandwidth | Mbps |
| AccOuttraffic | Public network outbound traffic | MB |
| WanOutpkg | Public network outbound packets | Packets/sec |
| WanInpkg | Public network inbound packets | Packets/sec |

#### 2.2.2. Monitoring metrics whose data can be obtained with installation of monitor agent required

| Metric Name | Description | Calculation Rule | Meaning | Unit | Period |
| ------------ | ------- | ---------------------------------------- | --------------------------- | ---- | ------------- |
| CPUUsage | CPU utilization | Ratio of user + nice + system + irq + softirq + idle + iowait time of the CPU to the total time | Percentage of CPU used in real time during machine operation | % | 10s, 60s, 300s |
| CPULoadAvg | Average CPU load | The data in `/proc/loadavg` is analyzed to calculate the average system load in the past 1 minute at an interval of 10 seconds.
(This metric is unavailable on Windows) | Average number of tasks that are using and waiting to use the CPU in a period of time | - | 10s, 60s, 300s |
| MemUsed | Used memory | On Windows, call `GlobalMemoryStatusEx`.
On Linux, call `psutil.virtual_memory()`.
Calculation rule: total memory - available memory (including `buffers` and `cached`) = used memory (excluding `buffers` and `cached`) | Amount of memory actually used, excluding the memory used by buffers and system caches | MB | 10s, 60s, 300s |
| MemUsage | Memory utilization | Ratio of used memory (excluding caches, buffers, and remaining available capacity) to total memory | Amount of memory actually used, excluding the memory used by buffers and system caches | % | 10s, 60s, 300s |
| TcpCurrEstab | TCP connections | On Windows, call `GetTcpTable` to get the number of TCP connections in `MIB_TCP_STATE_ESTAB` status. On Linux, get the value of `CurrEstab` from `/proc/net/snmp` | Number of connections in `ESTABLISHED` status | - | 10s, 60s, 300s |

Note: the reporting, display, and alarming time of metrics that can be obtained only after the agent is installed is the local time of your CVM instance. Therefore, if the local time of your instance is not in GMT +8, the time of the instance monitoring data will also not be in GMT +8.

## 3. Output Parameters

| Parameter Name | Type | Description |
| ---------- | --------------------- | ---------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues |

## 4. Samples

### Sample 1. Getting the monitoring data of one instance

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CVM
&MetricName=CPUUsage
&Period=300
&StartTime=2018-08-24T10:40:23+08:00
&EndTime=2018-08-24T10:50:23+08:00
&Instances.0.Dimensions.0.Name=InstanceId
&Instances.0.Dimensions.0.Value=ins-j0hk02zo
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
"Name": "InstanceId",
"Value": "ins-j0hk02zo"
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
"MetricName": "CPUUsage",
"Period": 300,
"RequestId": "d96ec542-6547-4af2-91ac-fee85c1b8b85",
"StartTime": "2018-08-24 10:40:00"
}
}
```

### Sample 2. Getting the monitoring data of multiple instances

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CVM
&MetricName=CPUUsage
&Period=300
&StartTime=2018-09-22T10:40:23+08:00
&EndTime=2018-09-22T10:50:23+08:00
&Instances.0.Dimensions.0.Name=InstanceId
&Instances.0.Dimensions.0.Value=ins-j0hk02zo
&Instances.1.Dimensions.0.Name=InstanceId
&Instances.1.Dimensions.0.Value=ins-o8vv2w10
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
"Name": "InstanceId",
"Value": "ins-j0hk02zo"
}
],
"Timestamps": [],
"Values": []
},
{
"Dimensions": [
{
"Name": "InstanceId",
"Value": "ins-o8vv2w10"
}
],
"Timestamps": [],
"Values": []
}
],
"EndTime": "2018-09-22 10:50:00",
"MetricName": "CPUUsage",
"Period": 300,
"RequestId": "9ac53ccc-fbab-483d-980b-b763bcc2f83f",
"StartTime": "2018-09-22 10:40:00"
}
}
```