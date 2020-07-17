## Namespace

Namespace=QCE/BLOCK_STORAGE

## Monitoring Metrics

| Metric | Meaning | Description | Unit | Dimension |
| ---------------- | ---------------- | ------------------------------------------------------------ | ---- | ------------------- |
| DiskReadIops | Disk read IOPS | Number of I/O operations of reading data from block storage to the memory in a second | - | diskId |
| DiskReadTraffic | Disk read traffic | Rate of reading data from block storage to the memory | KB/s | diskId |
| DiskWriteIops | Disk write IOPS | Number of I/O operations of writing data from the memory to block storage in a second | - | diskId |
| DiskWriteTraffic | Disk write traffic | Rate of writing data from the memory to block storage | KB/s | diskId |
| DiskAwait | Disk I/O waiting time | Percentage of time during which the CPU is idle with pending I/O requests | ms | diskId |
| DiskSvctm | Disk I/O service time | I/O service time | ms | diskId |
| DiskUtil | Ratio of busy disk I/O periods | Ratio of busy time (non-idle time) during which I/O operations run on the disk | % | diskId |
| DiskUsage | Disk partition usage | Percentage of the used disk partition capacity to the total disk capacity | % | InstanceId |

> ? The statistical granularity (`period`) may vary for different metrics. You can obtain the `period` supported by each metric by calling [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882).

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------- | ------------------------- | ----------------------------------- |
| Instances.N.Dimensions.0.Name | diskId | Dimension name of the block storage instance ID | Enter a string-type dimension name, such as diskId. |
| Instances.N.Dimensions.0.Value | diskId | ID of the block storage instance | Enter a specific instance ID, such as disk-test. |
| Instances.N.Dimensions.0.Name | InstanceId | Dimension name of the disk partition instance ID | Enter a string-type dimension name, such as InstanceId. |
| Instances.N.Dimensions.0.Value | InstanceId | ID of the disk partition instance | Enter a specific instance ID, such as ins-mm8bs222. |

## Input Parameters

Block storage allows you to combine the following two dimensions when querying monitoring data. The values of the two types of input parameters are set as follows:

#### 1. To query the monitoring data of block storage, set the input parameters as follows:

&Namespace=QCE/BLOCK_STORAGE
&Instances.N.Dimensions.0.Name=diskId
&Instances.N.Dimensions.0.Value=<Block storage ID>

#### 2. To query the disk partition usage of the server, set the input parameters as follows: 
&Namespace=QCE/BLOCK_STORAGE
&Instances.N.Dimensions.0.Name=InstanceId 
&Instances.N.Dimensions.0.Value=<ID of the disk partition instance>
