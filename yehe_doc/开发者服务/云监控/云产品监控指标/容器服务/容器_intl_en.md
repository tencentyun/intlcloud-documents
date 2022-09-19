## Notes

This document is only applicable to the [DescribeStatisticData](https://intl.cloud.tencent.com/document/product/248/39481) API. For all the following metrics, the `tke_cluster_instance_id` and `workload_name` dimensions are always required, and one of other required dimensions must be passed in.

## Namespace

Namespace = QCE/TKE2

## Monitoring Metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ------------------------------------ | ------------------------------------- | -------- | ------------------------------------------------------------ | --------------------------------------- |
| K8sContainerCpuCoreUsed              | Number of used CPU cores (average 2-minute number of CPU cores in the container) | - | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerFsWriteTimes             | Number of block device writes | - | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateCpuCoreUsedNode      | CPU utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateMemNoCacheNode       | Memory utilization (usage/node, excluding cache) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateMemUsageNode         | Memory utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerFsReadBytes              | Block device read bandwidth | MB/s | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerMemNoCacheBytes          | Memory usage (excluding cache) | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerNetworkReceivePackets    | Network inbound packets | Count/s | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerNetworkTransmitPackets   | Network outbound packets | Count/s | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateCpuCoreUsedRequest   | CPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateMemNoCacheRequest    | Memory utilization (usage/request, excluding cache) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateMemUsageRequest      | Memory utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerFsReadTimes              | Number of block device reads | - | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerMemUsageBytes            | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerNetworkTransmitBytes     | Network outbound traffic | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateCpuCoreUsedLimit     | CPU utilization (usage/limit) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateMemNoCacheLimit      | Memory utilization (usage/limit, excluding cache) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateMemUsageLimit        | Memory utilization (usage/limit) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerFsWriteBytes             | Block device write bandwidth | MB/s | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateGpuMemoryUsedNode    | GPU memory utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateGpuMemoryUsedRequest | GPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateGpuUsedNode          | GPU utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRateGpuUsedRequest       | GPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerGpuMemoryUsedBytes       | GPU memory usage | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerGpuUsed                  | Container GPU usage | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |

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
            <td rowspan="4"><span>Required</span></td>
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
            <td rowspan="16">Required (one of which must be passed in)</td>
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
<tr>
    <td><span>Conditions.N.Dimensions.N.Name</span></td>
    <td><span>container_name</span></td>
    <td><span>Dimension name of the container name</span></td>
    <td><span>Enter a string-type dimension name, such as `container_name`</span></td>
</tr>
<tr>
    <td><span>Conditions.N.Dimensions.N.Value</span></td>
    <td><span>container_name</span></td>
    <td><span>Specific container name</span></td>
    <td><span>Enter a specific container name, such as `coredns`</span></td>
</tr>
<tr>
    <td><span>Conditions.N.Dimensions.N.Name</span></td>
    <td><span>container_id</span></td>
    <td><span>Dimension name of the container ID</span></td>
    <td><span>Enter a string-type dimension name, such as `container_id`</span></td>
</tr>
<tr>
    <td><span>Conditions.N.Dimensions.N.Value</span></td>
    <td><span>container_id</span></td>
    <td><span>Specific container ID</span></td>
    <td><span>Enter a specific container ID, such as `containerd://a133bd 5ecaada12cd5d5d f01fe8b7e692c3780a11b3 ff0daf01ee6f35cbbdbdf`</span></td>
</tr>
<tr>
    <td><span>Conditions.N.Dimensions.N.Name</span></td>
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
</table>




## Input Parameters

**In the namespace dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns
&Conditions.N.Dimensions.2.Name=namespace
&Conditions.N.Dimensions.2.Value=kube-system

**In the node role dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns
&Conditions.N.Dimensions.2.Name=node_role
&Conditions.N.Dimensions.2.Value=node

**In the node name dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns
&Conditions.N.Dimensions.2.Name=node
&Conditions.N.Dimensions.2.Value=node

**In the node ID dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns
&Conditions.N.Dimensions.2.Name=un_instance_id
&Conditions.N.Dimensions.2.Value=ins-nwjhh123

**In the Pod name dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns
&Conditions.N.Dimensions.2.Name=pod_name
&Conditions.N.Dimensions.2.Value=coredns-6ffc45f789-46lpq

**In the container name dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns
&Conditions.N.Dimensions.2.Name=container_name
&Conditions.N.Dimensions.2.Value=coredns

**In the container ID dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns
&Conditions.N.Dimensions.2.Name=container_id
&Conditions.N.Dimensions.2.Value=containerd://a133bd5ecaada12cd5d5df01fe8b7e692c3780a11b3ff0daf01ee6f35cbbdbdf
