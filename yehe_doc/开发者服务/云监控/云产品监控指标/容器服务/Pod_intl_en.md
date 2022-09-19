## Notes

This document is only applicable to the [DescribeStatisticData](https://intl.cloud.tencent.com/document/product/248/39481) API. For all the following metrics, the `tke_cluster_instance_id` dimension is always required, one of other required dimensions must be passed in, and other dimensions are optional.

## Namespace

Namespace = QCE/TKE2

## Monitoring Metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ------------------------------ | ------------------------------------ | -------- | ------------------------------------------------------------ | ----------------------------------------- |
| K8sPodCpuCoreUsed              | CPU usage | Core | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodMemNoCacheBytes          | Memory usage (excluding cache) | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetworkReceivePackets    | Network inbound packets | Count/s | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateCpuCoreUsedLimit     | CPU utilization (usage/limit) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMemNoCacheNode       | Memory utilization (usage/node, excluding cache) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMemUsageRequest      | Memory usage (usage/request) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodFsReadBytes              | Block device read bandwidth | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodMemUsageBytes            | Memory usage | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetworkTransmitBytes     | Network outbound traffic | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateCpuCoreUsedNode      | CPU utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMemNoCacheRequest    | Memory utilization (usage/request, excluding cache) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRestartTotal             | Number of Pod restarts | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodFsReadTimes | Number of block device reads | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetworkReceiveBytes      | Network inbound traffic | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetworkTransmitBytesBw   | Network outbound bandwidth | MB/s | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateCpuCoreUsedRequest   | CPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMemUsageLimit        | Memory utilization (usage/limit) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodStatusReady | Pod_Ready status | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodFsWriteBytes | Block device write bandwidth | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetworkReceiveBytesBw    | Inbound bandwidth | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetworkTransmitPackets   | Network outbound packets | Count/s | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMemNoCacheLimit      | Memory utilization (usage/limit, excluding cache) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMemUsageNode         | Memory utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodFsWriteTimes | Number of block device writes | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateGpuMemoryUsedNode    | GPU memory utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateGpuMemoryUsedRequest | GPU memory utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateGpuUsedNode          | GPU utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateGpuUsedRequest       | GPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodGpuMemoryRequestBytes    | Number of requested GPU cards | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodGpuMemoryUsedBytes       | GPU memory usage | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodGpuRequest | Number of requested GPU cards | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodGpuUsed | GPU usage | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateCpuCoreUsedResource  | CPU utilization | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMemUsageResource     | Memory utilization (usage/pod specification) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMemNoCacheResource   | Memory utilization (usage/pod specification, excluding cache) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node<br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br>86400s |

## Statistical Granularity and Time Span
The supported time span varies by statistical granularity. When pulling monitoring data, you should keep in mind the time span restrictions as detailed below:

| Statistical Granularity | Maximum Time Span (End Time - Start Time) |
| -------- | ------------------------------------- |
| 60s      | 12 hours                                |
| 300s     | 3 days                                   |
| 3600s    | 30 days                                  |
| 86400s   | 186 days                                 |

## Dimensions and Parameters

<table>
    <thead>
        <tr>
            <th><span>Parameter Name</span></th>
            <th><span>Type</span></th>
            <th><span>Dimension Name</span></th>
            <th><span>Description</span></th>
            <th><span>Format</span></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td rowspan="2"><span>Required</span></td>
            <td><span>tke_cluster_instance_id</span></td>
            <td><span>Dimension name of the cluster</span></td>
            <td><span>Enter a string-type dimension name, such as `tke_cluster_instance_id`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>tke_cluster_instance_id</span></td>
            <td><span>Specific cluster ID</span></td>
            <td><span>Enter a specific cluster ID, such as `cls-fvkxp123`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
           <td rowspan="6">Required (one of which must be passed in)<span></span></td>
            <td><span>workload_name</span></td>
            <td><span>Dimension name of the workload name</span></td>
            <td><span>Enter a specific workload name, such as `workload_name`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>workload_name</span></td>
            <td><span>Specific workload name</span></td>
            <td><span>Enter a specific workload name, such as `coredns`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td><span>node</span></td>
            <td><span>Dimension name of the node name</span></td>
            <td><span>Enter a specific workload name, such as `node`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>node</span></td>
            <td><span>Specific node name</span></td>
            <td><span>Enter a specific node name, such as `node`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td><span>un_instance_id</span></td>
            <td><span>Dimension name of the node ID</span></td>
            <td><span>Enter a specific workload name, such as `un_instance_id`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>un_instance_id</span></td>
            <td><span>Specific node ID</span></td>
            <td><span>Enter a specific node ID, such as `ins-nwjhh123`</span></td>
        </tr>
           <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td rowspan="8">Optional (zero, one, or multiple of which can be passed in optionally)<span></span></td>
            <td><span>workload_kind</span></td>
            <td><span>Dimension name of the workload type</span></td>
            <td><span>Enter a specific workload name, such as `workload_kind`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>workload_kind</span></td>
            <td><span>Specific workload type</span></td>
            <td><span>Enter a specific workload name, such as `Deployment`</span></td>
        </tr>
          <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td><span>namespace</span></td>
            <td><span>Dimension name of the namespace</span></td>
            <td><span>Enter a string-type dimension name, such as `namespace`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>namespace</span></td>
            <td><span>Specific namespace</span></td>
            <td><span>Enter a specific namespace, such as `kube-system`</span></td>
        </tr>
          <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td><span>node_role</span></td>
            <td><span>Dimension name of the cluster</span></td>
            <td><span>Enter a string-type dimension name, such as `node_role`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>node_role</span></td>
            <td><span>Specific node role</span></td>
            <td><span>Enter a specific node role, such as `node`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Name</span></td>
            <td><span>pod_name</span></td>
            <td><span>Dimension name of the Pod name</span></td>
            <td><span>Enter a specific workload name, such as `pod_name`</span></td>
        </tr>
        <tr>
            <td><span>Conditions.N.Dimensions.N.Value</span></td>
            <td><span>pod_name</span></td>
            <td><span>Specific Pod name</span></td>
            <td><span>Enter a specific Pod name, such as `coredns-6ffc45f789-46lpq`</span></td>
        </tr>
    </tbody>
</table>



## Input Parameters

**In the namespace dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=namespace
&Conditions.N.Dimensions.1.Value=kube-system

**In the workload type dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_kind
&Conditions.N.Dimensions.1.Value=Deployment

**In the workload name dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns

**In the node role dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=node_role
&Conditions.N.Dimensions.1.Value=node

**In the node ID dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=un_instance_id
&Conditions.N.Dimensions.1.Value=ins-nwjhh123

**In the node name dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=node
&Conditions.N.Dimensions.1.Value=node

**In the Pod name dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=pod_name
&Conditions.N.Dimensions.1.Value=coredns-6ffc45f789-46lpq
