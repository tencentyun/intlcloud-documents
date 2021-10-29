## Note
For all the following metrics, the `tke_cluster_instance_id` dimension is required, while other dimensions are optional.

## Namespace
Namespace=QCE/TKE
## Monitoring Metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ------------------------------------------ | ------------------------------------ | -------- | ------------------------------------------------------------ | ----------------------------------- |
| K8sWorkloadAbnormal | Workload exception | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadFsWriteTimes | Number of block device reads | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetwork<br>ReceiveBytesBw | Network inbound bandwidth | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name |  60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetwork<br>TransmitBytesBw | Network outbound bandwidth | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateCpu<br>CoreUsedCluster | CPU utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkload<br>CpuCoreUsed | Number of used CPU cores | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadMemNo<br>CacheBytes | Memory usage (excluding cache) | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetwork<br>ReceivePackets | Network inbound packets | Packets/sec | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetwork<br>TransmitPackets | Network outbound packets | Packets/sec | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateMem<br>NoCacheCluster | Memory utilization (excluding cache) | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
required| K8sWorkload<br>FsReadBytes | Block device read size | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkload<br>MemUsageBytes | Memory usage | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetwork<br>TransmitBytes | Network outbound traffic | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadPod<br/>RestartTotal | Number of pod restarts | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateMem<br/>UsageBytesCluster | Memory utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkload<br>FsReadTimes | Number of block device reads | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetwork<br>ReceiveBytes | Network inbound traffic | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkload<br>FsWriteBytes | Block device write size | B | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadGpu<br>MemoryUsedBytes | GPU memory usage | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadGpuUsed | Number of used GPU cards | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateGpu<br>MemoryUsedCluster | GPU memory utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRate<br>GpuUsedCluster | GPU utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadEks<br>GpuMemoryUsage | GPU memory utilization (elastic container) | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadEks<br>GpuMemoryUsedMib | GPU memory usage (elastic container) | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadEks<br>GpuUtilizationRates | GPU utilization (elastic container) | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateCpu<br>CoreUsedResource | CPU utilization (usage/pod specification) | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateMem<br>UsageBytesResource | Memory utilization (usage/pod specification) | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateMem<br>NoCacheBytesResource | Memory utilization (usage/pod specification, excluding cache) | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |

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
            <td rowspan="2"><span>Required</span></td>
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
             <td rowspan="6"><span>Optional (zero, one, or multiple of which can be passed in optionally)</span></td>
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
            <td><span>workload_kind</span></td>
            <td><span>Workload type dimension name</span></td>
            <td><span>Enter a String-type dimension name: workload_kind</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Value</span></td>
            <td><span>workload_kind</span></td>
            <td><span>Specific workload type</span></td>
            <td><span>Enter a specific workload type, such as Deployment</span></td>
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
    </tbody>
</table>



## Input Parameter Description
**In the cluster dimension (required), use the following input parameters:**
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123

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





