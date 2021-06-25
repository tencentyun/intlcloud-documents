## May 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The features of cloud native monitoring were enhanced.</td>
		<td>
		<li>The data collection configuration is optimized.</li>
		<li>The status information of the collection target is added.</li>
		<li>The interaction process is optimized.</li>
		<li>The detection of the collection target is supported.</li></td>
		<td>2021-05-28</td>
		<td>Log Collection</td>
</tr>
<tr>
    <td>The OLM add-on was launched.</td>
		<td>
	The OLM add-on helps users install, update, and manage the lifecycle of Operators.
	  </td>
		<td>2021-05-28</td>
		<td><a href="https://cloud.tencent.com/document/product/457/56752">OLM</a>
</tr>
<tr>
    <td>The HPC add-on was launched.</td>
		<td>
	HPC is an add-on to periodically modify the number of replicas of K8s workload. Used in conjunction with HPC CRD resources, it can support scheduled actions in seconds.
	  </td>
		<td>2021-05-28</td>
		<td><a href="https://cloud.tencent.com/document/product/457/56753">HPC</a>
</tr>
<tr>
    <td>The feature of TKE console was enhanced.</td>
		<td>
<li>Users can select the operating system for when creating node.</li>
<li>Users can modify the desired number of nodes during the node pool scaling out.</li>
<li>Users can search for workload by tag.</li>
	  </td>
		<td>2021-05-20</td>
		<td>
<a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding a Node</a></td>
		</td>
</tr>
</table>

## April 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The feature of TKE console was enhanced.</td>
		<td>
		<li>StatefulSet and DaemonSet can be redeployed with one-click.</li>
		<li>Secret supports TLS certificate. You can import it from file or paste multiple key-value pairs to enter in a batch.</li>
		<li>The container health check support the use of port name.</li>
		<li>Namespace supports the selection of “All namespaces” and can be searched by keyword.</li></td>
		<td>2021-04-30</td>
		<td><li><a href="https://intl.cloud.tencent.com/document/product/457/30663">StatefulSet Management</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30664"> DaemonSet Management</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30676">Secret Management</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30669">Setting the Health Check for a Workload</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30660"> Namespaces</a></li></td>
</tr>
<tr>
    <td>The log collection capability is enhanced.</td>
		<td><li>It supports the extraction mode of multiple lines - full regex, which is suitable for searching for log by key-value pair in multi-line logs such as java program.</li>
		<li>It supports automatic generation of regular expressions based on user’s log samples, and automatic extraction of corresponding key-value pairs.</li></td>
		<td>2021-04-15</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32419">Log Collection</a></td>
</tr>
</table>


## March 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The beta ARM cluster starts.</td><td>The beta of ARM cluster starts. To join the beta, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td><td>2021-03-31</td><td>-</td>
</tr>
<tr>
    <td>The feature of TKE console was enhanced.</td><td>
		<li>Kubernetes objects support batch input by pasting multiple key-value pairs.</li>
		<li>When configMap is used as an environment variable, all keys can be selected with one-click.</li>
		<li>Secret can be modified through console.</li>
		<li>ConfigMap can be managed through console. You can manually add or upload file to add key-value pairs.</li>
		<li>subPathExpr can be configured through console.</li>
		<li>CronJob supports displaying the generated active Jobs. User can customize the “Completed Jobs Retained” and “Failed Jobs Retained”, pause the generation of a scheduled Job, resume the paused Job, and manually generate a new Job.</li>
		</td>
		<td>2021-03-31</td>
		<td>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30658">Kubernetes Object Management</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30676">Secret Management</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30675">ConfigMap Management</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30678">Instructions for Other Storage Volumes</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30666">CronJob Management</a></li>
		</td>
</tr>
<tr>
    <td>The node search feature was enhanced.</td><td>The nodes can be searched in batch by label or IP address.</td><td>2021-03-19</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30650">Node Overview</a></td>
</tr>
<tr>
    <td>The nodes of the scaling group can be removed from the node pool.</td><td>The nodes of the scaling group can be removed from the node pool. The monthly-subscribed nodes can only be removed, but cannot be terminated.</td><td>2021-03-15</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35900">Node Pool Overview</a></td>
</tr>
<tr>
    <td>Monthly-subscribed node pools support auto scale-out.</td><td>Monthly-subscribed node pools only support auto scale-out. The Auto Scale-in is not supported currently.</td><td>2021-03-02</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35901">Creating a Node Pool</a></td>
</tr>
</table>




## February 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The operations for nodes were enhanced.</td><td>The node in the node pool can be cordoned and drained, and the node management ability of the node pool is improved.</td><td>2021-02-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35900">Node Pool Overview</a></td>
</tr>
<tr>
    <td>Users can mount data disk partition when adding the existing node.</td><td>When adding existing node to a cluster or node pool, users can select partition or logical volume name for the data disk mounting, which provides more flexible mount Settings.</td><td>2021-02-20</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding an existing node</a></td>
</tr>
</table>

## January 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Master version upgrade supports minor version.</td><td>This feature provides a more flexible version upgrade mechanism.</td><td>2021-01-14</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading the Master Kubernetes Version</a></td>
</tr>
</table>

## December 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Descheduler addon was launched.</td><td>Based on the actual node loads, this addon supports automatic rescheduling of marked services on high-load nodes to maintain the cluster load balance.</td><td>2020-12-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39146">DeScheduler</a></td>
</tr>
<tr>
    <td>Nginx-ingress addon was fully launched.</td><td><ul class="params"><li>The issue of nginx-ingress-controller toleration scheduling was fixed.</li><li>Nginx-Ingress UI experience was improved, including the regular matching of forwarding rule, configuration of backend ClusterIP mode Service, and certificate supporting kubernetes.io/tls type Sercret.</li></ul></td><td>2020-12-24</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39143">Nginx-ingress</a></td>
</tr>
<tr>
    <td>CBS-CSI addon was launched.</td><td>CBS-CSI addon supports: <ul class="params"><li>Creating static volume/dynamic volume</li><li>Storage topology awareness</li><li>Scheduler awareness of node maxAttachLimit</li><li>Online volume expansion</li><li>Volume snapshot and restoration</li></ul></td><td>2020-12-22</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39136">CBS-CSI</a></td>
</tr>
<tr>
    <td>TKE node pool was fully launched.</td><td>Basic node pool features allow you to conveniently and quickly create, manage, and terminate nodes and dynamically scale nodes in or out.</td><td>2020-12-21</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35900">Node Pool Overview</a></td>
</tr>
<tr>
    <td>The feature of TKE console was enhanced.</td><td><ul class="params"><li>The console supports Resource Quota, which can be used to configure the resource quotas and default resource request values for the namespace.</li><li>The ConfigMap can be generated based on the imported file.</li></td><td>2020-12-09</td><td>-</td>
<tr>
   <td>NetworkPolicy addon was launched.</td><td>This addon supports automatic synchronization of NetworkPolicy to make the network isolation policy effective.</td><td>2020-12-03</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39120">Network Policy</a></td>
</tr>
</table>

## November 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The beta of new TKE network solution was launched.</td><td>Leveraging intelligent ENI, TKE launches a new container network solution. In this solution, each pod is assigned a dedicated ENI. Pod-to-pod communications can be implemented without traveling through the node protocol stack (default namespace), so as to shorten the container access link and the access latency.</td><td>2020-11-27</td><td>-</td>
</tr>
<tr>
    <td>The beta of Nginx-Ingress feature was launched.</td><td>TKE is fully compatible with the native Nginx-ingress, and provides more advanced features to help users quickly deploy and build production-level traffic access gateways. It provides comprehensive Nginx-ingress full lifecycle management, automatic cloud native monitoring, CLS, and OPS capabilities.</td><td>2020-11-26</td><td>-</td>
</tr>
<tr>
    <td>Event dashboard was launched.</td><td>This feature implements the aggregation search and trend observation of top events and exception events.</td><td>2020-11-26</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38892">Event Dashboard</a></td>
