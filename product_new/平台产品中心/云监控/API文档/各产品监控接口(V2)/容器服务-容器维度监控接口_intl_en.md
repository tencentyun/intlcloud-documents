## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. 

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

To query the monitoring data of TKE in the container dimension, use the following input parameters:

&Namespace=QCE/DOCKER

&Instances.N.Dimensions.0.Name=clusterId

&Instances.N.Dimensions.0.Value=cluster ID


## 2. Input Parameters


The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters
#### 2.1.1. Overview of input parameters
| Parameter Name | Required | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/DOCKER`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | clusterId | Cluster ID | String-type dimension name: clusterId |
| Instances.N.Dimensions.0.Value | clusterId | Specific cluster ID, i.e., the `clusterId` field returned by the DescribeClusters API | Specific cluster name, such as cls-xxxxx |
| Instances.N.Dimensions.1.Name | serviceName | Service name | String-type dimension name: serviceName |
| Instances.N.Dimensions.1.Value | serviceName | Specific service name, i.e., the `serviceName` field returned by the DescribeClusterService API | Specific service name, such as test |
| Instances.N.Dimensions.2.Name | namespace | Namespace name | String-type dimension name: namespace |
| Instances.N.Dimensions.2.Value | namespace | Specific namespace name, i.e., the `namespace` field returned by the DescribeClusterService API | Specific namespace name, such as default |
| Instances.N.Dimensions.3.Name | podName | Pod name | String-type dimension name: podName |
| Instances.N.Dimensions.3.Value | podName | Specific pod name, i.e., the `name` field returned by the DescribeServiceInstance API | Specific pod name, such as test-3488000495-nj6s9 |
| Instances.N.Dimensions.4.Name | containerId | Container name | String-type dimension name: containerId |
| Instances.N.Dimensions.4.Value | containerId | Specific container ID, i.e., the `containerId` field returned by the DescribeServiceInstance API. Note: only the first 12 characters of the container ID is needed | Specific container ID, such as 01c5509d2b39 |


### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://cloud.tencent.com/document/product/248/30351) API can be used to get the `period` and `dimension` supported by each metric.

| Monitoring Item | Metric Name | Unit | Description |
| ------------------ | ------------------------------- | ----- | --------------- |
| Container CPU usage | ContainerCpuUsed | Cores | Container CPU usage |
| Container CPU utilization (for node) | ContainerCpuUsageForNode | % | Container CPU utilization for node |
| Container CPU utilization (for request) | ContainerCpuUsageForRequest | % | Container CPU utilization for request |
| Container CPU utilization (for limit) | ContainerCpuUsageForLimit | % | Container CPU utilization for limit |
| Container memory usage | ContainerMemUsed | MiB | Container memory usage |
| Container memory utilization (for node) | ContainerMemUsageForNode | % | Container memory utilization for node |
| Container memory utilization (for request) | ContainerMemUsageForRequest | % | Container memory utilization for request |
| Container memory utilization (for limit) | ContainerMemUsageForLimit | % | Container memory utilization for limit |
| Container disk read traffic | ContainerDiskReadTraffic | KB/s | Container disk read traffic |
| Container disk write traffic | ContainerDiskWriteTraffic | KB/s | Container disk write traffic |
| Container disk read IOPS | ContainerDiskRead | Count | Container disk read IOPS |
| Container disk write IOPS | ContainerDiskWrite | Count | Container disk write IOPS |



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

### Sample 1 Getting the container CPU usage of one TKE containers
This example shows you how to get the container CPU usage of one TKE container using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/DOCKER
&MetricName=ContainerCpuUsed
&Period=60
&StartTime=2019-06-17T16:35:00+08:00
&EndTime=2019-06-17T16:40:00+08:00
&Instances.0.Dimensions.0.Name=clusterId
&Instances.0.Dimensions.0.Value=cls-12345
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=default
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=monitor
&Instances.0.Dimensions.3.Name=podName
&Instances.0.Dimensions.3.Value=monitor-68b6db4956-12345
&Instances.0.Dimensions.4.Name=containerId
&Instances.0.Dimensions.4.Value=abcd1234efg
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-06-17 16:35:00",
"EndTime": "2019-06-17 16:40:00",
"Period": 60,
"MetricName": "ContainerCpuUsed",
"DataPoints": [
{
"Dimensions": [
{
"Name": "clusterId",
"Value": "cls-12345"
},
{
"Name": "containerId",
"Value": "abcd1234efg"
},
{
"Name": "namespace",
"Value": "default"
},
{
"Name": "podName",
"Value": "monitor-68b6db4956-12345"
},
{
"Name": "serviceName",
"Value": "monitor"
}
],
"Timestamps": [
1560760500,
1560760560,
1560760620,
1560760680,
1560760740,
1560760800
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
"RequestId": "3a0008c9-ecc6-48aa-9033-8f37144cc816"
}
}
```
### Sample 2. Getting the container CPU usage of multiple TKE containers
This example shows you how to get the container CPU usage of multiple TKE containers using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/BLOCK_STORAGE
&MetricName=DiskUtil
&Period=60
&StartTime=2019-06-17T16:35:00+08:00
&EndTime=2019-06-17T16:40:00+08:00
&Instances.0.Dimensions.0.Name=clusterId
&Instances.0.Dimensions.0.Value=cls-12345
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=default
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=monitor
&Instances.0.Dimensions.3.Name=podName
&Instances.0.Dimensions.3.Value=monitor-68b6db4956-12345
&Instances.0.Dimensions.4.Name=containerId
&Instances.0.Dimensions.4.Value=abcd1234efg
&Instances.1.Dimensions.0.Name=clusterId
&Instances.1.Dimensions.0.Value=cls-123456
&Instances.1.Dimensions.1.Name=namespace
&Instances.1.Dimensions.1.Value=default
&Instances.1.Dimensions.2.Name=serviceName
&Instances.1.Dimensions.2.Value=monitor
&Instances.1.Dimensions.3.Name=podName
&Instances.1.Dimensions.3.Value=monitor-68b6db4956-12345
&Instances.1.Dimensions.4.Name=containerId
&Instances.1.Dimensions.4.Value=abcd1234efg
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-06-17 16:35:00",
"EndTime": "2019-06-17 16:40:00",
"Period": 60,
"MetricName": "ContainerCpuUsed",
"DataPoints": [
{
"Dimensions": [
{
"Name": "clusterId",
"Value": "cls-12345"
},
{
"Name": "containerId",
"Value": "abcd1234efg"
},
{
"Name": "namespace",
"Value": "default"
},
{
"Name": "podName",
"Value": "monitor-68b6db4956-12345"
},
{
"Name": "serviceName",
"Value": "monitor"
}
],
"Timestamps": [
1560760500,
1560760560,
1560760620,
1560760680,
1560760740,
1560760800
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
"Name": "clusterId",
"Value": "cls-123456"
},
{
"Name": "containerId",
"Value": "abcd1234efg"
},
{
"Name": "namespace",
"Value": "default"
},
{
"Name": "podName",
"Value": "monitor-68b6db4956-12345"
},
{
"Name": "serviceName",
"Value": "monitor"
}
],
"Timestamps": [
1560760500,
1560760560,
1560760620,
1560760680,
1560760740,
1560760800
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
"RequestId": "3a0008c9-ecc6-48aa-9033-8f37144cc816"
}
}
```