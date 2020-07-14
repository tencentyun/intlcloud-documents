## Namespace

Namespace=QCE/DOCKER

## Monitoring Metrics

| Metric Name | Parameter | Unit | Description | Dimension |
| ------------------------- | ------------------------- | ---- | ------------------------------------ | --------------------------------- |
| Service CPU utilization | ServiceCpuUsed | Core | Sum of the CPU usage of all container instances in a service | clusterId, serviceName, and namespace |
| Service CPU utilization (for the cluster) | ServiceCpuUsageForCluster | % | Ratio of the service CPU usage to the total cluster CPU configuration | clusterId, serviceName, and namespace |
| Service memory usage | ServiceMemUsed | MiB | Sum of the memory usage of all container instances in a service | clusterId, serviceName, and namespace |
| Service memory utilization (for the cluster) | ServiceMemUsageForCluster | % | Ratio of the service memory usage to the total cluster memory configuration | clusterId, serviceName, and namespace |
| Service network inbound traffic | ServiceInFlux | MB | Sum of the inbound traffic of all instances in a service in the time window | clusterId, serviceName, and namespace |
| Service network outbound traffic | ServiceOutFlux | MB | Sum of the outbound traffic of all instances in a service in the time window | clusterId, serviceName, and namespace |
| Service network inbound bandwidth | ServiceInBandwidth | Mbps | Sum of the inbound bandwidth of all instances in a service | clusterId, serviceName, and namespace |
| Service network outbound bandwidth | ServiceOutBandwidth | Mbps | Sum of the outbound bandwidth of all instances in a service | clusterId, serviceName, and namespace |
| Service network inbound packets | ServiceInPackets | Packets/sec | Sum of the inbound packets of all instances in a service | clusterId, serviceName, and namespace |
| Service network outbound packets | ServiceOutPackets | Packets/sec | Sum of the outbound packets of all instances in a service | clusterId, serviceName, and namespace |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ----------- | ------------------------------------------------------------ | ------------------------------------ |
| Instances.N.Dimensions.0.Name | clusterId | Dimension name of the cluster ID | Enter a string-type dimension name, such as clusterId |
| Instances.N.Dimensions.0.Value | clusterId | A specific cluster ID, namely the clusterId field returned by the [cluster list query](https://intl.cloud.tencent.com/document/product/457/32025) API | Enter a specific cluster ID, such as cls-xxxxx |
| Instances.N.Dimensions.1.Name | serviceName | Service name | Enter a string-type dimension name, such as serviceName |
| Instances.N.Dimensions.1.Value | serviceName | A specific service name, namely the serviceName field returned by the [service list query](https://intl.cloud.tencent.com/document/product/457/32025) API | Enter a specific service name, such as test |
| Instances.N.Dimensions.2.Name | namespace | Dimension name of the namespace | Enter a string-type dimension name, such as namespace |
| Instances.N.Dimensions.2.Value | namespace | A specific namespace name, namely the namespace field returned by the service list query API | Enter a specific namespace name, such as default |

## Input Parameters

To query the monitoring data of the TKE service dimension, use the following input parameters:
&Namespace=QCE/DOCKER
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value=<Cluster ID>
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=<Namespace name>
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=<Service name>