</tr>
<tr>
    <td>Auditing dashboard was launched.</td><td>This feature implements the aggregation search and direct observation of cluster global, nodes, K8s objects and other important operations.</td><td>2020-11-26</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38890">Auditing Dashboard</a></td>
</tr>
<tr>
    <td>The node pool and cluster operating system can be changed.</td><td>Users can create node pools of different operating systems as needed to facilitate the standardized management of nodes.</td><td>2020-11-23</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35901">Creating a Node Pool</a></td>
</tr>
<tr>
    <td>DynamicScheduler addon is added.</td><td>This addon performs scheduling based on actual node loads, so as to prevent traffic hotspots.</td><td>2020-11-21</td><td>-</td>
</tr>
</table>


## October 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TPS supports monitoring of edge clusters.</td><td>TPS supports monitoring of edge clusters, and provides the capability of cross-VPCs multi-cluster management.</td><td>2020-10-30</td><td>PROM Instance Management</td>
</tr>
<tr>
    <td>TPS supports WebHook in alarm policies.</td><td>TPS supports configuring WebHook, which can better help users find and solve service exceptions in time and is more conducive to the stable operation of services.</td><td>2020-10-30</td><td>Alarm Configurations</td>
</tr>
<tr>
    <td>TKE node pool adds the ability to view scaling records.</td><td>This feature can help users view the changes in the number of nodes in the node pool and the causes and results for scaling activities.</td><td>2020-10-13</td><td>Viewing Node Pool Scaling Logs</td>
</tr>
</table>


## September 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TKE ServiceConfig was optimized</td><td>You can configure service/ingress to create tkeserviceconfig automatically.</td><td>2020-09-23</td><td><a href="https://intl.cloud.tencent.com/document/product/457/37015">Using TKEServiceConfig to Configure CLBs</a></td>
</tr>
<tr>
    <td>The DNSAutoscaler add-on was launched.</td><td>This add-on can obtain number of nodes and cores of the cluster via Deployment, and auto-scaling the number of DNS replicas according to the preset scaling policy, so as to improve DNS availability.</td><td>2020-09-23</td></td><td><a href="https://intl.cloud.tencent.com/document/product/457/39122">DNSAutoscaler</a></td>
</tr>
<tr>
    <td>The beta cloud native ETCD was launched.</td><td>This feature enables you to one-click deploy the high-reliability and high-performance ETCD cluster, which is profusely verified through Tencent’s internal services. It also provides cross-AZ disaster recovery capabilities and optimal performance configuration.</td><td>2020-09-16</td><td>-</td>
</tr>
<tr>
    <td>One-click addon configuration was available when creating the cluster.</td><td>You can easily and quickly configure the required addons for the cluster.</td><td>2020-09-15</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
</table>

## August 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> 
</tr>
<tr>
    <td>The monitoring capability of the cloud native monitoring service was optimized.</td><td><ul class="params"><li>The cluster monitoring collection items are preset, and a diverse Grafana dashboard is available.</li><li>The Targets list page is added to allow users to view the real-time status of monitoring tasks.</li></ul></td><td>2020-08-31</td><td>-</td>
</tr>
<tr>
    <td>The alarm module of the cloud native monitoring service was upgraded.</td><ul class="params"><li>It can be associated with a local Alertmanager component.</li><li>Supports CRD management of Prometheus rules.</li></ul></td><td>2020-08-31</td><td>Alarm Configurations</td>
</tr>
<tr>
    <td>The NodeProblemDetectorPlus add-on was launched.</td><td>It supports configuring node self-healing policy on the basis of existing detection feature.</td><td>2020-08-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38784">Node-Problem-Detector-Plus Description</a></td>
</tr>
<tr>
    <td>TKE launched in-place major-version upgrade capabilities.</td><td>The in-place major-version upgrade feature supports major-version upgrade without node reinstallation.</td><td>2020-08-25</td><td>-</td>
</tr>
<tr>
    <td>TKE add-ons were fully launched.</td><td>The add-on feature enables users to install or uninstall multiple advanced add-ons for clusters.</td><td>2020-08-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/33988">Add-on Overview</a></td>
</tr>
<tr>
    <td>TKE Kubernetes 1.18 version was fully launched.</td><td>Allows users to create clusters of the Kubernetes 1.18 version and upgrade clusters to the 1.18 version.</td><td>2020-08-24</td><td>-</td>
</tr>
</table>


## July 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The capabilities of storage plug-ins are optimized.</td><td><ul class="params"><li>The TKE console supports PV creation without specifying StorageClass.</li><li>Users can set and mount COS subdirectories.</li></ul></td><td>2020-07-28</td><td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/37770">PV and PVC binding rules</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/36160">Using COS</a></li></ul></td>
</tr>
<tr>
    <td>Cluster creation supports setting node configuration placement groups.</td><td>This feature enables disaster recovery and high availability for nodes when they are launched.</td><td>2020-07-15</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
<tr>
    <td>Cloud native monitoring is launched for beta testing.</td><td>It supports one-click deployment of the high-availability monitoring architecture and quick association with TKE clusters and EKS clusters.</td><td>2020-07-15</td><td>Cloud Native Monitoring</td>
</tr>
<tr>
    <td>The collection configuration and alarm configuration of cloud native monitoring are implemented through products.</td><td><ul class="params"><li>Three configuration modes are supported: service monitor, pod monitor, and raw job.</li><li>Alarm history rewinding is supported.</li></ul></td><td>2020-07-15</td><td>-</td>
</tr>
<tr>
    <td>RBAC-based permission control with finer granularity is launched for beta testing.</td><td><ul class="params"><li>It allows cluster admins to configure management permissions for different roles regarding different resources in the cluster.</li><li>It supports certificate revocation.</li><li>It is suitable for enterprises’ compliance permission management scenarios.</li></ul></td><td>2020-07-10</td><td><a href="https://intl.cloud.tencent.com/document/product/457/37366">TKE Kubernetes Object-level Permission Control</a></td>
</tr>
</table>

## June 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The IPVS-bpf mode is launched for beta testing.</td><td>TKE uses eBPF to bypass conntrack and optimize the Kubernetes Service, improving the non-persistent connection performance by over 40% and reducing the p99 latency by over 31%.</td><td>2020-06-19</td><td>-</td>
</tr>
<tr>
    <td>TKE supports the creation of services in CLB-to-Pod direct access mode.</td><td>The forwarding performance of pods with LoadBalancer directly connected to ENI can be improved by over 10%.</td><td>2020-06-18</td><td><a href="https://intl.cloud.tencent.com/document/product/457/36837">Using services with LoadBalancer directly connected to pods</a></td>
</tr>
<tr>
    <td>TKE supports balanced forwarding and local binding.</td><td>TKE has strengthened the Loadbalancer Service and the LoadBalancer Ingress backend binding with the RS feature. TKE supports balanced forwarding and local binding.</td><td>2020-06-18</td><td><a href="https://intl.cloud.tencent.com/document/product/457/36836">Service backend selection</a></td>
</tr>
<tr>
    <td>The TKE app market was comprehensively upgraded.</td><td>The app market provides an output window for Tencent Cloud’s practical cloud-native technologies and also provides a variety of great community apps that users can easily and quickly use.</td> <td>2020-06-10</td><td><a href="https://intl.cloud.tencent.com/document/product/457/37706">Application Market</a></td>
</tr>
</table>

## May 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TKE launches the ContainerNative network LoadBalancer (supports CLB-to-Pod direct access).</td><td>In TKE, you can use services and ingresses with LoadBalancer directly connected to pods, which provides higher performance and more robust product capabilities. This feature can resolve issues such as imbalanced load for persistent connections, health check session persistence configuration issues, and IPVS jitter.</td><td>2020-05-12</td><td>-</td>
</tr>
<tr>
    <td>The cluster deletion feature is optimized.</td><td><ul class="params"><li>When deleting a cluster, you can view the existing nodes, security groups, cloud disks, and other resources in the cluster.</li><li>A deletion risk reminder is added to prevent accidental deletion that may interrupt your business.</li><li>You can delete the nodes, cloud disks, and other resources in the cluster at the same time.</li></ul></td><td>2020-05-12</td><td><a href="https://intl.cloud.tencent.com/document/product/457/36280">Deleting Clusters</a></td>
