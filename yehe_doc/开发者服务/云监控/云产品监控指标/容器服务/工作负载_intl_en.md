## Notes

This document is only applicable to the [DescribeStatisticData](https://intl.cloud.tencent.com/document/product/248/39481) API. For all the following metrics, the `tke_cluster_instance_id` dimension is required, while other dimensions are optional.

## Namespace

Namespace = QCE/TKE2

## Monitoring Metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| -------------------------------------- | ------------------------------------ | -------- | ------------------------------------------------------------ | ------------------------------------ |
| K8sWorkloadAbnormal | Workload exception | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadFsWriteTimes | Number of block device writes | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetworkReceiveBytesBw       | Network inbound bandwidth | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name |  60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetworkTransmitBytesBw      | Network outbound bandwidth | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateCpuCoreUsedCluster      | CPU utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadCpuCoreUsed                 | Number of used CPU cores | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadMemNoCacheBytes             | Memory usage (excluding cache) | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetworkReceivePackets       | Network inbound packets | Count/s | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetworkTransmitPackets      | Network outbound packets | Count/s | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateMemNoCacheCluster       | Memory utilization (excluding cache) | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadFsReadBytes                 | Block device read size | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadMemUsageBytes               | Memory usage | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetworkTransmitBytes        | Network outbound traffic | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadPodRestartTotal             | Number of Pod restarts | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateMemUsageBytesCluster    | Memory utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadFsReadTimes             | Number of block device reads | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadNetworkReceiveBytes         | Network inbound traffic | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadFsWriteBytes                | Block device write size | B | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadGpuMemoryUsedBytes          | GPU memory usage | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadGpuUsed | Number of used GPU cards | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateGpuMemoryUsedCluster    | GPU memory utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateGpuUsedCluster          | GPU utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateCpuCoreUsedResource     | CPU utilization (usage/pod specification) | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateMemUsageBytesResource   | Memory utilization (usage/pod specification) | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sWorkloadRateMemNoCacheBytesResource | Memory utilization (usage/pod specification, excluding cache) | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: namespace, workload_kind, workload_name | 60s, <br>300s, <br>3600s, <br>86400s |

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
             <td rowspan="6"><span>Optional (zero, one, or multiple of which can be passed in optionally)</span></td>
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
    </tbody>
</table>




## Input Parameters

**In the cluster dimension (required), use the following input parameters:**
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123

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
&Namespace=QCE/TKE2
&Conditions.N.Dimensions.0.Name=tke_cluster_instance_id
&Conditions.N.Dimensions.0.Value=cls-fvkxp123
&Conditions.N.Dimensions.1.Name=workload_name
&Conditions.N.Dimensions.1.Value=coredns
