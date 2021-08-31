
## Namespace

Namespace=QCE/DOCKER

## Monitoring Metrics

| Metric | Parameter | Unit | Description | Dimension |
| ------------------ | ------------------------------- | ----- | --------------- | --------------- |
| Container CPU usage | ContainerCpuUsed | Cores | Container CPU usage | clusterId, <br>serviceName, <br>namespace, <br>podName, <br>containerId |
| Container CPU utilization (for server) | ContainerCpuUsageForNode | % | Ratio of the container CPU usage to the server CPU configuration | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container CPU utilization (for Request) | ContainerCpuUsageForRequest | % | Ratio of the container CPU usage to the CPU configuration for Request | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container CPU utilization (for Limit) | ContainerCpuUsageForLimit | % | Ratio of the container CPU usage to the CPU configuration for Limit | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container memory usage | ContainerMemUsed | MiB | Container memory usage | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container memory utilization (for server) | ContainerMemUsageForNode | % | Ratio of the container memory usage to the server memory configuration | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container memory utilization (for Request) | ContainerMemUsageForRequest | % | Ratio of the container memory usage to the memory configuration for Request | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container memory utilization (for Limit) | ContainerMemUsageForLimit | % | Ratio of the container memory usage to the memory configuration for Limit | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container disk read traffic | ContainerDiskReadTraffic | KB/s | Disk read traffic for the container | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container disk write traffic | ContainerDiskWriteTraffic | KB/s | Disk write traffic for the container | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container disk read IOPS | ContainerDiskRead | Count | Disk read IOPS for the container | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |
| Container disk write IOPS | ContainerDiskWrite | Count | Disk write IOPS for the container | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>containerId |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values and dimensions supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ----------- | ------------------------------------------------------------ | --------------------------------------------- |
| Instances.N.Dimensions.0.Name | clusterId | Cluster ID dimension name | Enter a string-type dimension name: clusterId |
| Instances.N.Dimensions.0.Value | clusterId | Specific cluster ID, namely, the `clusterId` field returned by the [DescribeClusters](https://intl.cloud.tencent.com/document/product/457/32025) API | Enter a specific cluster ID, such as `cls-xxxxx` |
| Instances.N.Dimensions.1.Name | serviceName | Service dimension name | Enter a string-type dimension name: serviceName |
| Instances.N.Dimensions.1.Value | serviceName | Service name, which can be queried by the [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) | Enter a specific service name, such as `test` |
| Instances.N.Dimensions.2.Name | namespace | Namespace dimension name | Enter a string-type dimension name: namespace |
| Instances.N.Dimensions.2.Value | namespace | Specific namespace name, which can be queried by the [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) | Enter a specific namespace name, such as `default` |
| Instances.N.Dimensions.3.Name | podName | Pod dimension name | Enter a string-type dimension name: podName |
| Instances.N.Dimensions.3.Value | podName | Specific pod name, which can be queried by the [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) | Enter a specific pod name, such as `test-3488000495-nj6s9` |
| Instances.N.Dimensions.4.Name | containerId | Container ID dimension name | Enter a string-type dimension name: containerId |
| Instances.N.Dimensions.4.Value | containerId | Specific container ID, namely, the `containerId` field returned by the `DescribeClusters` API. Note that it is sufficient to take the first 12 characters of the container ID for this parameter | Enter a specific container name, such as `01c5509d2b39` |

## Input Parameter Description

**To query the monitoring data of TKE in the container dimension, set the following input parameters:**

&Namespace=QCE/DOCKER
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value=Cluster ID 
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=Namespace
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=Service name
&Instances.0.Dimensions.3.Name=podName
&Instances.0.Dimensions.3.Value=Pod name
&Instances.0.Dimensions.4.Name=containerId
&Instances.0.Dimensions.4.Value=Container ID