</tr>
<tr>
    <td>TKE launches the open-source KMS plug-in.</td><td><ul class="params"><li><a href="https://github.com/Tencent/tke-kms-plugin">The Tencent Cloud TKE-KMS plug-in</a> integrates the rich key management features of the Key Management Service (KMS) to provide robust encryption/decryption capabilities for secrets in Kubernetes clusters.</li><li>By using the TKE-KMS plug-in, you can perform KMS encryption on your business credential information stored in clusters to enhance your security.</li></ul></td><td>2020-05-08</td><td>-</td>
</tr>    
</table>



## April 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The TKE console supports multidimensional node filtering and node list export.</td><td><ul class="params"><li>Cluster nodes can be filtered based on lock status.</li><li>Cluster nodes can be filtered based on CVM attributes such as node status and IP address.</li><li>Cluster nodes can be exported in batches.</li></ul></td><td>2020-04-22</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30650">Node Overview</a></td>
</tr>
<tr>
	<td>TKE Image Registry can configure a global image lifecycle management policy.</td><td>TKE Image Registry adds the image lifecycle management feature, which allows users to configure a global image version clearing policy for the main account and supports independent version clearing policies retained for individual repositories.</td><td>2020-04-16</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/38867">Image Lifecycle Management</a></td>
</tr>
<tr>
    <td>The TKE beta version supports the node pool feature.</td><td>The node pool feature can be used in the following scenarios:
		<ul class="params">
		<li>When a cluster contains multiple heterogeneous nodes (different models), node pools can standardize node group management.</li><li>If a cluster needs to scale nodes in or out frequently, node pools can reduce the operation costs.</li><li>If application scheduling rules in a cluster are complex, node pool tags can quickly specify business scheduling rules.</li><li>During routine cluster node maintenance, node pools can conveniently manage Kubernetes and Docker version upgrades.</li></ul></td><td>2020-04-10</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35899">Node Pool Management</a></td>
</tr>
<tr>
	<td>TKE removes Kubernetes 1.8 as an option.</td><td>TKE no longer supports creating clusters using Kubernetes 1.8.</td><td>2020-04-03</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
<tr>
	<td>Self-deployed cluster master update.</td><td>You can now use the TKE console to perform rolling updates of Kubernetes masters on self-deployed clusters.</td><td>2020-04-02</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Updating a Cluster</a></td>
</tr>
</table>

## March 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
	<td>TKE now supports both GlobalRouter and VPC-CNI network modes.</td>
	<td>TKE now supports GlobalRouter and VPC-CNI network modes for your business needs. Choose the one that fits your needs.</td>
	<td>2020-03-30</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/38966">How to Choose TKE Network Mode</a></td>
</tr>
<tr>
	<td>TKE has stopped providing features related to TencentHub.</td><td>We plan to discontinue support for TencentHub this month, so TKE has officially stopped providing features related to TencentHub and no longer supports related APIs.</td>
	<td>2020-03-25</td><td>-</td>
</tr>
<tr>
    <td>TKE supports enabling "Local Disk Formatting" for BM and big data models.</td> <td>TKE now allows you to enable "Local Disk Formatting" for BM and big data model nodes and also allows you to mount and set container directories.</td><td>2020-03-02</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating Clusters</a></td>
</tr>
</table>

## February 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
    <td>TKE cluster scaling groups support node shutdown when scaling in.</td> <td>When scaling in, cluster scaling groups now support <b>shutting nodes down instead of terminating or draining them</b>. To enable this feature, you need to submit a <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1">ticket</a>.</td> <td>2020-02-17</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
<tr>
    <td>TKE fully launches Kubernetes 1.16 and passes <a href="https://github.com/cncf/k8s-conformance/pull/879">conformance verification.</a></td><td><ul class="params"><li>Users can create self-deployed clusters and managed clusters of the Kubernetes 1.16 version.</li><li>Users can update a cluster from Kubernetes 1.14 to 1.16.</li></ul></td><td>2020-02-14</td>
    <td><ul  class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading a Cluster</a></li></ul></td>
</table>

## January 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TKE allows users to create clusters using a cluster template.</td> <td>The template-based cluster creation feature provides multiple templates for creating managed clusters, self-deployed clusters, and elastic clusters, <b>simplifying the current cluster creation process and improving the cluster creation experience</b>. It applies to various business scenarios such as HA clusters and GPU clusters.</td> <td>2020-01-12</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
</table>

## December 2019

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
	<td>TKE supports the PVs and the PVCs of the Cloud File Storage (CFS) and Cloud Object Storage (COS) types.</td>
    <td>TKE supports the PVCs and the PVs of the CFS and COS types <b>connecting storage resources with Kubernetes</b>, which makes it convenient for users to use basic Tencent Cloud products through the native Kubernetes mode and allows users to <b>manage file storage and object storage via PVs and PVCs</b>.</td> <td>2019-12-27</td>
	<td>-</td>
</tr>
<tr>
	<td>TKE Kubernetes 1.16 beta is launched.</td>
    <td><li>This allows users to create Kubernetes 1.16 self-deployed clusters and managed clusters via the console.</li><li>It also allows users to upgrade the Kubernetes version of a cluster from 1.14 to 1.16.</li></td> <td>2019-12-18</td>
	<td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading a Cluster</a></li></ul></td>
</tr>
<tr>
	<td>TKE supports purchasing multiple data disks during node initialization as well as custom formatting.</td>
    <td>TKE allows users to purchase multiple data disks during node initialization and supports custom data disk formatting, allowing users to <b>isolate data</b> and <b>format settings flexibly based on their actual needs</b>.</td> <td>2019-12-12</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding Nodes</a></td>
</tr>
<tr>
	<td>TKE nodes support the in-place rolling updates of minor Kubernetes versions.</td>
    <td>Nodes in in-place updates support the rolling update mode. <li><b>Only one node is updated at a time, and </b>the next node will be updated only after the current node is successfully updated. </li><li>Currently, in-place updates only support <b>updating different minor versions of the same major version</b>.</li></td> <td>2019-12-03</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Updating a Cluster</a></td>
</tr>
</table>


## November 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
	<td>The beta custom Hostname supported by TKE is launched.</td>
    <td>The TKE custom Hostname feature provides the following advantages: <li><b>Helps clusters interwork with enterprises’ internal domain name service systems.</b></li><li><b>Makes it easier for users to quickly create nodes with a specified Hostname in batches</b>.</li></td>
    <td>2019-11-15</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding a Node</a></td>
</tr>
<tr>
	<td>TKE Ingress performance optimization is released.</td>
    <td>TKE Ingress performance is optimized to better serve users. <li>CLB changes are optimized to <b>allow batch calling APIs to process backend binding.</b></li><li>CVM backend query is optimized to help users <b>avoid unnecessary repeated queries</b>.</li></td>
    <td>2019-11-07</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30673">Ingress Management</a></td>
</tr>
</table>

## October 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>Cluster worker nodes support configuring several security groups simultaneously and using the default security group.</td>
    <td>TKE allows <b>a cluster worker node to bind multiple security groups</b> and provides a default security group, helping users <b>quickly configure available security groups</b>.</td>
<td>2019-10-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/9084">TKE Security Group Settings</a></td>
</tr>
<td>Node labels can be added in batches during creation of clusters/nodes.</td>
    <td>When a cluster is created or new nodes are added to an existing cluster, TKE allows users to <b>add labels for nodes that run the same business or have the same configurations</b>. The labels help users divide resources, label resource attributes, and filter and batch process massive resource volumes.</td>
