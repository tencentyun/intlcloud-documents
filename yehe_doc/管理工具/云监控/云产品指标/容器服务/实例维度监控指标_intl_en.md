## Namespace

Namespace=QCE/DOCKER

## Monitoring Metrics

| Metric Name | Parameter | Unit | Description | Dimension |
| ------- | ----------------- | ---- | ------------------------- | ------------------------- |
| Pod network inbound bandwidth | PodInBandwidth | Mbps | Containers in the same pod share the same network. This parameter indicates the network inbound bandwidth of the pod | clusterId, serviceName, namespace, and podName |
| Pod network outbound bandwidth | PodOutBandwidth | Mbps | Containers in the same pod share the same network. This parameter indicates the network outbound bandwidth of the pod | clusterId, serviceName, namespace, and podName |
| Pod network inbound traffic | PodInFlux | MB | Containers in the same pod share the same network. This parameter indicates the network inbound traffic of the pod | clusterId, serviceName, namespace, and podName |
| Pod network outbound traffic | PodOutFlux | MB | Containers in the same pod share the same network. This parameter indicates the network outbound traffic of the pod | clusterId, serviceName, namespace, and podName |
| Pod network inbound packets | PodInPackets | Packets/sec | Containers in the same pod share the same network. This parameter indicates the network inbound packets of the pod | clusterId, serviceName, namespace, and podName |
| Pod network outbound packets | PodOutPackets | Packets/sec | Containers in the same pod share the same network. This parameter indicates the network outbound packets of the pod | clusterId, serviceName, namespace, and podName |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ----------- | ------------------------------------------------------------ | ---------------------------------------------- |
| Instances.N.Dimensions.0.Name | clusterId | Dimension name of the cluster ID | Enter a string-type dimension name, such as clusterId |
| Instances.N.Dimensions.0.Value | clusterId | A specific cluster ID; that is, the clusterId field returned by the [cluster list query](https://intl.cloud.tencent.com/document/product/457/32025) API | Enter a specific cluster ID, such as disk-test |
| Instances.N.Dimensions.1.Name | serviceName | Dimension name of the service | Enter a string-type dimension name, such as serviceName |
| Instances.N.Dimensions.1.Value | serviceName | A specific service name; that is, the serviceName field returned by the [service list query] API | Enter a specific service name, such as test |
| Instances.N.Dimensions.2.Name  | namespace | Dimension name of the namespace | Enter a string-type dimension name, such as namespace |
| Instances.N.Dimensions.2.Value | namespace | A specific namespace name; that is, the namespace field returned by the [service list query] API | Enter a specific namespace name, such as default |
| Instances.N.Dimensions.3.Name | podName | Dimension name of the pod | Enter a string-type dimension name, such as podName |
| Instances.N.Dimensions.3.Value | podName | A specific pod name; that is, the name field returned by the [service instance list query] API | Enter a specific pod name, such as test-3488000495-nj6s9 |

## Input Parameters

To query the monitoring data of a TKE pod dimension, use the following input parameters:

&Namespace=QCE/DOCKER
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value=<Cluster ID>
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value=<Namespace name>
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value=<Service name>
&Instances.0.Dimensions.3.Name=podName
&Instances.0.Dimensions.3.Value=<Pod name>

