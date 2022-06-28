## Notes

This document is only applicable to the [DescribeStatisticData](https://intl.cloud.tencent.com/document/product/248/39481) API.

## Namespace

Namespace = QCE/TKE2

## Monitoring Metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ------------------------------------------ | ------------------------------- | -------- | ----------------------- | ---------------------------------------- |
| K8sClusterCpuCoreTotal                     | Total number of CPU cores                   | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s             |
| K8sClusterFsReadTimes                      | Number of block device reads              | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterMemUsageBytes                    | Memory usage                  | MB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterNetwork<br/>TransmitBytes        | Network outbound traffic                  | MB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterRateCpu<br/>CoreRequestCluster   | CPU allocation                   | %        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterRateMem<br/>RequestBytesCluster  | Memory allocation                  | %        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterCpuCoreUsed                      | Number of used CPU cores                   | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s     |
| K8sClusterFsWriteBytes                     | Block device write size              | MB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterNetwork<br/>ReceiveBytes         | Network inbound traffic                  | MB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterNetwork<br/>TransmitBytesBw      | Network outbound bandwidth                  | MB/s     | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterRateCpu<br/>CoreUsedCluster      | CPU utilization                   | %        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterRateMem<br/>UsageBytesCluster    | Memory utilization                  | %        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterEtcdDb<br/>TotalSizeBytes        | etcd storage capacity                  | MB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterFsWriteTimes                     | Number of block device writes              | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterNetwork<br/>ReceiveBytesBw       | Network inbound bandwidth                  | B        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterNetwork<br/>TransmitPackets      | Network outbound packets                  | Count/s    | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterRateMemNo<br/>CacheBytesCluster  | Memory utilization (excluding cache)        | %        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterFsReadBytes                      | Block device read size              | MB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterMemoryTotal                      | Total memory                    | GB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterNetwork<br/>ReceivePackets       | Network inbound packets                  | Count/s    | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterMem<br/>NoCacheBytes             | Memory usage (excluding cache)        | MB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterAllocatable<br/>PodsTotal        | Number of allocatable pods         | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterGpu<br/>MemoryTotalBytes         | Total GPU memory                 | GB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterPods<br/>UsedTotal               | Number of pods                     | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterNodeTotal                        | Total number of nodes                    | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterGpu<br/>MemoryUsedBytes          | GPU memory usage               | MB       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterGpuTotal                         | Total number GPU cards                     | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterGpuUsed                          | Number of used GPU cards                   | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterRateGpu<br/>MemoryRequestCluster | GPU memory allocation               | %        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterRateGpu<br/>MemoryUsedCluster    | GPU memory utilization               | %        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterRate<br/>GpuRequestCluster       | GPU allocation                   | %        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterRate<br/>GpuUsedCluster          | GPU utilization                   | %        | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterEks<br/>CpuCoreUsed              | Number of used CPU cores                   | -       | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterEksMem<br/>NoCacheBytes          | Elastic container memory usage (excluding cache) | MB/s     | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sClusterEksMem<br/>UsageBytes            | Memory usage                  | MB/s     | tke_cluster_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |

## Statistical Granularity and Time Span

The supported time span varies by statistical granularity. When pulling monitoring data, you should pay attention to the time span restrictions as detailed below:

| Statistical Granularity | Maximum Time Span (End Time - Start Time) |
| -------- | ------------------------------------- |
| 60s      | 12 hours                                |
| 300s     | 3 days                                   |
| 3600s    | 30 days                                  |
| 86400s   | 186 days                                 |

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ----------------------- | -------------- | ------------------------------------------------- |
| Instances.N.Dimensions.N.Name  | tke_cluster_instance_id | Dimension name of the cluster | Enter a string-type dimension name, such as `tke_cluster_instance_id` |
| Instances.N.Dimensions.N.Value | tke_cluster_instance_id | Specific cluster ID    | Enter a specific cluster ID, such as cls-fvkxp123               |

## Input Parameter Description

**Use the following input parameters:**
&Namespace=QCE/TKE2
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123





