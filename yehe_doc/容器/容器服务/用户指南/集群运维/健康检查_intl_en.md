## Overview
The cluster health check feature is a service provided by Tencent Kubernetes Engine (TKE) for checking the status and health of each resource in a cluster. The resulting check report displays the detailed status and configuration of components, nodes, workloads, and other check items. If an exception is detected, this feature can describe the exception in detail, automatically analyze the severity, cause, and impact, and propose rectification suggestions.
>! During the health check, namespace **tke-cluster-inspection** will be automatically created in your cluster, and a Daemonset will be installed to collect node information. Both objects will be automatically deleted after the health check is completed.

## Main Check Items
<table>
<thead>
<tr>
<th width="10%">Check Category</th>
<th width="30%">Check Item</th>
<th width="45%">Check Content</th>
<th width="15%">Self-Deployed Clusters Only</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan=10>Resource status</td>
<td>kube-apiserver status</td>
<td rowspan=7>Check whether the component is running. If the component runs as a pod, the health check feature checks whether it has restarted over the past 24 hours</td>
<td>Yes</td>
</tr>
<tr>
<td>kube-scheduler status</td>
<td>Yes</td>
</tr>
<tr>
<td>kube-controller-manager status</td>
<td>Yes</td>
</tr>
<tr>
<td>etcd status</td>
<td>Yes</td>
</tr>
<tr>
<td>kubelet status</td>
<td>No</td>
</tr>
<tr>
<td>kube-proxy status</td>
<td>No</td>
</tr>
<tr>
<td>dockerd status</td>
<td>No</td>
</tr>
<tr>
<td>Master node status</td>
<td>Check whether the node status is Ready and free of any other exceptions, such as insufficient memory and insufficient disk space</td>
<td>Yes</td>
</tr>
<tr>
<td>Worker node status</td>
<td>Check whether the node status is Ready and free of any other exceptions, such as insufficient memory and insufficient disk space</td>
<td>No</td>
</tr>
<tr>
<td>Status of each workload</td>
<td>Check whether the number of currently available pods of the workload meets the expected number of pods</td>
<td>No</td>
</tr>
<tr>
<td rowspan=14>Running status</td>
<td>Parameter configuration of kube-apiserver</td>
<td>Check the following parameters based on the master node configuration:<ul><li>max-requests-inflight: maximum number of non-change requests running in a given period</li><li>max-mutating-requests-inflight: maximum number of change requests running in a given period</li></ul></td>
<td>Yes</td>
</tr>
<tr>
<td>Parameter configuration of kube-scheduler</td>
<td>Check the following parameters based on the master node configuration:<ul><li>kube-api-qps: QPS of kube-apiserver resquests</li><li>kube-api-burst: maximum burst value during communication with kube-apiserver</li></ul></td>
<td>Yes</td>
</tr>
<tr>
<td>Parameter configuration of kube-controller-manager</td>
<td>Check the following parameters based on the master node configuration:<ul><li>kube-api-qps: QPS of kube-apiserver requests</li>
<li>kube-api-burst: maximum burst value during communication with kube-apiserver</li></ul></td>
<td>Yes</td>
</tr>
<tr>
<td>Parameter configuration of etcd</td>
<td>Check the following parameter based on the master node configuration:<br>quota-backend-bytes: storage capacity</td>
<td>Yes</td>
</tr>
<tr>
<td>Reasonability of the master node configuration</td>
<td>Check whether the current master node configuration is sufficient to the current cluster scale</td>
<td>Yes</td>
</tr>
<tr>
<td>High availability of nodes</td>
<td>Check whether the current cluster is a single-node cluster.
Check whether current cluster nodes support multi-AZ disaster recovery<br>
That is, the health check feature checks whether the total number of resources in other availability zones is sufficient to the current cluster business scale in the event that one availability zone becomes unavailable</td>
<td>No</td>
</tr>
<tr>
<td>Request and Limit configuration of workloads</td>
<td>Check whether workloads have configured resource-limiting containers. Configuring resource limits helps improve resource planning, pod scheduling, cluster availability, and other functions</td>
<td>No</td>
</tr>
<tr>
<td>Anti-affinity configuration of workloads</td>
<td>Check whether workloads have configured affinity or anti-affinity. Configuring anti-affinity helps improve the high availability of business</td>
<td>No</td>
</tr>
<tr>
<td>PDB configuration of workloads</td>
<td>Check whether workloads have configured PDB, which can help prevent your business from becoming unavailable due to eviction.</td>
<td>No</td>
</tr>
<tr>
<td>Health check configuration of workloads</td>
<td>Check whether a health check is configured for workloads. Health check helps detect business exceptions</td>
<td>No</td>
</tr>
<tr>
<td>HPA-IP configuration</td>
<td>Check whether the current number of remaining pod IP addresses in the cluster meets the maximum number for HPA scale-out</td>
<td>No</td>
</tr>
</tr>
</tr>
</tbody></table>

## Directions
1. Log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and choose **Cluster OPS** > **Health Check** in the left sidebar.
2. On the **Health Check** page that appears, select the health check mode for the cluster.   
    In the Health Check page, there’re three options: Batch Check, Check Now, and Auto Check.
 - **Batch Check**: simultaneously checks multiple clusters.
 - **Check Now**: checks only one cluster.
 - **Auto Check**: enables periodic health check for the cluster. 
![](https://main.qcloudimg.com/raw/4fc59b17066d8883e4476b5265b77a40.png)
In the **Auto-Checking Settings** window that appears, you can enable/disable auto-check, and set the check period and time based on your needs.
![](https://main.qcloudimg.com/raw/6d61b2b43e8791bc49fa78ec99bd1780.png)
3. When the health check starts, you can view the check progress.
![](https://main.qcloudimg.com/raw/0b167cfe1cfb15aa274208d3dc4e50cb.png)
4. After the check is completed, you can click **View Check Result** to view the check report.
![](https://main.qcloudimg.com/raw/e0cff922a5f8510795436a187cb3d8ac.png)
On the check report page, click **Resource Status** and **Running Status** tab to view resource statuses and exceptions respectively. Click **Check Contents** to view the detailed check contents. Click **Exceptions** to view the exception severity, descriptions, causes, impacts, and rectification suggestions.
![](https://main.qcloudimg.com/raw/bcbcf5a137377a5336e83cac311b55ce.png)