<td>2019-10-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30634">Cluster Management</a></td>
</tr>
<tr>
<td>Runtime component Containerd supports the GPU model.</td>
    <td>The TKE runtime component Containerd supports the GPU model. When users need to <b>create a GPU application in a cluster, they can choose Containerd as the runtime component</b>.</td>
<td>2019-10-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/31088">How to Choose Containerd and Docker</a></td>
</tr>
<tr>
<td>The beta for rolling Kubernetes reinstallation and upgrade of TKE nodes is launched.</td>
    <td>TKE <b>supports the batch update of nodes in a cluster from an earlier version to a later version</b>. This feature applies to clusters whose <b>Kubernetes version is outdated and clusters whose nodes do not have relevant custom configurations</b>. Custom configurations will become invalid after the rolling reinstallation and upgrade of nodes.</td>
<td>2019-10-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading a Cluster</a></td>
</tr>
<tr>
<td>TKE supports GPU monitoring metrics.</td>
    <td>TKE supports GPU monitoring metrics, <b>enabling users to monitor GPU-related resources</b>. By checking monitoring data, users can precisely identify specific problems, shorten troubleshooting time, and reduce OPS costs, ensuring the continuous and stable running of businesses.</td>
<td>2019-10-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30691">List of Monitoring and Alarm Metrics</a></td>
</tr>
</table>

## September 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<td>Related APIs of the TKE cluster scaling group have been updated to API 3.0.</td>
    <td>TKE APIs have been updated to 3.0 and support all-region access. <b>The new API documentation is more standardized and comprehensive, with unified parameter styles and common error codes. The SDK/CLI version is consistent with the API documentation</b>, providing a simple and convenient user experience.</td>
<td>2019-09-12</td>
<td>Related APIs of the Scaling Group</td>
<tr>
<td>TKE Kubernetes 1.14 is fully launched and has passed conformance verification.</td>
    <td>TKE <b>Kubernetes 1.14 is fully launched</b> and has passed conformance verification to ensure that the latest Kubernetes version is available.</td>
<td>2019-09-07</td>
<td><a href="https://github.com/cncf/k8s-conformance/tree/master/v1.14/tencentcloud">Conformance Verification</a></td>
</tr>
<tr>
<td>TKE supports the Tencent Cloud tag, allowing authorization by tag.</td>
    <td>If the Tencent Cloud tag is added to a cluster when the cluster is created, <b>the Tencent Cloud services, cloud disks, CLBs, and other resources created in the cluster will automatically inherit the cluster’s tag</b>, allowing users to clearly view resource categories.</td>
<td>2019-09-06</td>
<td>-</td>
</tr>
<tr>
<td>The default instance type for created LoadBalancer-type services is CLB.</td>
    <td>When TKE creates a LoadBalancer-type service, the default instance type is CLB.<b> This instance type covers all features of a conventional CLB</b>. <li>The CLB instance type supports the TCP, UDP, HTTP, and HTTPS protocols.</li><li>It provides flexible forwarding capabilities based on domain names and URLs.</li></td>
<td>2019-09-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8847">Instance Types</a></td>
</tr>
<tr>
<td>TKE self-deployed clusters support the separate viewing of Master and Etcd nodes.</td>
    <td>This feature allows users to <b>intuitively view the list of all Master and Etcd nodes of a self-deployed cluster and the details of such nodes</b>. Users no longer have trouble distinguishing Master and Etcd nodes in self-deployed clusters.</td>
<td>2019-09-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30649">Node Management</a></td>
</tr>
</table>


## August 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>
When a “self-deployed cluster” is created, a security group is automatically bound to the Master node.</td>
    <td>This feature can <b>automatically bind an applicable security group to the Master node in a self-deployed cluster</b>. This prevents the Master node from being associated with a security group with communication problems and improves the success rate of creating self-deployed clusters.</td>
<td>2019-08-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
<tr>
<td>TKE supports the visualized display of the cluster creation progress.</td>
    <td>The visualized display of the cluster creation progress <b>enables users to see the waiting time for cluster creation and troubleshoot the steps with exceptions</b>. This improves the success rate of cluster creation and ensures the continuous and stable running of businesses.</td>
<td>2019-08-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
<tr>
<td>Open source components: <a href="https://github.com/TencentCloud/tencentcloud-cloud-controller-manager">TencentCloud-controller-manager</a> and <a href="https://github.com/TencentCloud/kubernetes-csi-tencentcloud">cbs-csi</a> support Kubernetes 1.14.</td>
    <td>The open source components Tencent Cloud-controller-manager and cbs-csi<b> support Kubernetes 1.14</b>.</td>
<td>2019-08-12</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/32430">Open Source Components</a></td>
</tr>
<tr>
<td>Use existing CLB instances to create Ingress.</td>
<td>Users no longer have to create new CLB instances in order to create a new Ingress. They can now avoid additional costs by using existing CLB instances to create a new Ingress.</td>
<td>2019-08-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30673">Basic Ingress Features</a></td>
</tr>
<tr>
<td>TKE Kubernetes 1.14 beta is launched.</td>
    <td>Users can now use the TKE console to <b>create clusters based on Kubernetes 1.14</b>.</td>
<td>2019-08-04</td>
<td>-</td>
</tr>
<tr>
<td>Related APIs of TKE cluster nodes have been updated to API 3.0.
</td>
<td>TKE APIs have been updated to 3.0 and support all-region access. The new API documentation is more standardized and comprehensive, with unified parameter styles and common error codes. The SDK/CLI version is consistent with the API documentation, providing a simple and convenient user experience.</td>
<td>2019-08-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/6787">API 3.0</a></td>
</tr>
<tr>
<td>TKE now supports application-level log collection.</td>
    <td>By checking the collected file logs in the container, <b>users can view the running status of applications in the container</b>, precisely identify specific problems, shorten the troubleshooting time, and reduce OPS costs to ensure the continuous and stable running of businesses.</td>
<td>2019-08-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/32419">Log Collection</a></td>
</tr>
</table>

## July 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<tr>
<td>The CLB health check failure issue in IPVS mode is fixed.</td>
<td>Fixes the compatibility issue between the TLinux kernel and IPVS and fixes the CLB health check failures in IPVS mode.</td>
<td>2019-07-16</td>
<td>-</td>
<tr>
<td>TKE scaling groups support spot models.</td>
    <td>When TKE creates a scaling group, users can choose spot instances <b>and purchase pods at a certain discount</b>. However, the system may automatically recall these pods that are sold at a discount.
</td>
<td>2019-07-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/17816">Spot Instances</a></td>
</tr>
<tr>
<td>TKE supports choosing Containerd as the container runtime component.</td>
    <td>When Containerd serves as the container runtime component, <b>it only runs necessary features to manage images and the container lifecycle</b>, providing users with more stable and more resource-efficient container running infrastructures.
</td>
<td>2019-07-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/31088">How to Choose Containerd and Docker</a></td>
</tr>
</table>

## June 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>The beta VPC-CNI network mode is launched.</td>
    <td>TKE provides the VPC-CNI extended network mode, which <b>can assign intra-VPC IP addresses to Pods in a cluster</b>. In the VPC-CNI mode, clusters can create StatefulSet that supports fixed IP address types, and the Pod IP addresses will not change because of restart or migration.</td>
<td>2019-06-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/38971">Enabling VPC-CNI When Creating the Cluster</a></td>
<tr>
<td>The beta StatefulSet with fixed IP addresses is launched.</td>
    <td> The StatefulSet with fixed IP addresses help <b>resolve issues related to IP address changes caused by Pod restart or migration</b>. Users can create the StatefulSet with fixed IP addresses for source IP address authorization, IP-based process review, log query based on Pod IP addresses, and other business needs to ensure the continuous and stable running of businesses.</td>
<td>2019-06-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/38974">Managing StatefulSets with Static Pod IP Addresses</a></td>
</tr>
<tr>
<td>TKE uses the new console version by default.</td>
    <td>In order to provide a better product user experience, TKE now uses <b>the new Kubernetes-compatible console</b>.</td>
