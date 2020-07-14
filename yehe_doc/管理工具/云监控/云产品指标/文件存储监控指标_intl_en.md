## Namespace

Namespace=QCE/CFS

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ------------------|---- | --------- | ---- | ---- |
| Storage | Storage capacity of the file system | Current storage capacity of the file system | GB | FileSystemId |
| DataReadIoBytes | Read bandwidth | Average amount of data read by the file system per second | KB/s | FileSystemId |
| DataWriteIoBytes | Write bandwidth | Average amount of data written to the file system per second | KB/s | FileSystemId |
| DataReadIoCount | Read IOPS | Average number of reads from the file system per second | Times/sec | FileSystemId |
| DataWriteIoCount | Write IOPS | Average number of writes to the file system per second | Times/sec | FileSystemId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ------------ | -------------------- | --------------------------------------- |
| Instances.N.Dimensions.0.Name | FileSystemId | Dimension name of the file system ID | Enter a string-type dimension name, such as FileSystemId |
| Instances.N.Dimensions.0.Value | FileSystemId | A specific file system ID | Enter a specific file system ID, such as cfs-fjojeogej |

## Input Parameters

To query the monitoring data of the file storage, use the following input parameters: 

&Namespace=QCE/CFS
&Instances.N.Dimensions.0.Name=FileSystemId
&Instances.N.Dimensions.0.Value=<File system ID> 
