## Namespace

Namespace=QCE/BLOCK_STORAGE

## Monitoring Metrics

| Metric | Meaning | Description | Unit | Dimension |
| ---------------- | ---------------- | ------------------------------------------------------------ | ---- | ------------------- |
| DiskReadIops | Disk read IOPS | Number of I/O reads from block storage to the memory per second | - | diskId |
| DiskReadTraffic | Disk read traffic | Rate at which data is read from block storage to the memory | KB/s | diskId |
| DiskWriteIops | Disk write IOPS | Number of I/O writes from the memory to block storage per second | - | diskId |
| DiskWriteTraffic | Disk write traffic | Rate at which data is written from the memory to block storage | KB/s | diskId |
| DiskAwait | Disk I/O waiting time | Percentage of time when the CPU is idle with pending I/O requests | ms | diskId |
| DiskSvctm | Disk I/O service time | I/O service time | ms | diskId |
| DiskUtil | Ratio of busy disk I/O periods | Ratio of non-idle time during which I/O operations run on the disk | % | diskId |
| DiskUsage | Disk partition usage | Percentage of used disk partition capacity to the total capacity | % | InstanceId |

> ? The statistical granularity (`period`) may vary by metrics. You can obtain the `period` supported by each metric by calling the [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Overview of parameters in each dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------- | ------------------------- | ----------------------------------- |
| Instances.N.Dimensions.0.Name | diskId | Dimension name of the block storage instance ID | Enter a string-type dimension name, such as diskId |
| Instances.N.Dimensions.0.Value | diskId | ID of the block storage instance | Enter a specific instance ID, such as disk-test |
| Instances.N.Dimensions.0.Name | InstanceId | Dimension name of the disk partition instance ID | Enter a string-type dimension name, such as InstanceId |
| Instances.N.Dimensions.0.Value | InstanceId | ID of the disk partition instance | Enter a specific instance ID, such as ins-mm8bs222 |

## Input Parameters

Block storage allows you to query monitoring data with the following two dimensional combinations. The input parameters are as follows:

#### 1. To query the monitoring data of block storage, configure input parameters as follows:

&Namespace=QCE/BLOCK_STORAGE
&Instances.N.Dimensions.0.Name=diskId
&Instances.N.Dimensions.0.Value=<Block storage ID>

#### 2. To query the disk partition usage of the server, configure input parameters as follows: 
&Namespace=QCE/BLOCK_STORAGE
&Instances.N.Dimensions.0.Name=InstanceId 
&Instances.N.Dimensions.0.Value=<ID of the disk partition instance>
