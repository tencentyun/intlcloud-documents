## Namespace

Namespace=QCE/BLOCK_STORAGE

## Monitoring Metrics

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ---------------- | -------------- | ---------------- | ---- | ---------- | ---------------------------------- |
| DiskReadTraffic  | Disk read traffic     | Disk read traffic per second   | KB/s | diskId    | 60s, 300s, <br/>3600s, 86400s      |
| DiskWriteTraffic | Disk write traffic     | Disk write traffic per second   | KB/s | diskId     | 60s, 300s, <br/>3600s, 86400s      |
| DiskReadIops     | Disk read IOPS     | Number of disk reads per second | -   | diskId    | 10s, 60s, 300s, <br/>3600s, 86400s |
| DiskWriteIops    | Disk write IOPS     | Number of disk writes per second | -   | diskId     | 10s, 60s, 300s, <br/>3600s, 86400s |
| DiskAwait        | Disk IO wait time | Disk IO wait time   | ms   | diskId     | 10s, 60s, 300s, <br/>3600s, 86400s |
| DiskSvctm        | Disk IO service time | Disk IO service time   | ms   | diskId    | 10s, 60s, 300s, <br/>3600s, 86400s |
| DiskUtil         | Disk IO utilization | Disk IO utilization   | %    | diskId     | 10s, 60s, 300s, <br/>3600s, 86400s |
| DiskUsage        | Disk utilization     | Disk utilization       | %    | InstanceId | 60s, 300s, <br/>3600s, 86400s |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ---------- | ------------------------- | ----------------------------------- |
| Instances.N.Dimensions.0.Name  | diskId     | Cloud disk ID dimension name | Enter a String-type dimension name: diskId     |
| Instances.N.Dimensions.0.Value | diskId   | Specific cloud disk ID            | Enter a specific cloud disk ID, such as `disk-test`    |
| Instances.N.Dimensions.0.Name  | InstanceId | Disk partition instance ID dimension name | Enter a String-type dimension name: InstanceId |
| Instances.N.Dimensions.0.Value | InstanceId | Specific disk partition instance ID     | Enter a specific instance ID, such as `ins-mm8bs222` |

## Input Parameter Description

CBS monitoring data can be queried based on the following two combinations of dimensions. The values for input parameters are as follows:

#### 1. To query the monitoring data of a cloud disk, use the following input parameters:

&Namespace=QCE/BLOCK_STORAGE
&Instances.N.Dimensions.0.Name=diskId
&Instances.N.Dimensions.0.Value=Cloud disk ID

#### 2. To query the disk partition utilization of a server, use the following input parameters: 
&Namespace=QCE/BLOCK_STORAGE
&Instances.N.Dimensions.0.Name=InstanceId 
&Instances.N.Dimensions.0.Value=Specific disk partition instance ID
