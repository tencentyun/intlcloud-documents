## Note
For all the following metrics, the `tke_cluster_instance_id` dimension is always required, one of other required dimensions must be passed in, and other dimensions are optional.

## Namespace
Namespace=QCE/TKE
## Monitoring Metrics
| Parameter | Metric | Unit | Dimension | Statistical Period |
| ----------------------------------- | ------------------------------------ | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| K8sPodCpu<br/>CoreUsed | CPU usage | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodMem<br/>NoCacheBytes | Memory usage (excluding cache) | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetwork<br/>ReceivePackets | Network inbound packets | Packets/sec | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateCpu<br/>CoreUsedLimit | CPU utilization (usage/limit) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMem<br/>NoCacheNode | Memory utilization (usage/node, excluding cache) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMem<br/>UsageRequest | Memory usage (excluding cache) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodFs<br/>ReadBytes | Block device read bandwidth | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodMem<br/>UsageBytes | Memory usage | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetwork<br/>TransmitBytes | Network outbound traffic | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRate<br/>CpuCoreUsedNode | CPU utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRate<br/>MemNoCacheRequest | Memory utilization (usage/request, excluding cache) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRestartTotal | Number of pod restarts | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodFsReadTimes | Number of block device reads | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetwork<br/>ReceiveBytes | Network inbound traffic | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetwork<br/>TransmitBytesBw | Network outbound bandwidth | MB/s | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateCpu<br/>CoreUsedRequest | CPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRate<br/>MemUsageLimit | Memory utilization (usage/limit) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodStatusReady | Pod_Ready status | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodFsWriteBytes | Block device write bandwidth | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetwork<br/>ReceiveBytesBw | inbound bandwidth | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodNetwork<br/>TransmitPackets | Network outbound packets | Packets/sec | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRate<br/>MemNoCacheLimit | Memory utilization (usage/limit, excluding cache) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRate<br/>MemUsageNode | Memory utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodFsWriteTimes | Number of block device writes | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateGpu<br/>MemoryUsedNode | GPU memory utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateGpu<br/>MemoryUsedRequest | CPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRate<br/>GpuUsedNode | GPU utilization (usage/node) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRate<br/>GpuUsedRequest | GPU utilization (usage/request) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodGpuMemory<br/>RequestBytes | Number of requested GPU cards | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodGpuMemory<br/>UsedBytes | GPU memory usage | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodGpuRequest | Number of requested GPU cards | - | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodGpuUsed | GPU usage | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodEksGpu<br/>MemoryUsage | GPU memory utilization (elastic container) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodEksGpu<br/>MemoryUsedMib | GPU memory usage (elastic container) | MB | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodEksGpu<br/>UtilizationRates | GPU utilization (elastic container) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): namespace, workload_kind, workload_name, node_role, node, un_instance_id, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateCpu<br/>CoreUsedResource | CPU utilization | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMem<br/>UsageResource | Memory utilization (usage/pod specification) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node <br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sPodRateMem<br/>NoCacheResource | Memory utilization (usage/pod specification, excluding cache) | % | Always required dimensions: tke_cluster_instance_id <br>Required dimensions (one of which must be passed in): workload_name, un_instance_id, node<br>Optional dimensions: node_role, workload_kind, namespace, pod_name | 60s, <br/>300s, <br/>3600s, 86400s |

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
            <td rowspan="2"><span>Always required</span></td>
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
           <td rowspan="6">Required (one of which must be passed in)<span></span></td>
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
            <td rowspan="8">Optional (zero, one, or multiple of which can be passed in optionally)<span></span></td>
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
          <tr>
            <td><span>Instances.N.Dimensions.N.Name</span></td>
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
    </tbody>
</table>


## Input Parameter Description
**In the namespace dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=namespace
&Instances.N.Dimensions.1.Value=kube-system

**In the workload type dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=workload_kind
&Instances.N.Dimensions.1.Value=Deployment

**In the workload name dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=workload_name
&Instances.N.Dimensions.1.Value=coredns

**In the node role dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=node_role
&Instances.N.Dimensions.1.Value=node

**In the node ID dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=un_instance_id
&Instances.N.Dimensions.1.Value=ins-nwjhh123

**In the node name dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=node
&Instances.N.Dimensions.1.Value=node

**In the pod name dimension, use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=pod_name
&Instances.N.Dimensions.1.Value=coredns-6ffc45f789-46lpq