<td>2019-06-17</td>
<td><a href="https://console.cloud.tencent.com/tke2">The New TKE Console</a></td>
</tr>
<tr>
<td>Fixes an issue where cordoning a node while it is being created causes the process to freeze.</td>
<td>Fixes an issue where cordoning a node while it is being created causes the process to freeze.</td>
<td>2019-06-13</td>
    <td><a href="https://github.com/kubernetes/kubernetes/pull/69047">pr69047</a></td>
</tr>
<tr>
<td>Fixes an issue where too many secrets results in a pod creation failure.</td>
<td>Fixes an issue where too many secrets results in a pod creation failure.</td>
<td>2019-06-13</td>
    <td><a href="https://github.com/kubernetes/kubernetes/pull/74755">pr74755</a></td>
</tr>
<tr>
<td>The new version of the TKE international console is launched.</td>
    <td>The new version of the TKE international console adjusts a series of functional modules and <b>provides a native, easier-to-use platform</b>, which helps users resolve environmental issues in development, testing, and OPS, reduce costs, and improve efficiency.</td>
<td>2019-06-05</td>
    <td>TKE international console.</td>
</tr>
<tr>
<td>Managed clusters support configuring ACLs for public network access.</td>
<td>Users can set security group rules for managed clusters that enable public network access.</td>
<td>2019-06-05</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/9084">TKE Security Group Settings</a></td>
</tr>
</table>

## May 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>Nodes in a scaling group tolerate drain failures during automatic scaling in.</td>
    <td>When scale-in conditions such as the number of idle nodes are met, the cluster automatically scales in. <b>However, only when all pods of a node are successfully scheduled to other nodes can the pods be drained successfully and scale-in be performed successfully</b>.</td>
<td>2019-05-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
<tr>
<td>Supports registering the TKE network to CCN.</td>
    <td>TKE allows users to <b>register existing clusters to CCN, which can manage the container’s network</b>. After the container’s network is registered, you can enable or disable its IP range routing on the CCN side to achieve interconnection between the container’s cluster and the resources in CCN.</td>
<td>2019-05-17</td>
<td>Supports registering the TKE network to CCN.</td>
</tr>
<tr>
<td>TKE supports GPU virtualization.</td>
<td><ul  class="params"><li>Extension components support the installation and the deployment of GPU visualization components.</li><li>Clusters that have deployed GPU nodes and gpu_manager can extend GPU-related settings during workload creation.</li></ul></td>
<td>2019-05-17</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/30656">Using a GPU Node</a></td>
</tr>
</table>


## April 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>Kubelet applies CNI mode by default</td>
<td>TKE Kubelet uses the VPC-CNI network mode by default.</td>
<td>2019-04-24</td>
<td>-</td>
</tr>
<tr>
<td>Docker 18.06 is launched for beta testing.</td>
<td>Runtime components that use Docker 18.06 can create clusters.</td>
<td>2019-04-22</td>
<td>-</td>
</tr>
<tr>
<td>The new alarm version is launched and supports all regions.</td>
    <td>Alarms enable users to discover exceptions in TKE in a timely manner to ensure business stability and reliability. <b>The new alarm version provides more alarm metrics</b>. We recommend that you configure necessary alarms for all production clusters.</td>
<td>2019-04-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30690">Setting Alarms</a></td>
</tr>
<tr>
<td>Cluster management - Kubernetes online updates - managed master nodes</td>
    <td>In the managed cluster mode, the Master and Etcd nodes of your Kubernetes cluster will be centrally managed and maintained by the Tencent Cloud technical team. <b>The online updates of the Kubernetes version ensure business stability</b>.</td>
<td>2019-04-11</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/31417">Cluster Hosting Modes</a></td>
</tr>
<tr>
<td>Self-deployed clusters support Master and Etcd monitoring.</td>
<td>Users can query monitoring information about Master and Etcd nodes on the **Node Management** page of self-deployed clusters.</td>
<td>2019-04-11</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/30689">Viewing Monitoring Data</a></td>
</tr>
</table>


## March 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>TKE supports Bare Metal (BM 2.0) nodes.</td>
<td>BM physical servers are a type of on-demand pay-as-you-go physical server rental service that provides high-performance and securely isolated physical server clusters for cloud users.</td>
<td>2019-03-28</td>
<td>-</td>
</tr>
<tr>
<td>Users can use a purchased CVM to create clusters.</td>
    <td>Using existing CVMs to create clusters helps users <b>reuse existing resources and reduce costs</b>.</td>
<td>2019-03-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30637#UseExistingCVMCreateCluster">Create a cluster using existing CVMs</a></td>
</tr>
<tr>
<td>Cluster auto-scaling (CA) supports disabling pod draining.</td>
<td>When there are multiple idle nodes in a cluster, scale-in will be triggered. CA supports disabling pod draining.</td>
<td>2019-03-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
<tr>
<td>Cluster scaling groups support the scale-out of GPU nodes.</td>
    <td>When a pod in a cluster cannot be scheduled due to a lack of available resources in the cluster, the previously set auto scale-out policy will be triggered. <b>GPU nodes can be added during scale-out</b>.</td>
<td>2019-03-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
</table>

## February 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>A new monitoring system is released.</td>
    <td>A good monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud TKE. <b>You can collect monitoring data in different dimensions for different resources</b> to quickly understand the resource usage situation and easily locate errors.</td>
<td>2019-02-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
</tr>
<tr>
<td>Self-deployed clusters support Kubernetes 1.12.</td>
    <td>Users can now <b>create Kubernetes 1.12 self-deployed clusters</b> in the TKE console.</td>
<td>2019-02-15</td>
<td>-</td>
</tr>
<tr>
<td>Fixes the runC vulnerability CVE-2019-5736.</td>
<td>The lightweight container runtime environment runc was found to have a container escape vulnerability, which allowed attackers to overwrite the host runc file (and consequently obtain host root access). This vulnerability has been fixed.</td>
<td>2019-02-13</td>
    <td>[WARNING] runC Container Escape Vulnerability</td>
</tr>
</table>

## January 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>Existing CLBs can be used to create Service.</td>
<td>Using existing CLBs to create Service can save resources and help users reduce costs.</td>
<td>2019-01-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/36832">Service Management</a></td>
</tr>
<tr>
<td>Custom images can be used to create clusters.</td>
<td>TKE allows users to create custom images based on the basic image provided by TKE and use these custom images to create clusters. To enable this feature, submit a <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1">ticket</a> to apply.</td>
<td>2019-01-24</td>
    <td>Custom Images</td>
</tr>
<tr>
<td>Affinity scheduling can be set during workload creation.</td>
    <td>YAML is delivered to the Kubernetes cluster to schedule pods in a workload. <b>The affinity and anti-affinity mechanism of Kubernetes ensures that pods are scheduled according to specific rules</b>.</td>
<td>2019-01-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30668">Setting the Scheduling Rule for a Workload</a></td>
</tr>
<tr>
<td>TKE allows multiple Services to use the same CLB instance.</td>
<td>Multiple Services can now use the same CLB instance to avoid additional resource costs.</td>
<td>2019-01-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/36832">Service Management</a></td>
</tr>
</table>

