## 1. API Description

API: GetMonitorData
Domain name for API request: `monitor.tencentcloudapi.com`

This API can be used to get the monitoring data of **Redis 2.8, 4.0, and 5.0 Standard Edition and Cluster Edition**. It is used to get the monitoring data of a Tencent Cloud product by passing in the product's namespace, object dimension, and monitoring metric. API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points. This API may fail due to the rate limit if you need to call many metrics and objects. We recommend that you distribute call requests across a period of time.

To query the monitoring data of a TencentDB for Redis instance, use the following input parameters:
&Namespace=QCE/REDIS
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=Instance ID

## 2. Input Parameters

The list below contains only the API request parameters and some common request parameters. Common request parameters need to be added when a call is made. For more information, see [Common Params](https://intl.cloud.tencent.com/document/product/248/33876#.E7.AD.BE.E5.90.8D.E6.96.B9.E6.B3.95-v1).

### 2.1 Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| :---------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/product/239/32045) supported by TencentDB for Redis |
| Namespace | Yes | String | Namespace. Each Tencent Cloud service has a namespace, such as QCE/REDIS for TencentDB for Redis. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Timestamp | Start time, such as "2016-01-01 10:25:00". The default value is "00:00:00" of the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `endTime` cannot be earlier than `startTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :--------- | :----------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.Name | instanceid | Instance ID | Enter a string-type dimension name, such as instanceId |
| Instances.N.Dimensions.0.Value | instanceid | Specific instance ID | Enter a specific TencentDB for Redis instance ID such as tdsql-123456. This ID is the instance serial number, such as crs-ifmymj41, which can be queried through the [DescribeRedis](https://intl.cloud.tencent.com/document/product/239/1384) API |
| Instances.N.Dimensions.1.Name | clusterid | Shard ID | Enter a string-type dimension name, such as clusterid. If the overall information is to be pulled, do not pass in this parameter. If the shard information is to be pulled, the input parameter must be `clusterid` |
| Instances.N.Dimensions.1.Value | clusterid | Specific shard ID | Enter a specific shard ID such as: tdsql-123456, which can be obtained by running commands like `cluster nodes` |

### 2.2. Metric names

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` and `dimension` supported by each metric.

#### 2.2.1 Monitoring metrics for the standard edition

| Metric Name | Meaning | Unit | Description |
| :--------------- | :--------------- | :---- | :----------------------------------------------------------- |
| CpuUsMin | CPU utilization | % | Average CPU utilization |
| StorageMin | Memory usage | MB | Actually used memory capacity, including the capacities for data and cache |
| StorageUsMin | Memory utilization | % | Ratio of the actually used memory to the requested total memory |
| KeysMin | Total keys | - | Total number of keys stored in an instance (first-level keys) |
| ExpiredKeysMin | Expired keys | - | Number of keys expired in a time window, which corresponds to the `expired_keys` output by the `info` command |
| EvictedKeysMin | Evicted keys | - | Number of keys evicted in a time window, which corresponds to the `evicted_keys` output by the `info` command |
| ConnectionsMin | Connections | - | Number of TCP connections to an instance |
| ConnectionsUsMin | Connection utilization | % | Ratio of the actual number of TCP connections to the maximum number of connections |
| InFlowMin | Inbound traffic | MB/sec | Private inbound traffic |
| InFlowUsMin | Inbound traffic utilization | % | Ratio of actually used private inbound traffic to maximum traffic |
| OutFlowMin | Outbound traffic | MB/sec | Private outbound traffic |
| OutFlowUsMin | Outbound traffic utilization | % | Ratio of actually used private outbound traffic to maximum traffic |
| LatencyMin | Average execution latency | ms | Average execution latency between the proxy and the Redis server |
| LatencyGetMin | Average read latency | ms | Average execution latency of read commands between the proxy and the Redis server. For the classification of read commands, see monitoring description |
| LatencySetMin | Average write latency | ms | Average execution latency of write commands between the proxy and the Redis server. For the classification of write commands, see monitoring description |
| LatencyOtherMin | Average latency of other commands | ms | Average execution latency of commands other than read and write commands between the proxy and the Redis server. For the classification of other commands, see monitoring description |
| QpsMin | Total requests | Times/sec | QPS, that is, the number of command executions |
| StatGetMin | Read requests | Times/min | Number of read command executions. For the classification of read commands, see monitoring description |
| StatSetMin | Write requests | Times/min | Number of write command executions. For the classification of write commands, see monitoring description |
| StatOtherMin | Other requests | Times/sec | Number of the executions of commands other than read and write commands. For the classification of other commands, see monitoring description |
| BigValueMin | Big-value requests | Times/sec | Number of command executions for which the request size exceeds 32 KB |
| SlowQueryMin | Slow queries | - | Number of slow queries |
| StatSuccessMin | Read request hits | - | Number of existing read request keys, which corresponds to the `keyspace_hits` metric output by the `info` command |
| StatMissedMin | Read request misses | - | Number of nonexistent read request keys, which corresponds to the `keyspace_misses` metric output by the `info` command |
| CmdErrMin | Execution errors | - | Number of command execution errors, such as when a command does not exist or a parameter is incorrect |
| CacheHitRatioMin | Read request hit rate | % | Key hits/(Key hits + Key misses). This metric reflects the cache miss situation |

#### 2.2.2 Overall metrics for the cluster edition

| Metric Name | Meaning | Unit | Description |
| :--------------- | :----------------- | :---- | :----------------------------------------------------------- |
| CpuUsMin | Average CPU utilization | % | Average CPU utilization |
| CpuMaxUs | Maximum shard CPU utilization | % | Highest CPU utilization value of all shards in a cluster |
| StorageMin | Memory usage | MB | Actually used memory capacity, including the capacities for data and cache |
| StorageUsMin | Memory utilization | % | Ratio of the actually used memory to the requested total memory |
| StorageMaxUs | Maximum shard memory utilization | % | Highest memory utilization value of all shards in a cluster |
| KeysMin | Total keys | - | Total number of keys stored in an instance (first-level keys) |
| ExpiredKeysMin | Expired keys | - | Number of keys expired in a time window, which corresponds to the `expired_keys` output by the `info` command |
| EvictedKeysMin | Evicted keys | - | Number of keys evicted in a time window, which corresponds to the `evicted_keys` output by the `info` command |
| ConnectionsMin | Connections | - | Number of TCP connections to an instance |
| ConnectionsUsMin | Connection utilization | % | Ratio of the actual number of TCP connections to the maximum number of connections |
| InFlowMin | Inbound traffic | MB/sec | Private inbound traffic |
| InFlowUs | Inbound traffic utilization | % | Ratio of actually used private inbound traffic to maximum traffic |
| OutFlowMin | Outbound traffic | MB/sec | Private outbound traffic |
| OutFlowUs | Outbound traffic utilization | % | Ratio of actually used private outbound traffic to maximum traffic |
| LatencyMin | Average execution latency | ms | Average execution latency between the proxy and the Redis server |
| LatencyGetMin | Average read latency | ms | Average execution latency of read commands between the proxy and the Redis server. For the classification of read commands, see monitoring description |
| LatencySetMin | Average write latency | ms | Average execution latency of write commands between the proxy and the Redis server. For the classification of write commands, see monitoring description |
| LatencyOtherMin | Average latency of other commands | ms | Average execution latency of commands other than read and write commands between the proxy and the Redis server. For the classification of other commands, see monitoring description |
| QpsMin | Total requests | Times/sec | QPS, that is, the number of command executions |
| StatGetMin | Read requests | Times/sec | Number of read command executions. For the classification of read commands, see monitoring description |
| StatSetMin | Write requests | Times/sec | Number of write command executions. For the classification of write commands, see monitoring description |
| StatOtherMin | Other requests | Times/sec | Number of the executions of commands other than read and write commands. For the classification of other commands, see monitoring description |
| BigValueMin | Big-value requests | Times/sec | Number of command executions for which the request size exceeds 32 KB |
| SlowQueryMin | Slow queries | - | Number of command executions with a latency greater than the slowlog-log-slower-than configuration |
| StatSuccessMin | Read request hits | - | Number of existing read request keys, which corresponds to the `keyspace_hits` metric output by the `info` command |
| StatMissedMin | Read request misses | - | Number of nonexistent read request keys, which corresponds to the `keyspace_misses` metric output by the `info` command |
| CmdErrMin | Execution errors | - | Number of command execution errors, such as when a command does not exist or a parameter is incorrect |
| CacheHitRatioMin | Read request hit rate | % | Key hits/(Key hits + Key misses). This metric reflects the cache miss situation |

#### 2.2.3 Shard metrics for the cluster edition

| Metric Name | Meaning | Unit | Description |
| :--------------- | :----------- | :---- | :----------------------------------------------------------- |
| CpuUsMin | CPU utilization | % | Average CPU utilization |
| StorageMin | Memory usage | MB | Actually used memory capacity, including the capacities for data and cache |
| StorageUsMin | Memory utilization | % | Ratio of the actually used memory to the requested total memory |
| KeysMin | Total keys | - | Total number of keys stored in an instance (first-level keys) |
| ExpiredKeysMin | Expired keys | - | Number of keys expired in a time window, which corresponds to the `expired_keys` output by the `info` command |
| EvictedKeysMin | Evicted keys | - | Number of keys evicted in a time window, which corresponds to the `evicted_keys` output by the `info` command |
| QpsMin | Total requests | Times/sec | QPS, that is, the number of command executions |
| StatGetMin | Read requests | Times/sec | Number of read command executions. For the classification of read commands, see monitoring description |
| StatSetMin | Write requests | Times/sec | Number of write command executions. For the classification of write commands, see monitoring description |
| StatOtherMin | Other requests | Times/sec | Number of the executions of commands other than read and write commands. For the classification of other commands, see monitoring description |
| SlowQueryMin | Slow queries | - | Number of command executions with a latency greater than the slowlog-log-slower-than configuration |
| StatSuccessMin | Read request hits | - | Number of existing read request keys, which corresponds to the `keyspace_hits` metric output by the `info` command |
| StatMissedMin | Read request misses | - | Number of nonexistent read request keys, which corresponds to the `keyspace_misses` metric output by the `info` command |
| CmdErrMin | Execution errors | - | Number of command execution errors, such as when a command does not exist or a parameter is incorrect |
| CacheHitRatioMin | Read request hit rate | % | Key hits/(Key hits + Key misses). This metric reflects the cache miss situation. When the number of access requests is 0, the value of this metric is null |

## 3. Output Parameters

| Parameter Name | Type | Description |
| :--------- | :-------------------- | :----------------------------------------------------------- |
| MetricName | String | Monitoring metric |
| StartTime  | Timestamp | Data point start time |
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

## 5. Online Debugging

You can use the [online debugging tool](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=GetMonitorData&SignVersion=) to debug the API.

## 6. Samples

### Sample 1

This example shows you how to get the monitoring data for the number of GET commands of one TencentDB for Redis instance using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-1234567
&[<Common Request Parameters>](https://intl.cloud.tencent.com/document/product/248/4478)
```

#### Sample output code



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

### Sample 2

This example shows you how to get the monitoring data for the number of GET commands of multiple TencentDB for Redis instances using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



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

#### Sample output code



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

### Sample 3

This example shows you how to get the monitoring data for the number of GET commands of one TencentDB for Redis instance at shard-level using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



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
&[<Common Request Parameters>](https://intl.cloud.tencent.com/document/product/248/4478)
```

#### Sample output code



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

### Sample 4

This example shows you how to get the monitoring data for the number of GET commands of multiple TencentDB for Redis instances at shard-level using a statistical period of 60 seconds for a specified length of time.

#### Sample input code



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

#### Sample output code



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