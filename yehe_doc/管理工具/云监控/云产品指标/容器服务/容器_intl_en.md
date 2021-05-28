## Note
For all the following metrics, the `tke_cluster_instance_id` and `workload_name` dimensions are always required, and one of other required dimensions must be passed in.

## Namespace
Namespace=QCE/TKE
## Monitoring Metrics
| Parameter | Metric | Unit | Dimension | Statistical Period |
| ----------------------------------------- | ------------------------------------- | -------- | ------------------------------------------------------------ | -------------------------------------- |
| K8sContainer<br/>CpuCoreUsed | Number of used CPU cores (average 2-minute number of CPU cores in the container) | - | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>FsWriteTimes | Number of block device writes | - | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>NetworkReceiveBytesBw | Network inbound bandwidth | MB/s | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerNetwork<br/>TransmitBytesBw | Network outbound bandwidth | MB/s | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRate<br/>CpuCoreUsedNode | CPU utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRate<br/>MemNoCacheNode | Memory utilization (usage/node, excluding cache) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerRate<br/>MemUsageNode | CPU utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>FsReadBytes | Block device read bandwidth | MB/s | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>MemNoCacheBytes | Memory usage (excluding cache) | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>NetworkReceivePackets | Network inbound packets | Packets/sec | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>NetworkTransmitPackets | Network outbound packets | Packets/sec | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateCpuCoreUsedRequest | Memory utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateMemNoCacheRequest | Memory utilization (usage/request, excluding cache) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateMemUsageRequest | Memory utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>FsReadTimes | Number of block device reads | - | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>MemUsageBytes | Memory usage | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>NetworkTransmitBytes | Network outbound traffic | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateCpuCoreUsedLimit | CPU utilization (usage/limit) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateMemNoCacheLimit | Memory utilization (usage/limit, excluding cache) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateMemUsageLimit | Memory utilization (usage/limit) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>FsWriteBytes | Block device write bandwidth | MB/s | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateGpuMemoryUsedNode | GPU memory utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateGpuMemoryUsedRequest | GPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateGpuUsedNode | GPU utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>RateGpuUsedRequest | GPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>GpuMemoryUsedBytes | GPU memory usage | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainer<br/>GpuUsed | Container GPU usage | MB | Always required dimensions: tke_cluster_instance_id, <br>workload_name <br/>Required dimensions (one of which must be passed in): namespace, node_role, node, un_instance_id, pod_name, container_name, container_id, workload_kind | 60s, <br/>300s, <br/>3600s, <br/>86400s |

## Overview of Parameters in Each Dimension
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
            <td><span>Instances.N.Dimensions.N.Name</span></td>
            <td rowspan="4"><span>Always required</span></td>
            <td><span>tke_cluster_instance_id</span></td>
            <td><span>Cluster dimension name</span></td>
            <td><span>Enter a String-type dimension name: tke_cluster_instance_id</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Value</span></td>
            <td><span>tke_cluster_instance_id</span></td>
            <td><span>Specific cluster ID</span></td>
            <td><span>Enter a specific cluster ID, such as cls-fvkxp123</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Name</span></td>
            <td><span>workload_name</span></td>
            <td><span>Workload name dimension name</span></td>
            <td><span>Enter a String-type dimension name: workload_name</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Value</span></td>
            <td><span>workload_name</span></td>
            <td><span>Specific workload name</span></td>
            <td><span>Enter a specific workload name, such as coredns</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Name</span></td>
            <td rowspan="16">Required (one of which must be passed in)</td>
            <td><span>namespace</span></td>
            <td><span>Namespace dimension name</span></td>
            <td><span>Enter a String-type dimension name: namespace</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Value</span></td>
            <td><span>namespace</span></td>
            <td><span>Specific namespace</span></td>
            <td><span>Enter a specific namespace, such as kube-system</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Name</span></td>
            <td><span>node_role</span></td>
            <td><span>Cluster dimension name</span></td>
            <td><span>Enter a String-type dimension name: node_role</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Value</span></td>
            <td><span>node_role</span></td>
            <td><span>Specific node role</span></td>
            <td><span>Enter a specific node role, such as node</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Name</span></td>
            <td><span>node</span></td>
            <td><span>Node name dimension name</span></td>
            <td><span>Enter a String-type dimension name: node</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Value</span></td>
              <td><span>node</span></td>
        <td><span>Specific node name</span></td>
        <td><span>Enter a specific node name, such as node</span></td>
    </tr>
    <tr>
        <td><span>Instances.N.Dimensions.N.Name</span></td>
            <td><span>un_instance_id</span></td>
    <td><span>Node ID dimension name</span></td>
    <td><span>Enter a String-type dimension name: un_instance_id</span></td>
