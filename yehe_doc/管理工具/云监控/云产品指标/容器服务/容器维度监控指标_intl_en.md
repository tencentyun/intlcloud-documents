
## Namespace

Namespace=QCE/DOCKER

## Monitoring Metrics

| Metric Name | Parameter | Unit | Description | Dimension |
| ------------------ | ------------------------------- | ----- | --------------- | --------------- |
| Container CPU usage | ContainerCpuUsed | Core | Container CPU usage | clusterId, <br>serviceName, <br>namespace, <br>podName, <br>and containerId |
| Container CPU utilization (for the CVM) | ContainerCpuUsageForNode | % | Ratio of the container CPU usage to the CVM CPU configuration | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container CPU utilization (for Request) | ContainerCpuUsageForRequest | % | Ratio of the container CPU usage to the CPU configuration for Request | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container CPU utilization (for Limit) | ContainerCpuUsageForLimit | % | Ratio of the container CPU usage to the CPU configuration for Limit | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container memory usage | ContainerMemUsed | MiB | Container memory usage | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container memory utilization (for the CVM) | ContainerMemUsageForNode | % | Ratio of the container memory usage to the CVM memory configuration | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container memory utilization (for Request) | ContainerMemUsageForRequest | % | Ratio of the container memory usage to the memory configuration for Request | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container memory utilization (for Limit) | ContainerMemUsageForLimit | % | Ratio of the container memory usage to the memory configuration for Limit | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container disk read traffic | ContainerDiskReadTraffic | KB/s | Disk read traffic for the container | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container disk write traffic | ContainerDiskWriteTraffic | KB/s | Disk write traffic for the container | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container disk read IOPS | ContainerDiskRead | Count | Disk read IOPS for the container | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |
| Container disk write IOPS | ContainerDiskWrite | Count | Disk write IOPS for the container | clusterId, <br/>serviceName, <br/>namespace, <br/>podName, <br/>and containerId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ----------- | ------------------------------------------------------------ | ---------------------------------------------- |
| Instances.N.Dimensions.0.Name | clusterId | Dimension name of the cluster ID | Enter a string-type dimension name, such as clusterId |
| Instances.N.Dimensions.0.Value | clusterId | A specific cluster ID; that is, the clusterId field returned by the [cluster list query](https://intl.cloud.tencent.com/document/product/457/32025) API | Enter a specific cluster ID, such as cls-xxxxx |
| Instances.N.Dimensions.1.Name | serviceName | Dimension name of the service | Enter a string-type dimension name, such as serviceName |
| Instances.N.Dimensions.1.Value | serviceName | A specific service name; that is, the serviceName field returned by the [service list query] API | Enter a specific service name, such as test |
| Instances.N.Dimensions.2.Name | namespace | Dimension name of the namespace | Enter a string-type dimension name, such as namespace |
| Instances.N.Dimensions.2.Value | namespace | A specific namespace name; that is, the namespace field returned by the [service list query] API | Enter a specific namespace name, such as default |
| Instances.N.Dimensions.3.Name | podName | Dimension name of the pod | Enter a string-type dimension name, such as podName |
| Instances.N.Dimensions.3.Value | podName | A specific pod name; that is, the name field returned by the [service instance list query] API | Enter a specific pod name, such as test-3488000495-nj6s9 |
| Instances.N.Dimensions.4.Name | containerId | Dimension name of the container ID | Enter a string-type dimension name, such as containerId |
| Instances.N.Dimensions.4.Value | containerId | A specific container ID; that is, the containerId field returned by the [service instance list query] API. Note that it is sufficient to take the first 12 characters of the container ID for this parameter | Enter a specific container name, such as 01c5509d2b39 |

## Input Parameters

 To query the monitoring data of a TKE container dimension, use the following input parameters:

&Namespace=QCE/DOCKER
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value=<Cluster ID> 
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=<Namespace name>
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=<Service name>
&Instances.0.Dimensions.3.Name=podName
&Instances.0.Dimensions.3.Value=<Pod name>
&Instances.0.Dimensions.4.Name=containerId
&Instances.0.Dimensions.4.Value=<Container ID>
