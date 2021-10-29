## Namespace

Namespace=QCE/DOCKER

## Monitoring Metrics

| Metric | Parameter | Unit | Description | Dimension |
| ------------------------- | ------------------------- | ---- | ------------------------------------ | --------------------------------- |
| Service CPU usage | ServiceCpuUsed | Cores | Sum of the CPU usage of all pods in a service | clusterId, serviceName, namespace |
| Service CPU utilization (for cluster) | ServiceCpuUsageForCluster | % | Ratio of the service CPU usage to the total cluster CPU configuration | clusterId, serviceName, namespace |
| Service memory usage | ServiceMemUsed | MiB | Sum of the memory usage of all pods in a service | clusterId, serviceName, namespace |
| Service memory utilization (for cluster) | ServiceMemUsageForCluster | % | Ratio of the service memory usage to the total cluster memory configuration | clusterId, serviceName, namespace |
| Service network inbound traffic | ServiceInFlux | MB | Sum of the inbound traffic of all pods in a service in the time window | clusterId, serviceName, namespace |
| Service network outbound traffic | ServiceOutFlux | MB | Sum of the outbound traffic of all pods in a service in the time window | clusterId, serviceName, namespace |
| Service network inbound bandwidth | ServiceInBandwidth | Mbps | Sum of the inbound bandwidth of all pods in a service | clusterId, serviceName, namespace |
| Service network outbound bandwidth | ServiceOutBandwidth | Mbps | Sum of the outbound bandwidth of all pods in a service | clusterId, serviceName, namespace |
| Service network inbound packets | ServiceInPackets | Packets/sec | Sum of the inbound packets of all pods in a service | clusterId, serviceName, namespace |
| Service network outbound packets | ServiceOutPackets | Packets/sec | Sum of the outbound packets of all pods in a service | clusterId, serviceName, namespace |

>?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ----------- | ------------------------------------------------------------ | ------------------------------------ |
| Instances.N.Dimensions.0.Name | clusterId | Cluster ID dimension name | Enter a string-type dimension name: clusterId |
| Instances.N.Dimensions.0.Value | clusterId | Specific cluster ID, namely, the `clusterId` field returned by the [DescribeClusters](https://intl.cloud.tencent.com/document/product/457/32025) API | Enter a specific cluster ID, such as `cls-xxxxx` |
| Instances.N.Dimensions.1.Name | serviceName | Service name | Enter a string-type dimension name: serviceName |
| Instances.N.Dimensions.1.Value | serviceName | Specific service name, which can be queried by the [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) | Enter a specific service name, such as `test` |
| Instances.N.Dimensions.2.Name | namespace | Namespace dimension name | Enter a string-type dimension name: namespace |
| Instances.N.Dimensions.2.Value | namespace | Specific namespace name, which can be queried by the [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) | Enter a specific namespace name, such as `default` |

## Input Parameter Description

**To query the monitoring data of TKE in the service dimension, set the following input parameters:**
&Namespace=QCE/DOCKER
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value=Cluster ID
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=Namespace
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=Service name

