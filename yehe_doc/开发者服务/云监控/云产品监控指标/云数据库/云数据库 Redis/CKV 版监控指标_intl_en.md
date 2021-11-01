## Namespace

Namespace=QCE/REDIS

## Monitoring Metrics

| Metric Name | Parameter | Collection Method (in Linux) | Statistical Method | Unit | Dimension |
| ----------- | ---------------- | ---------------------------------------- | ------------------------- | ----- | ----- |
| Total requests | Qps | Total number of commands within 1 minute divided by 60 | This metric is collected every minute, and its value at the 5-minute granularity is its average over the last 5 minutes | Times/sec | redis_uuid |
| Connections | Connections | Total number of connections within 1 minute | This metric is collected every minute, and its value at the 5-minute granularity is its sum over the last 5 minutes | Count | redis_uuid |
| CPU utilization | CpuUs | Percentage of time during which the CPU is occupied, which is calculated by obtaining `/proc/stat` data | This metric is collected every minute, and its value at the 5-minute granularity is its average over the last 5 minutes | % | redis_uuid |
| Inbound traffic | InFlow | Sum of inbound traffic within 1 minute | This metric is collected every minute, and its value at the 5-minute granularity is its sum over the last 5 minutes | Mb/min | redis_uuid |
| Total keys | Keys | Maximum number of keys within 1 minute | This metric is collected every minute, and its value at the 5-minute granularity is its maximum over the last 5 minutes | Count | redis_uuid |
| Outbound traffic | OutFlow | Sum of outbound traffic within 1 minute | This metric is collected every minute, and its value at the 5-minute granularity is its sum over the last 5 minutes | Mb/min | redis_uuid |
| Write requests | StatGet | Number of get/hget/hgetall/hmget/mget/getbit/getrange command requests within 1 minute | This metric is collected every minute, and its value at the 5-minute granularity is its sum over the last 5 minutes | Times/min | redis_uuid |
| Read requests | StatSet | Number of set/hset/hmset/hsetnx/lset/mset/msetx/setbit/setex/setrange/setnx command requests within 1 minute | This metric is collected every minute, and its value at the 5-minute granularity is its sum over the last 5 minutes | Times/min | redis_uuid |
| Memory usage | Storage | Maximum consumed capacity within 1 minute | This metric is collected every minute, and its value at the 5-minute granularity is its maximum over the last 5 minutes | MB/min | redis_uuid |
| Memory utilization | StorageUs | Maximum percentage of the consumed capacity within 1 minute | This metric is collected every minute, and its value at the 5-minute granularity is its maximum over the last 5 minutes | % | redis_uuid |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension
| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | redis_uuid | Dimension name of the instance ID | Enter a string-type dimension name, such as redis_uuid |
| Instances.N.Dimensions.0.Value | redis_uuid | A specific instance ID | Enter a specific instance ID on TencentDB for Redis, such as crs-123456 |

## Input Parameters

To query the monitoring data of a TencentDB for Redis instance, use the following input parameters:
&Namespace= QCE/REDIS
&Instances.N.Dimensions.0.Name=redis_uuid
&Instances.N.Dimensions.0.Value=<Instance uuid> 
