## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension description, and monitoring metrics.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the monitoring data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call many metrics and objects. We recommend that you distribute call requests across a period of time.

To query the monitoring data of CVM, use the following input parameters:
&Namespace=QCE/CVM
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=Specific CVM ID

## 2. Input Parameters

The list below contains only the API request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1 Input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, see the [list of regions](https://intl.cloud.tencent.com/document/product/213/31574#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by CVMs. |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as QCE/CVM for CVMs. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

### 2.2. Metric names

The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

#### 2.2.1 Data monitoring metrics obtained without the installation of the monitor agent

| Metric Name | Description | Unit |
| :------------ | :--------- | :---- |
| lanOuttraffic | Private network outbound bandwidth | Mbps |
| lanIntraffic | Private network inbound bandwidth | Mbps |
| lanOutpkg | Private network outbound packets | Packets/second |
| lanInpkg | Private network inbound packets | Packets/second |
| WanOuttraffic | Public network outbound bandwidth | Mbps |
| WanIntraffic | Public network inbound bandwidth | Mbps |
| AccOuttraffic | Public network outbound traffic | MB |
| WanOutpkg | Public network outbound packets | Packets/second |
| WanInpkg | Public network inbound packets | Packets/second |

#### 2.2.2 Data monitoring metrics obtained after the installation of the monitor agent

| Metric Name | Description | Calculation Method | Meaning | Unit | Statistical Granularity (Period) |
| :----------- | :----------- | :----------------------------------------------------------- | :----------------------------------------------------- | :--- | :----------------- |
| CPUUsage | CPU utilization | CPU "user+nice+system+irq+softirq+idle+iowait" time as a percentage of the total time | Percentage of the time during which the CPU is occupied in real time when the CVM is running | % | 10s, 60s, and 300s |
| CPULoadAvg | CPU average load | Analyze data in /proc/loadavg, and collect the average load of the system in the last 1 minute every 10 seconds (metric is not available on Windows CVMs) | Average number of tasks that are using and about to use the CPU over a period of time | - | 10s, 60s, and 300s |
| MemUsed | Memory usage | Windows: call GlobalMemoryStatusEx. Linux: call psutil.virtual_memory(). Calculate the value of memory usage (excluding buffers and cached) by subtracting the available memory (including buffers and cached) from the total memory | Actual memory used by users, excluding those used by buffers and system caches | MB | 10s, 60s, and 300s |
| MemUsage | Memory utilization | Ratio of the used memory (excluding caches, buffers, and the remaining memory) to the total memory | Actual memory used by users, excluding those used by buffers and system caches | % | 10s, 60s, and 300s |
| TcpCurrEstab | TCP connections | On Windows, call `GetTcpTable` to get the number of TCP connections in `MIB_TCP_STATE_ESTAB` status. On Linux, get the value of `CurrEstab` from `/proc/net/snmp` | Number of TCP connections in `ESTABLISHED` status | - | 10s, 60s, and 300s |

Note: The metric reporting, display and alarm times obtained only by installing the agent are the local time of the user’s CVM. If the local time on the CVM is not UTC+08:00, then the time when the monitoring data is collected is the non-UTC+08:00 local time on the CVM.

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. RequestId is required to troubleshoot issues |

## 4. Samples

### Sample 1. Getting the monitoring data of a single instance

#### Sample input code



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

#### Sample output code



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

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CVM
&MetricName=CPUUsage
&Period=300
&StartTime=2018-09-22T10:40:23+08:00
&EndTime=2018-09-22T20:51:23+08:00
&Instances.0.Dimensions.0.Name=InstanceId
&Instances.0.Dimensions.0.Value=ins-j0hk02zo
&Instances.1.Dimensions.0.Name=InstanceId
&Instances.1.Dimensions.0.Value=ins-o8vv2w10
&<Common request parameters>
```

#### Sample output code



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