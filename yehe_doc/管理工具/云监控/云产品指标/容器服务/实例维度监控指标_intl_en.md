## Namespace

Namespace=QCE/DOCKER

## Monitoring Metrics

| Metric | Parameter | Unit | Description | Dimension |
| ------- | ----------------- | ---- | ------------------------- | ------------------------- |
| Pod network inbound bandwidth | PodInBandwidth | Mbps | Containers in the same pod share the same network. This parameter indicates the network inbound bandwidth of the pod | clusterId, serviceName, namespace, podName |
| Pod network outbound bandwidth | PodOutBandwidth | Mbps | Containers in the same pod share the same network. This parameter indicates the network outbound bandwidth of the pod | clusterId, serviceName, namespace, podName |
| Pod network inbound traffic | PodInFlux | MB | Containers in the same pod share the same network. This parameter indicates the network inbound traffic of the pod | clusterId, serviceName, namespace, podName |
| Pod network outbound traffic | PodOutFlux | MB | Containers in the same pod share the same network. This parameter indicates the network outbound traffic of the pod | clusterId, serviceName, namespace, podName |
| Pod network inbound packets | PodInPackets | Packets/sec | Containers in the same pod share the same network. This parameter indicates the network inbound packets of the pod | clusterId, serviceName, namespace, podName |
| Pod network outbound packets | PodOutPackets | Packets/sec | Containers in the same pod share the same network. This parameter indicates the network outbound packets of the pod | clusterId, serviceName, namespace, podName |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ----------- | ------------------------------------------------------------ | ---------------------------------------------- |
| Instances.N.Dimensions.0.Name | clusterId | Cluster ID dimension name | Enter a string-type dimension name: clusterId |
| Instances.N.Dimensions.0.Value | clusterId | Specific cluster ID, namely, the `clusterId` field returned by the [DescribeClusters](https://intl.cloud.tencent.com/document/product/457/32025) API | Enter a specific cluster ID, such as `disk-test` |
| Instances.N.Dimensions.1.Name | serviceName | Service dimension name | Enter a string-type dimension name: serviceName |
| Instances.N.Dimensions.1.Value | serviceName | Service name, which can be queried by the [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) | Enter a specific service name, such as test |
| Instances.N.Dimensions.2.Name | namespace | Namespace dimension name | Enter a string-type dimension name: namespace |
| Instances.N.Dimensions.2.Value | namespace | Specific namespace name, which can be queried by the [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) | Enter a specific namespace name, such as `default` |
| Instances.N.Dimensions.3.Name | podName | Pod dimension name | Enter a string-type dimension name: podName |
| Instances.N.Dimensions.3.Value | podName | Specific pod name, which can be queried by the [Kunbernetes API](https://kubernetes.io/zh/docs/concepts/overview/kubernetes-api/) | Enter a specific pod name, such as `test-3488000495-nj6s9` |

## Input Parameter Description

To query the monitoring data of TKE in the pod dimension, set the following input parameters:

&Namespace=QCE/DOCKER
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value=Cluster ID
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=Namespace
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=Service name
&Instances.0.Dimensions.3.Name=podName
&Instances.0.Dimensions.3.Value=Pod name