## December 2018
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
	<td>TencentHub supports Helm Chart management.</td>
	<td>Helm is a package management tool of Kubernetes. Chart is a collection of files describing Kubernetes resources. Tencent Hub provides an address for users to store Helm Charts.</td>
	<td>2018-12-26</td>
	<td>Overview of Helm Charts</td>
	</tr>
	<tr>
	<td>TKE supports Helm application installation.</td>
        <td>Helm is a packaging tool for managing Kubernetes applications. <b>TKE has integrated Helm-related features to visually add, delete, modify, and query Helm Charts in a specified cluster.</b></td>
  <td>2018-12-26</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30683">Helm Application Management</a></td>
	</tr>
	<tr>
	<td>The privilege escalation vulnerability in Kubernetes is fixed.</td>
	<td>Tencent Cloud Security Center detected that a severe privilege escalation vulnerability existed in Kubernetes (vulnerability ID: CVE-2018-1002105). This vulnerability has been fixed. Now, TKE can effectively prevent attackers from using the vulnerability to illegally access Kubernetes cluster resources, inducing privilege escalation and initiating malicious requests that ultimately jeopardize the security of the business system.</td>
	<td>2018-12-04</td>
        <td>[WARNING] Privilege Escalation Vulnerability in Kubernetes</td>
	</tr>
	<tr>
	<td>Removes Kubernetes 1.7.8 as an option for creating clusters.</td>
	<td>Users can disable the entry for creating clusters of Kubernetes 1.7.8 in the console. To enable this feature, submit a <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1">ticket</a> to apply.</td>
	<td>2018-12-04</td>
        <td>-</td>
	</tr>
	<tr>
	<td>pr71415 is merged to fix CVE-2018-1002105.</td>
	<td>CVE-2018-1002105 is fixed and backend error responses are processed.</td>
	<td>2018-12-04</td>
        <td><a href="https://github.com/kubernetes/kubernetes/pull/71415">pr71415</a></td>
	</tr>
	<tr>
	<td>Kubelet disables kmem accounting to avoid kernel cgroup leakage.</td>
	<td>Kernel cgroup leakage has an adverse impact on the system. Kubelet disables kmem accounting to avoid kernel cgroup leakage.</td>
	<td>2018-12-04</td>
	<td>-</td>
	</tr>
</table>

## November 2018
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
	<td>The kubelet inotify leakage issue is fixed.</td>
	<td>The kubelet inotify leakage problem is fixed.</td>
	<td>2018-11-12</td>
	<td>-</td>
	</tr>
</table>

## October 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
	<td>The beta TKE console is launched.</td>
        <td>The new TKE console adjusts a series of feature modules to<b> provide you with a native and easy-to-use platform</b>. <b>The new and old consoles are fully compatible in terms of features</b>. Switching consoles will not affect your business. You can use the new console to continue to operate existing clusters.</td>
	<td>2018-10-31</td>
        <td>Notes on the New Console</td>
	</tr>
	<tr>
	<td>Service CLB can be bound to specified nodes.</td>
	<td>If your cluster is large, you will need to set affinity for entry-type applications to schedule them to certain nodes. You can configure the Service CLB to be bound only to specified nodes.</td>
	<td>2018-10-31</td>
	<td>-</td>
	</tr>
	<tr>
	<td>Conflicts and Pod creation failures caused by the frequent updates of quota statuses by the quota controller are resolved.</td>
	<td>Previously, if the quota controller frequently updated the quota status, conflicts and even Pod creation failures would occur. This problem has been resolved.</td>
	<td>2018-10-22</td>
	<td>-</td>
	</tr>
</table>

## September 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>The default Kubernetes version in TKE is 1.10.</td>
		<td>When a new cluster is created, the default Kubernetes version is 1.10. However, you can change the version based on your actual needs.</td>
		<td>2018-09-10</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
	</tr>
	<tr>
		<td>BM clusters support Kubernetes 1.10.</td>
		<td>TKE allows users to create BM clusters with Kubernetes 1.10.</td>
		<td>2018-09-10</td>
		<td>-</td>
	</tr>
	<tr>
		<td>BM clusters support Ubuntu 16.04.</td>
		<td>When TKE creates a BM cluster, the default operating system is Ubuntu 16.04.</td>
		<td>2018-09-10</td>
		<td>-</td>
	</tr>
</table>

## July 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE supports the Russia and India regions.</td>
		<td>The TKE console supports the Russia and India regions. You can go to the console to switch to and use these regions.</td>
		<td>2018-07-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE supports private network access to the Master node.</td>
		<td>After the private network access entry is enabled, TKE allows private network access to the Master node.</td>
		<td>2018-07-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>The open source component tencentcloud-cloud-controller-manager is released.</td>
        <td>This component is the Cloud Controller Manager implementation for TKE <b>and allows the following features to be implemented on the Kubernetes clusters built by Tencent Cloud CVMs</b>:<li>Updates the relevant addresses information of the Kubernetes nodes.</li><li>routecontroller: creates routes within pod IP ranges in a VPC. </li><li>servicecontroller: creates a corresponding CLB when a load balancer-type service is created in a cluster.</li></td>
		<td>2018-07-30</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32430">Open Source Components</a></td>
	</tr>
	<tr>
		<td>The open source component kubernetes-csi-tencentcloud is released.</td>
        <td>This component is a plug-in for the Tencent Cloud CBS service and complies with CSI standards. <b>It allows users to use CBS on Kubernetes clusters built by Tencent Cloud CVMs</b>.</td>
		<td>2018-07-30</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32430">Open Source Components</a></td>
	</tr>
	<tr>
		<td>The BM cluster ingress plug-in is released.</td>
		<td>ingress-tke-bm is the ingress controller for Tencent Cloud TKE BM clusters. This controller monitors ingress resources, creates BM CLBs, and binds them to the corresponding services.</td>
		<td>2018-07-30</td>
		<td>-</td>
	</tr>
</table>

## June 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>CCS is renamed TKE.</td>
        <td><b>Tencent Kubernetes Engine (TKE) </b>is a highly scalable and high-performance container management service. It allows you to easily run applications on a managed CVM instance cluster.</td>
		<td>2018-06-22</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/6759">Tencent Kubernetes Engine</a></td>
	</tr>
	<tr>
		<td>Cluster auto scaling supports custom configurations.</td>
		<td>TKE allows users to customize cluster scaling settings based on their actual needs, making it easier for them to configure businesses flexibly.</td>
		<td>2018-06-22</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
	</tr>
	<tr>
		<td>Node initialization supports the import of scripts.</td>
        <td><b>This feature allows users to configure a node using custom data</b>. As long as the script can be re-inputted and has a clear retry pattern, it will be used to configure the node after startup.</td>
		<td>2018-06-22</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding a Node</a></td>
	</tr>
</table>

## May 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE supports BM clusters.</td>
		<td>BM container clusters extend Tencent Cloud’s CPM, BM Load Balancer, and other Kubernetes plug-ins, providing a complete set of features such as high-efficient deployment and resource scheduling for containerized applications. This helps industries such as gaming and AI easily cope with the challenges of high-performance computing business scenarios.</td>
		<td>2018-05-01</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE supports GPU clusters.</td>
        <td>If your business <b>involves scenarios such as deep learning and high-performance computing</b>, you can use the GPU feature supported by TKE, which can help you quickly use a GPU container.</td>
		<td>2018-05-01</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30642">Enabling GPU Scheduling for a Cluster</a></td>
	</tr>
</table>

## April 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE integrates the new Tencent Cloud UI version.</td>
		<td>The new Tencent Cloud UI is elegant and easy to use, offering a better container service experience.</td>
		<td>2018-04-01</td>
        <td><a href="https://console.cloud.tencent.com/tke2">TKE Console</a></td>
	</tr>
	<tr>
		<td>TKE now supports all CVM models.</td>
		<td>During cluster creation or node addition, the models available for selection on the TKE console are consistent with those on the CVM platform.</td>
		<td>2018-04-01</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
	</tr>
</table>

## March 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE supports the auto-scaling of services.</td>
        <td>Horizontal Pod Autoscaler (HPA) can <b>automatically scale the number of pods for services according to the average CPU utilization and other metrics of target pods</b>.</td>
		<td>2018-03-01</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32424">Basic Operations of Automatic Scaling</a></td>
	</tr>
	<tr>
		<td>The TKE console interface is updated.</td>
		<td>The feature modules of the TKE console are adjusted.</td>
		<td>2018-03-01</td>
		<td>-</td>
	</tr>
</table>