</tr>
<tr>
    <td><span>Instances.N.Dimensions.N.Value</span></td>
    <td><span>un_instance_id</span></td>
    <td><span>Specific node ID</span></td>
    <td><span>Enter a specific node ID, such as ins-nwjhh123</span></td>
</tr>
<tr>
    <td><span>Instances.N.Dimensions.N.Name</span></td>
    <td><span>pod_name</span></td>
    <td><span>Pod name dimension name</span></td>
    <td><span>Enter a String-type dimension name: pod_name</span></td>
</tr>
<tr>
    <td><span>Instances.N.Dimensions.N.Value</span></td>
    <td><span>pod_name</span></td>
    <td><span>Specific pod name</span></td>
    <td><span>Enter a specific pod name, such as coredns-6ffc45f789-46lpq</span></td>
</tr>
<tr>
    <td><span>Instances.N.Dimensions.N.Name</span></td>
    <td><span>container_name</span></td>
    <td><span>Container name dimension name</span></td>
    <td><span>Enter a String-type dimension name: container_name</span></td>
</tr>
<tr>
    <td><span>Instances.N.Dimensions.N.Value</span></td>
    <td><span>container_name</span></td>
    <td><span>Specific container name</span></td>
    <td><span>Enter a specific container name, such as coredns</span></td>
</tr>
<tr>
    <td><span>Instances.N.Dimensions.N.Name</span></td>
    <td><span>container_id</span></td>
    <td><span>Container ID dimension name</span></td>
    <td><span>Enter a String-type dimension name: container_id</span></td>
</tr>
<tr>
    <td><span>Instances.N.Dimensions.N.Value</span></td>
    <td><span>container_id</span></td>
    <td><span>Specific container ID</span></td>
    <td><span>Enter a specific container ID, such as containerd://a133bd 5ecaada12cd5d5d f01fe8b7e692c3780a11b3 ff0daf01ee6f35cbbdbdf</span></td>
</tr>
<tr>
    <td><span>Instances.N.Dimensions.N.Name</span></td>
     <td><span>workload_kind</span></td>
<td><span>Workload type dimension name</span></td>
<td><span>Enter a String-type dimension name: workload_kind</span></td>
    </tr>
<tr>
    <td><span>Instances.N.Dimensions.N.Value</span></td>
        <td><span>workload_kind</span></td>
    <td><span>Specific workload type</span></td>
    <td><span>Enter a specific workload name, such as Deployment</span></td>
</tr>
</table>

​      



## Input Parameter Description
**In the namespace dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=workload_name
&Instances.N.Dimensions.1.Value=coredns
&Instances.N.Dimensions.2.Name=namespace
&Instances.N.Dimensions.2.Value=kube-system

**In the node role dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=workload_name
&Instances.N.Dimensions.1.Value=coredns
&Instances.N.Dimensions.2.Name=node_role
&Instances.N.Dimensions.2.Value=node

**In the node name dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=workload_name
&Instances.N.Dimensions.1.Value=coredns
&Instances.N.Dimensions.2.Name=node
&Instances.N.Dimensions.2.Value=node

**In the node ID dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=workload_name
&Instances.N.Dimensions.1.Value=coredns
&Instances.N.Dimensions.2.Name=un_instance_id
&Instances.N.Dimensions.2.Value=ins-nwjhh123

**In the pod name dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=workload_name
&Instances.N.Dimensions.1.Value=coredns
&Instances.N.Dimensions.2.Name=pod_name
&Instances.N.Dimensions.2.Value=coredns-6ffc45f789-46lpq

**In the container name dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=workload_name
&Instances.N.Dimensions.1.Value=coredns
&Instances.N.Dimensions.2.Name=container_name
&Instances.N.Dimensions.2.Value=coredns

**In the container ID dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=workload_name
&Instances.N.Dimensions.1.Value=coredns
&Instances.N.Dimensions.2.Name=container_id
&Instances.N.Dimensions.2.Value=containerd://a133bd5ecaada12cd5d5df01fe8b7e692c3780a11b3ff0daf01ee6f35cbbdbdf





