## Namespace

Namespace=QCE/BLOCK_STORAGE

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ------------------ | -------- | ---------------------- |---- | ------------ |
| DiskReadIops | Disk read IOPS | Number of I/O operations of reading data from block storage to the memory | Times | diskId and InstanceId |
| DiskReadTraffic | Disk read traffic | Rate of reading data from block storage to the memory | KB/s | diskId and InstanceId |
| DiskWriteIops | Disk write IOPS | Number of I/O operations of writing data from the memory to block storage | Times | diskId and InstanceId |
| DiskWriteTraffic | Disk write traffic | Rate of writing data from the memory to block storage | KB/s | diskId and InstanceId |
| DiskAwait | Disk I/O waiting time | Percentage of time during which the CPU is idle and there are pending I/O requests | ms | diskId and InstanceId |
| DiskSvctm | Disk I/O service time | I/O service time | ms | diskId and InstanceId |
| DiskUtil | Ratio of busy disk I/O periods | Ratio of non-idle time during which I/O operations run on the disk | % | diskId and InstanceId |
| DiskUsage | Disk partition usage | Percentage of the used disk partition capacity to the total capacity | % | diskId and InstanceId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | diskId | Dimension name of the block storage instance ID | Enter a string-type dimension name, such as diskId |
| Instances.N.Dimensions.0.Value | diskId | A specific ID of a block storage instance | Enter a specific instance ID, such as disk-test |
| Instances.N.Dimensions.0.Name | InstanceId | Dimension name of the disk partition instance ID | Enter a string-type dimension name, such as InstanceId |
| Instances.N.Dimensions.0.Value | InstanceId | A specific ID of a disk partition instance | Enter a specific instance ID, such as ins-mm8bs222 |

## Input Parameters

Block storage supports querying monitoring data by combining the following two dimensions. The following describes the input parameters:

1. To query the monitoring data of block storage, use the following input parameters:

&Namespace=QCE/BLOCK_STORAGE

&Instances.N.Dimensions.0.Name=diskId

&Instances.N.Dimensions.0.Value=<Block storage ID>

2. To query the disk partition usage of the server, use the following input parameters: 

&Namespace=QCE/BLOCK_STORAGE

&Instances.N.Dimensions.0.Name=InstanceId 

&Instances.N.Dimensions.0.Value=<CVM ID> 