## February 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE supports the auto-scaling of clusters.</td>
        <td>Cluster auto scaling <b>adjusts the number of nodes dynamically according to resource demand</b>:<li>If pods become unschedulable due to a lack of resources, the cluster will automatically scale out.</li><li>If there are enough idle nodes, the cluster will automatically scale in to reduce costs.</li></td>
		<td>2018-02-08</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
	</tr>
	<tr>
		<td>TKE supports log collection.</td>
        <td>This feature allows <b>log files from services or specific node paths to be sent to Kafka, Elasticsearch, or CLS</b> so that users can store and analyze them.</td>
		<td>2018-02-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32419">Log Collection</a></td>
	</tr>
	<tr>
		<td>TKE supports application management.</td>
		<td>TKE supports the group management of services via applications, which significantly simplifies service management.</td>
		<td>2018-02-06</td>
		<td>-</td>
	</tr>
</table>


## December 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>Vouchers can be used to purchase cluster nodes.</td>
		<td>TKE allows users to use vouchers in their accounts to purchase nodes.</td>
		<td>2017-12-20</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Empty clusters can be created.</td>
		<td>This feature allows users to create clusters that do not contain nodes.</td>
		<td>2017-12-20</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Users can set the container directory and the project of the resources when adding existing nodes.</td>
		<td><li>Container directory: users can set the directory for storing containers and images. We recommend that they be stored in data disks.</li><li>Project: newly added resources will be automatically assigned to this project.</li></td>
		<td>2017-12-20</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30652#addExistingNode">Adding an Existing Node</a></td>
	</tr>
</table>

## November 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>Cluster reservation policy.</td>
        <td><b>Reserves system process resources such as dockerd and kubelet</b>: when a cluster runs the retention policy, certain resources are reserved to ensure the proper running of system processes such as dockerd and kubelet.</td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Cluster draining policy.</td>
        <td><b>To ensure that there are sufficient resources for system processes, pods will be drained when necessary</b>.</td>
		<td>2017-11-30</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30654">Draining or Cordoning a Node</a></td>
	</tr>
	<tr>
		<td>Dockerd log rollback.</td>
        <td><b>Logs are recycled automatically to ensure that there is sufficient disk space</b>: when log files occupy a certain amount of memory, the log rollback feature will be triggered to automatically recycle logs to ensure that there is sufficient disk space.</td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Ingress forwarding rules support wildcards.</td>
        <td><b>Ingress forwarding rules must comply with both the rules for the public network load balancing domain names and the Kubernetes rules for the Ingress domain names</b>. <li>They support regular expressions with a length of 1-80 characters.</li><li>Other than regular expressions, they also support `a - z, 0 - 9, and -`. </li><li>For domain names with wildcards, currently, only one `*` can be used in a domain name, such as `*.example.com`.</li></td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
</table>


