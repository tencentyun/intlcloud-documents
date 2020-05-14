## 1. API Description

API: GetMonitorData
Domain name for API request: monitor.tencentcloudapi.com

This API is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric.

API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend that you spread the call requests over time.

To query the monitoring data of a TencentDB for MongoDB instance, use the following input parameters:
&Namespace= QCE/CMONGO
&Instances.N.Dimensions.0.Name=target
&Instances.N.Dimensions.0.Value=subject to query dimension

The following describes the valid values of `Instances.N.Dimensions.0.Value`. TencentDB for MongoDB is a cluster service. This API can be used to query the monitoring data in the "entire cluster", "specified replica set", or "specified node" dimension. The "entire instance" dimension represents a purchased TencentDB for MongoDB instance, and can be used to query the number of read/write requests, capacity utilization, or timed-out requests of the entire instance. The "specified replica set" dimension can be used to query the capacity utilization and master/slave lag of a specified replica set. The "specified node" dimension can be used to query information such as CPU and memory of a specified node in the cluster.

### dimensions.0.value reference table

| Value Type | Value Example | Description |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Instance ID   | cmgo-6ielucen                                                | Unique ID of a TencentDB for MongoDB instance, which can be queried in the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) or by calling TencentDB for MongoDB APIs |
| Replica set ID | cmgo-6ielucen_0cmgo-6ielucen_2                               | A replica set ID can be obtained by adding "_index number" after the instance ID. The "index number" starts at 0 and has a maximum value that equals to the number of replica sets - 1. A replica set instance has only one replica set and suffix "_0" is sufficient. A sharded instance has many shards, each of which is a replica set. For example, for the replica set ID of the third shard, suffix "_2" |
| Node ID   | cmgo-6ielucen_0-node-primarycmgo-6ielucen_1-node-slave0cmgo-6ielucen_3-node-slave2 | Add "-node-primary" after the replica set ID to get the master node ID of the replica set. Add "-node-slave node index number" to get the corresponding slave node ID. The "slave node index number" starts at 0 and has a maximum value that equals to the number of slave nodes - 1 |

## 2. Input Parameters

The list below contains only API request parameters and certain common parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. Please see the [region list](https://intl.cloud.tencent.com/document/product/240/32141#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by TencentDB for MongoDB |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/CMONGO` for TencentDB for MongoDB, which must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :------- | :------------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | target   | target   | String-type dimension name, such as target                           |
| Instances.N.Dimensions.0.Value | target   | Subject to the query dimension | Please see the [value reference table](https://intl.cloud.tencent.com/document/product/248/35671#dimensions.0.value-.E5.8F.96.E5.80.BC.E5.8F.82.E7.85.A7.E8.A1.A8) |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the period and dimension supported by each metric.

| Metric             | Description                                   | Unit | Cluster/Instance | dimensions.0.value Value |
| :--------------- | :------------------------------------- | :--- | :-------- | :--------------------- |
| Inserts          | Number of writes in unit time                     | -   | Cluster/instance | Instance ID                 |
| Reads            | Number of reads in unit time                     | -   | Cluster/instance | Instance ID                 |
| Updates          | Number of updates in unit time                     | -   | Cluster/instance | Instance ID                 |
| Deletes          | Number of deletions in unit time                     | -   | Cluster/instance | Instance ID                 |
| Counts           | Number of counts in unit time                     | -   | Cluster/instance | Instance ID                 |
| Aggregates       | Number of aggregates in unit time               | -   | Cluster/instance | Instance ID                 |
| ClusterDiskusage | Cluster capacity utilization                         | %    | Cluster/instance | Instance ID                 |
| Success          | Number of successful requests in unit time                 | -   | Cluster/instance | Instance ID                 |
| Delay10          | Number of successful requests with a delay of 10–50 ms in unit time  | -   | Cluster/instance | Instance ID                 |
| Delay50          | Number of successful requests with a delay of 50–100 ms in unit time  | -   | Cluster/instance | Instance ID                 |
| Delay100          | Number of successful requests with a delay of over 100 ms in unit time  | -   | Cluster/instance | Instance ID                 |
| ReplicaDiskusage | Replica set capacity utilization                       | %    | Replica set    | Replica set ID               |
| Slavedelay       | Average master/slave lag in unit time                 | Seconds   | Replica set    | Replica set ID               |
| Cpuusage         | CPU utilization                              | %    | Node      | Node ID                 |
| Memusage         | Memory utilization                             | %    | Node      | Node ID                 |
| Qr               | Read requests waiting in the queue               | Count   | Node      | Node ID                 |
| Qw               | Write requests waiting in the queue               | Count   | Node      | Node ID                 |
| Conn             | Connections                                 | Count   | Node      | Node ID                 |
| Netin            | Network inbound traffic                             | MB/s | Node      | Node ID                 |
| Netout           | Network outbound traffic                             | MB/s | Node      | Node ID                 |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique request ID, which is returned in each request. The `RequestId` is required to troubleshoot issues |

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

### Sample 1. Getting the number of writes of one TencentDB for MongoDB instance in unit time

This example shows you how to get the monitoring data for the number of writes in unit time of one TencentDB for MongoDB instance using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/CMONGO
&MetricName=Inserts
&Period=60
&StartTime=2019-06-17T20:20:00+08:00
&EndTime=2019-06-178T20:25:00+08:00
&Instances.0.Dimensions.0.Name=target
&Instances.0.Dimensions.0.Value=cmgo-g9c1234
&[<Common request parameters>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### Output sample code

```
{
  "Response": {
    "StartTime": "2019-06-17 20:20:00",
    "EndTime": "2019-06-17 20:25:00",
    "Period": 60,
    "MetricName": "Inserts",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "target",
            "Value": "cmgo-g9c1234"
          }
        ],
        "Timestamps": [
          1560774000,
          1560774060,
          1560774120,
          1560774180,
          1560774240,
          1560774300
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
    "RequestId": "d133e798-4d13-4ecf-af21-cce93967811c"
  }
}
```

### Sample 2. Getting the number of writes of multiple TencentDB for MongoDB instances in unit time

This example shows you how to get the monitoring data for the number of writes in unit time of multiple TencentDB for MongoDB instances using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CMONGO
&MetricName=Inserts
&Period=60
&StartTime=2019-06-17T20:20:00+08:00
&EndTime=2019-06-178T20:25:00+08:00
&Instances.0.Dimensions.0.Name=target
&Instances.0.Dimensions.0.Value=cmgo-g9c1234
&Instances.1.Dimensions.0.Name=target
&Instances.1.Dimensions.0.Value=cmgo-g9c12345
&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "StartTime": "2019-06-17 20:20:00",
    "EndTime": "2019-06-17 20:25:00",
    "Period": 60,
    "MetricName": "Inserts",
    "DataPoints": [
      {
        "Dimensions": [
          {
            "Name": "target",
            "Value": "cmgo-g9c1234"
          }
        ],
        "Timestamps": [
          1560774000,
          1560774060,
          1560774120,
          1560774180,
          1560774240,
          1560774300
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
            "Name": "target",
            "Value": "cmgo-g9c12345"
          }
        ],
        "Timestamps": [
          1560774000,
          1560774060,
          1560774120,
          1560774180,
          1560774240,
          1560774300
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
    "RequestId": "d133e798-4d13-4ecf-af21-cce93967811c"
  }
}
```