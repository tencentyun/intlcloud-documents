## Namespace

Namespace=QCE/CFS

## Monitoring Metrics

### Bandwidth

| Parameter | Metric | Description | Unit | Dimension |
| --------------- | ---------- | ------------------------------ | ---- | ------------ |
| DataReadIoBytes | Read bandwidth | Average volume of data read from file system per second | KB/s | FileSystemId |
| DataWriteIoBytes | Write bandwidth | Average volume of data written to file system per second | KB/s | FileSystemId |

### Reads and writes

| Parameter | Metric | Description | Unit | Dimension |
| ---------------- | ---------- | ---------------------------- | ----- | ------------ |
| DataReadIOPS | Read IOPS | Average number of reads from file system per second | Reads/sec | FileSystemId |
| DataWriteIOPS | Write IOPS | Average number of writes to file system per second | Writes/sec | FileSystemId |

### Storage

| Parameter | Metric | Description | Unit | Dimension |
| ---------- | -------------- | ------------------------ | ---- | ------------ |
| Storage | File system storage capacity | Current storage capacity of file system | GB | FileSystemId |

### Latency

| Parameter | Metric | Description | Unit | Dimension |
| ------------------ | ---------- | -------------------- | ---- | ------------ |
| DataReadIoLatency  | Read latency   | Average read latency of file system | ms   | FileSystemId |
| DataWriteIoLatency | Write latency   | Average write latency of file system | ms   | FileSystemId |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ------------ | -------------------- | --------------------------------------- |
| Instances.N.Dimensions.0.Name  | FileSystemId | File system ID dimension name | Enter a String-type dimension name: FileSystemId    |
| Instances.N.Dimensions.0.Value | FileSystemId | Specific file system ID       | Enter a specific file system ID, such as `cfs-fjojeogej` |

## Input Parameter Description

To query the monitoring data of a CFS file system, set the following input parameters: 

&Namespace=QCE/CFS
&Instances.N.Dimensions.0.Name=FileSystemId
&Instances.N.Dimensions.0.Value=file system ID 