## October 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>The beta TKE application management feature is launched.</td>
        <td>With the rise of micro-service and Devops, users need to deploy and manage multiple services in multiple environments. <b>TKE supports the group management of services via applications</b>, which significantly simplifies service management.</td>
		<td>2017-10-31</td>
		<td>-</td>
	</tr>
	<tr>
		<td>The multi-region deployment of Image Registry supports the new Hong Kong (China) region.</td>
        <td>Image Registry is used to store Docker images, which are used to deploy TKE. Each image has a unique ID (the image's repository address + the image name + the image Tag). <b>Image Registry can be deployed in multiple regions, including the Hong Kong (China) region that is now also supported</b>.</td>
		<td>2017-10-31</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1051/38866">Image Registry Overview</a></td>
	</tr>
	<tr>
		<td>The Tencent Cloud international console supports TKE.</td>
		<td>The TKE international console is launched, which helps users solve environmental issues in development, testing, and OPS, reduce costs, and improve efficiency.</td>
		<td>2017-10-31</td>
		<td><a href="https://console.cloud.tencent.com/tke2?language=en">CCS International Console</a></td>
	</tr>
</table>

## September 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE Image Registry integrates access permission management.</td>
        <td>The address format of a TKE image is as follows: <code>ccr.ccs.tencentyun.com/${namespace}/${name}:${tag}</code>. <b>The following fields are required for configuring the permissions of Image Registry</b>:<li>${namespace}: the namespace of the image repository.</li><li>${name}: the name of the image repository.</li></td>
		<td>2017-09-26</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/11527">TKE Image Registry Resource-level Permission Settings</a></td>
	</tr>
	<tr>
		<td>TKE supports setting labels for services.</td>
        <td>TKE supports setting labels for service pods. <b>When searching services, you can filter them by label</b>.</td>
		<td>2017-09-26</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Configuration items can be imported to environment variables.</td>
		<td>When deploying a container in a pod, users can import the configuration items ConfigMap and Secret to environment variables.</td>
		<td>2017-09-26</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30674">Configuration</a></td>
	</tr>
	<tr>
		<td>Clusters support the Project attribute.</td>
        <td><li>Clusters are not project-specific, but CVMs, CLBs, and other resources in a cluster are project-specific.</li><li>Project: new resources added to the cluster will be allocated to the project.</li></td>
		<td>2017-09-26</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/11185">Projects of New Resources</a></td>
	</tr>
	<tr>
		<td>TKE supports the Singapore region.</td>
		<td>TKE now supports purchasing resources and deploying businesses in the Singapore region.</td>
		<td>2017-09-26</td>
        <td><a href="https://console.cloud.tencent.com/tke2">TKE Console</a></td>
	</tr>
</table>

## August 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE integrates the alarm platform.</td>
        <td>TKE allows users to set multi-dimensional alarms for clusters to <b>discover cluster exceptions quickly and reduce business risks</b>.</td>
		<td>2017-08-23</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30690">Setting Alarms</a></td>
	</tr>
	<tr>
		<td>TKE clusters support Kubernetes 1.7.</td>
        <td>TKE <b>allows users to create clusters with Kubernetes 1.7</b>. </td>
		<td>2017-08-23</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Continuous integration and deployment based on TencentHub.</td>
		<td>TencentHub is a management platform created by Tencent Cloud for storing R&D process files and creating DevOps workflows. TencentHub allows users to quickly and conveniently perform operations such as storage, query, and calls for files generated during the full project cycle.</td>
		<td>2017-08-23</td>
        <td>TencentHub Product Overview</td>
	</tr>
	<tr>
		<td>Image Registry adds the trigger feature.</td>
        <td>The Image Registry trigger feature allows users to trigger actions such as service update, webhook, and message push after creating an image. <b>The trigger feature can be combined with continuous integration for continuous deployment</b>.</td>
		<td>2017-08-23</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/10155">Trigger Overview</a></td>
	</tr>
	<tr>
		<td>Image Registry supports operation logs.</td>
		<td>Operation logs allow users to view image uploads and download records, which helps troubleshoot problems.</td>
		<td>2017-08-23</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Kubectl is used to operate clusters on public networks.</td>
        <td>Kubectl is a CLI tool for Kubernetes cluster operations. <b>You can use Kubectl to connect a local client to a TKE cluster</b>.</td>
		<td>2017-08-04</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30639">Connecting to a Cluster</a></td>
	</tr>
	<tr>
		<td>TKE clusters integrate access permission management.</td>
        <td>Access management is mainly used to help you securely manage and control access to resources under your Tencent Cloud accounts. <b>Using CAM, you can create, manage, and terminate users (or user groups) and manage the use of Tencent Cloud resources through identity management and policies</b>.</td>
		<td>2017-08-04</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/37499">TKE Cluster-level Permission</a></td>
	</tr>
</table>


## July 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE supports configuration file management.</td>
        <td><li>The configuration file management feature can help you manage the configurations of different businesses under different environments. It supports multiple versions and the YAML format.</li><li>The configuration file supports multiple versions, allowing you to update and roll back applications. </li><li>It also allows you to quickly import configurations, in the form of files, into containers.</li></td>
		<td>2017-07-19</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE supports CI source code building.</td>
        <td>Continuous container integration <b>enables the automatic and manual building of container images on the Tencent TKE Platform.</b></td>
		<td>2017-07-18</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1051/38869">Image Registry Overview</a></td>
	</tr>
	<tr>
		<td>Image Registry adds TencentHub images.</td>
		<td>Image Registry allows users to view and use TencentHub images.</td>
		<td>2017-07-18</td>
		<td>TencentHub Product Overview</td>
	</tr>
	<tr>
		<td>Image Registry adds "Favorite Public Images".</td>
		<td>"Favorite Public Images" will display the images bookmarked by users, allowing users to query and use specific images.</td>
		<td>2017-07-18</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1051/38866">Image Registry Overview</a></td>
	</tr>
	<tr>
		<td>Image Registry supports multiple namespaces.</td>
        <td><b>Image Registry supports the creation of multiple namespaces. The names of namespaces are globally unique. </b>If the namespace name you want to use is already being used by another user, try using another appropriate name.</td>
		<td>2017-07-18</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1051/38866#.E5.88.9B.E5.BB.BA.E5.91.BD.E5.90.8D.E7.A9.BA.E9.97.B4">Creating a Namespace</a></td>
	</tr>
</table>

## June 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE supports NFS volumes.</td>
		<td>NFS volumes are used for the persistent storage of data that is read and written many times. They can also be used in scenarios such as big data analysis, media processing, and content management. </td>
		<td>2017-06-24</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30678">Volume Management</a></td>
	</tr>
	<tr>
		<td>TKE supports privileged containers and working directory configurations.</td>
        <td><li>A privileged container has a certain priority. </li><li>WorkingDir: specifies the current working directory. If it does not exist, one will be automatically created. If no directory is specified, the default directory when the container runs is used. If workingDir is not specified in the image or through the console, the default workingDir is `/`.</li></td>
		<td>2017-06-24</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE supports cluster capacity.</td>
		<td>A cluster is a collection of cloud resources required for running a container, including several CVMs and CLBs. You can run your applications in your cluster.</td>
		<td>2017-06-07</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30635">Cluster Overview</a></td>
	</tr>
	<tr>
		<td>TKE supports auto-formatting data disks and specifying container directories while creating/adding CVMs in container clusters.</td>
		<td>If the system disk capacity is small or a server with a data disk needs to format the data disk, you can set the storage directory of the containers and images.</td>
		<td>2017-06-07</td>
        <td><li><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding a Node</a></li></td>
	</tr>
	<tr>
		<td>TKE supports service re-deployment.</td>
		<td>Re-deployment means to re-deploy containers under a service and re-fetch images.</td>
		<td>2017-06-07</td>
        <td><li><a href="https://intl.cloud.tencent.com/document/product/457/36832">Service Management</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30673">Basic Ingress Features</a></li></td>
	</tr>
</table>

## April 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE supports adding existing CVMs to container clusters.</td>
		<td>TKE allows users to add existing CVMs to container clusters, which helps users reuse existing resources and effectively reduce costs.</td>
        <td>2017-04-27</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30652#.E6.B7.BB.E5.8A.A0.E5.B7.B2.E6.9C.89.E8.8A.82.E7.82.B9">Adding an Existing Node</a></td>
	</tr>
	<tr>
		<td>TKE supports the query of monitoring metrics for instances, services, and clusters.</td>
		<td>A good monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud TKE. You can collect monitoring data in different dimensions for different resources to quickly understand the resource usage situation and easily locate errors.</td>
        <td>2017-04-27</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
	</tr>
	<tr>
		<td>TKE supports viewing container logs.</td>
		<td>By creating log collection rules, TKE can provide users with log information from within a cluster, making it easier for them to maintain and troubleshoot containers.</td>
        <td>2017-04-27</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32419">Log Collection</a></td>
	</tr>
	<tr>
		<td>The TKE remote terminal allows you to upload and download files remotely.</td>
		<td><ul class="params"><li>When uploading files, you need to specify the file directory.</li><li>When downloading files, you need to specify the file path.</li></ul></td>
        <td>2017-04-19</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/9120">Basic Remote Terminal Operations</a></td>
	</tr>
	<tr>
		<td>TKE supports the creation of monthly subscription CVMs to clusters.</td>
        <td><b>Monthly subscription is a prepaid mode that requires customers to pay for CVMs for a period of one or multiple months/years in advance. </b>It is cheaper than the pay-as-you-go mode and is suitable for scenarios where device demands can be predicted in advance.</td>
        <td>2017-04-19</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding a Node</a></td>
	</tr>
	<tr>
		<td>TKE supports custom security groups when creating a cluster.</td>
        <td>If the current default security group cannot meet your business requirements, you can customize cluster security groups. For details, see<a href="https://intl.cloud.tencent.com/document/product/213/34275">Managing Security Group Rules</a>.</td>
        <td>2017-04-19</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
	</tr>
</table>

## March 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE allows remote web terminals to log in to containers.</td>
        <td>Remote terminals help you debug containers quickly and connect to the containers for troubleshooting. <b>It supports file copy, paste, upload, and download operations, and helps solve the problems of long container login paths and difficult debugging</b>.</td>
        <td>2017-03-15</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/9120">Remote Terminal Basic Operations</a></td>
	</tr>
	<tr>
		<td>TKE supports third-party image creation services.</td>
        <td>The third-party image creation service <b>helps users deploy applications flexibly based on their actual business needs</b>.</td>
        <td>2017-03-15</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE now supports 7-layer load balancing.</td>
        <td>An Ingress is a collection of rules that allow access to services within a cluster. You can configure different forwarding rules to <b>allow different URLs to access different services within the cluster</b>.</td>
        <td>2017-03-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/37013">Ingress Management</a></td>
	</tr>
	<tr>
		<td>Users can query monitoring information about clusters, services, and pods.</td>
        <td>A good monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud TKE. <b>You can collect monitoring data in different dimensions for different resources </b>to quickly understand the resource usage situation and easily locate errors.</td>
        <td>2017-03-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
	</tr>
	<tr>
		<td>TKE supports native Kubernetes APIs, requesting Kubernetes certificates via Tencent Cloud APIs, and all Kubernetes features.</td>
        <td>TKE makes it easy for you to build, operate, and manage container clusters by seamlessly utilizing Tencent Cloud computing, networking, storage, monitoring, and security capabilities. <b>You can refer to corresponding examples in the API documentation to perform operations such as adding, deleting, modifying, and querying scaling groups, networks, nodes, and clusters</b>.</td>
        <td>2017-03-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32029">Overview of APIs</a></td>
	</tr>
</table>

## December 2016
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>Cluster management.</td>
		<td>Cluster management supports cluster addition, deletion, modification, and query, VPC-based container clusters, cross-AZ clusters, and open-source native Kubernetes APIs.</td>
        <td>2016-12-26</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30634">Cluster Management</a></td>
	</tr>
	<tr>
		<td>Service management.</td>
		<td>Service management supports service addition, deletion, modification, and query, the creation of services via private images and official Docker images, and cross-AZ scheduling of services.</td>
        <td>2016-12-26</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/36832">Service Management</a></td>
	</tr>
	<tr>
		<td>Image management.</td>
		<td>Image management supports official Docker images, My Images, uploading and downloading private images, and official Docker image acceleration.</td>
        <td>2016-12-26</td>
        <td> - </td>
	</tr>
	<tr>
		<td>Cluster monitoring and container monitoring.</td>
		<td>TKE provides the basic monitoring feature for all clusters by default.</td>
        <td>2016-12-26</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30689">Viewing Monitoring Data</a></td>
	</tr>
	<tr>
		<td>Service creation, event updates, and rolling updates for services.</td>
		<td>Rolling updates indicate that pods are updated one by one, which allows you to update the service without interrupting your business.</td>
        <td>2016-12-26</td>
		<td>-</td>
	</tr>
</table> 

<style>
	.params{ margin-bottom:0px!important; } 
</style>
