## Notes
This document is only applicable to the [DescribeStatisticData](https://intl.cloud.tencent.com/document/product/248/39481) API. For all the following metrics, the `tke_cluster_instance_id` dimension is required, while other dimensions are optional.

## Namespace
Namespace = QCE/TKE2
## Monitoring Metrics
>?The following four metrics are not supported for managed clusters: `K8sComponentApiserverReady`, `K8sComponentControllerManagerReady`, `K8sComponentEtcdReady`, and `K8sComponentSchedulerReady`.


| Parameter | Metric | Unit | Dimension | Statistical Period |
| --------------------------------------- | ------------------------------- | -------- | ------------------------------------------------------------ | --------------------------------------- |
| K8sComponent<br/>ApiserverReady | kube-apiserver health status | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sComponentController<br/>ManagerReady | kube-controller-manager health status | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sComponent<br/>EtcdReady | etcd health status | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sComponent<br/>SchedulerReady | kube-scheduler health status | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerNet<br/>workReceiveBytes | Network inbound traffic | MB/s | Required dimensions: tke_cluster_instance_id, workload_name<br/>Optional dimensions: node, un_instance_id. At least three dimensions should be input for this metric | 60s, <br/>300s, <br/>3600s, <br/>86400s |

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
            <td rowspan="4"><span>Required</span></td>
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
            <td><span>workload_name</span></td>
            <td><span>Dimension name of the workload name</span></td>
            <td><span>Enter a string-type dimension name, such as `workload_name`</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Value</span></td>
            <td><span>workload_name</span></td>
            <td><span>Specific workload name</span></td>
            <td><span>Enter a specific workload name, such as coredns</span></td>
        </tr>
        <tr>
            <td><span>Instances.N.Dimensions.N.Name</span></td>
            <td rowspan="4"><span>Optional (zero, one, or multiple of which can be passed in optionally)</span></td>
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
## Statistical Granularity and Time Span

The supported time span varies by statistical granularity. When pulling monitoring data, you should pay attention to the time span restrictions as detailed below:

| Statistical Granularity | Maximum Time Span (End Time - Start Time) |
| -------- | ------------------------------------- |
| 60s      | 12 hours                                |
| 300s     | 3 days                                   |
| 3600s    | 30 days                                  |
| 86400s   | 186 days                                 |


## Input Parameter Description
**In the cluster dimension, use the following input parameters:**
&Namespace=QCE/TKE2
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123

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
