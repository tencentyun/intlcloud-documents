## Note
For all the following metrics, the `tke_cluster_instance_id` dimension is required, while other dimensions are optional.

## Namespace
Namespace=QCE/TKE
## Monitoring Metrics

| Parameter | Metric | Unit | Dimension | Statistical Period |
| --------------------------------------- | ------------------------------- | -------- | ------------------------------------------------------------ | -------------------------------------- |
| K8sComponent<br/>ApiserverReady | kube-apiserver health status | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sComponentController<br/>ManagerReady | kube-controller-manager health status | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sComponent<br/>EtcdReady | etcd health status | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sComponent<br/>SchedulerReady | kube-scheduler health status | - | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |
| K8sContainerNet<br/>workReceiveBytes | Network inbound traffic | MB/s | Required dimensions: tke_cluster_instance_id <br/>Optional dimensions: node, un_instance_id | 60s, <br/>300s, <br/>3600s, <br/>86400s |

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
            <td rowspan="4"><span>Optional (zero, one, or multiple of which can be passed in optionally)</span></td>
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
    </tbody>
</table>



## Input Parameter Description
****In the cluster dimension, use the following input parameters:****
&Namespace=QCE/TKE
&Instances.N.Dimensions.0.Name=tke_cluster_instance_id
&Instances.N.Dimensions.0.Value=cls-fvkxp123

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

