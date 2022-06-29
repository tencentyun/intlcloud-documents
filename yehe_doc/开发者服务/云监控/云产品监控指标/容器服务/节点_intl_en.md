## Notes
This document is only applicable to the [DescribeStatisticData](https://intl.cloud.tencent.com/document/product/248/39481) API. For all the following metrics, the `tke_cluster_instance_id` dimension is required, while other dimensions are optional.

## Namespace
Namespace = QCE/TKE2

## Monitoring Metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| ----------------------------------- | ----------------- | -------- | ------------------------------------------------------------ | -------------------------------------- |
| K8sNodeCpuUsage | CPU utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sNodeStatusReady | Node status | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sNodeLanIntraffic | Private inbound bandwidth | MB/s | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sNodeTcpCurrEstab | Number of TCP connections | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sNodeLanOuttraffic | Private outbound bandwidth | MB/s | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sNodeWanIntraffic | Public inbound bandwidth | MB/s | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sNodeMemUsage | Memory utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sNodePod<br>RestartTotal | Number of pod restarts on the node | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sNodeCpu<br>CoreRequestTotal | Number of allocated CPU cores | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br>300s, <br>3600s, <br>86400s |
| K8sNodeGpu<br/>MemoryUsedBytes | GPU memory usage | B | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sNodeGpuUsed | GPU utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sNodeRateGpu<br/>MemoryUsed | GPU memory utilization |% | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sNodeWan<br/><br/>Outtraffic | Public outbound bandwidth | MB/s | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sNodeRate<br/>GpuUsed | GPU utilization | % | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sNodeMemory<br/>RequestBytesTotal | Memory allocation | MB | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node_role, node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |

## Statistical Granularity and Time Span

The supported time span varies by statistical granularity. When pulling monitoring data, you should pay attention to the time span restrictions as detailed below:

| Statistical Granularity | Maximum Time Span (End Time - Start Time) |
| -------- | ------------------------------------- |
| 60s      | 12 hours                                |
| 300s     | 3 days                                   |
| 3600s    | 30 days                                  |
| 86400s   | 186 days                                 |

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
            <td><span>Dimension name of the cluster</span></td>
            <td><span>Enter a string-type dimension name, such as `tke_cluster_instance_id`</span></td>
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
            <td><span>node_role</span></td>
            <td><span>Dimension name of the cluster</span></td>
            <td><span>Enter a string-type dimension name, such as `node_role`</span></td>
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
            <td><span>Dimension name of the node name</span></td>
            <td><span>Enter a string-type dimension name, such as `node`</span></td>
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
            <td><span>Dimension name of the node ID</span></td>
            <td><span>Enter a string-type dimension name, such as `un_instance_id`</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Value</span></td>
            <td><span>un_instance_id</span></td>
            <td><span>Specific node ID</span></td>
            <td><span>Enter a specific node ID, such as ins-nwjhh123</span></td>
        </tr>
    </tbody>
</table>


## Input Parameter Description
**In the cluster dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123

**In the node role dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=node_role
&Instances.N.Dimensions.1.Value=node

**In the node ID dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=un_instance_id
&Instances.N.Dimensions.1.Value=ins-nwjhh123

**In the node name dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123
&Instances.N.Dimensions.1.Name=node
&Instances.N.Dimensions.1.Value=node




