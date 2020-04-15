## March 2020

<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
    <td>Supports local disk formatting configuration for nodes running on bare metal and big data models.</td><td>Supports local disk formatting configuration for nodes running on bare metal and big data models. It also supports configuring and mounting container directories.</td><td>2020-03-02</td>
    <td><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></td>
</tr>
</table>

## February 2020

<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
    <td>Supports node shutdown when scaling down</td> <td>When scaling down, cluster scaling groups now support <b>shutting nodes down, instead of terminating or draining them</b>. To enable this feature, you need to submit a <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1">ticket</a>.</td> <td>2020-02-17</td>
	<td><a href="https://cloud.tencent.com/document/product/457/32190">Cluster Scaling</a></td>
</tr>
<tr>
    <td>TKE has been upgraded to Kubernetes 1.16 and passed the <a href="https://github.com/cncf/k8s-conformance/pull/879">conformance verification</a></td><td><ul class="params">.<li>TKE now supports creating clusters and managed clusters using Kubernetes 1.16.</li><li>It supports upgrading clusters from Kubernetes 1.14 to 1.16.</li></ul></td><td>2020-02-14</td>
    <td><ul  class="params"><li><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></li><li><a href="https://cloud.tencent.com/document/product/457/32192">Upgrading Clusters</a></li></ul></td>
</table>

## January 2020

<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
    <td>Supports using cluster templates to create clusters</td> <td>This feature offers templates for clusters, managed clusters, and scaling groups and is best suited for use cases such as high availability clusters and GPU clusters. You can use these templates to <b>simplify cluster creation and improve the user experience</b>.</td> <td>2020-01-12</td>
	<td><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></td>
</tr>
</table>

## December 2019

<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
	<td>TKE now supports file and object storage PV and PVC.</td>
    <td>TKE now supports file and object storage PV and PVC, which <b>connects storage resource and Kubernetes</b> and allows users to <b>manage file and object storage using Kubernetes native PVs and PVCs</b>.</td> <td>2019-12-27</td>
	<td>-</td>
</tr>
<tr>
	<td>TKE Kubernetes 1.16 beta is now in beta.</td>
    <td><li>Users can create Kubernetes clusters and managed clusters using the console.</li><li>Users can upgrade clusters from Kubernetes 1.14 to 1.16.</li></td> <td>2019-12-18</td>
	<td><ul class="params"><li><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></li><li><a href="https://cloud.tencent.com/document/product/457/32192">Upgrading Clusters</a></li></ul></td>
</tr>
<tr>
	<td>TKE now supports purchasing multiple data disks and formatting them when initializing a node.</td>
    <td>TKE now supports purchasing multiple data disks and custom formatting when initializing a node. This allows you to <b>isolate data</b> and <b>format disks as needed</b>.</td> <td>2019-12-12</td>
	<td><a href="https://cloud.tencent.com/document/product/457/32203">Adding Nodes</a></td>
</tr>
<tr>
	<td>TKE nodes now supports in-place rolling updates for minor Kubernetes versions.</td>
    <td>In-place rolling updates follow these rules:<li><b>Updates one node at a time.</b> The next node is only updated when the update of the current node is successful.</li><li>In-place update only supports <b>updating to a minor version of the same major version</b>.</li></td> <td>2019-12-03</td>
	<td><a href="https://cloud.tencent.com/document/product/457/32192">Updating Clusters</a></td>
</tr>
</table>


## November 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
	<td>TKE supports custom hostnames for TKE nodes in the beta version.</td>
    <td>With custom hostnames, you can: <i><b>Connect clusters and corporate domain services.</b></li><li><b>Create nodes with specific hostnames quickly in batches</b>.</li></td>
    <td>2019-11-15</td>
	<td><a href="https://cloud.tencent.com/document/product/457/32203">Adding Nodes</a></td>
</tr>
<tr>
	<td>TKE Ingress performance optimization</td>
    <td>TKE Ingress performance optimization does the following:<li><b>Optimizes CLB changes to implement backend binding for aggregated API batch processing.</b></li><li>Optimizes backend queries for CVM to help users <b>avoid unnecessary queries</b>.</li></td>
    <td>2019-11-07</td>
	<td><a href="https://cloud.tencent.com/document/product/457/31711">Basic Ingress Operations</a></td>
</tr>
</table>

## October 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
<td>Cluster worker nodes can now be associated with multiple security groups simultaneously and users can set a default security group</td>
    <td>TKE <b>cluster work nodes can now be associated with multiple security groups</b>. A default security group can also be set to <b>quickly configure a usable security group</b>.</td>
<td>2019-10-22</td>
<td><a href="https://cloud.tencent.com/document/product/457/9084">TKE Security Group Settings</a></td>
</tr>
<td>Node labels can be added in batches during the creation of cluster/nodes</td>
    <td>When creating a cluster or adding new nodes to an existing cluster, TKE allows you to <b>batch add labels to the nodes running the same service or having the same configuration</b>. You can use this feature to divide resources, label them, filter them, and batch process them.</td>
<td>2019-10-21</td>
<td><a href="https://cloud.tencent.com/document/product/457/32185">Managing Clusters</a></td>
</tr>
<tr>
<td>Runtime component containerd now supports the GPU model.</td>
    <td>TKE runtime component containerd now supports GPU models. Users can choose <b>containerd as the runtime component when they create GPU applications</b>.</td>
<td>2019-10-17</td>
<td><a href="https://cloud.tencent.com/document/product/457/35747">How to choose between Containerd and Docker</a></td>
</tr>
<tr>
<td>TKE nodes support Kubernetes rolling reinstall and update in the beta version.</td>
    <td>TKE now supports batch updates of cluster nodes from <b>lower versions to higher versions</b>. This is suitable for <b>clusters using Kubernetes versions that are too old and do not have custom configurations</b>. Custom configurations will no longer take effect after the rolling reinstall or update.</td>
<td>2019-10-15</td>
<td><a href="https://cloud.tencent.com/document/product/457/32192">Updating Clusters</a></td>
</tr>
<tr>
<td>TKE now supports GPU monitoring metrics.</td>
    <td>TKE now supports GPU monitoring metrics, so <b>users can monitor GPU resources</b>. By monitoring these metrics, users can easily locate issues and reduce repair time and maintenance costs while ensuring service stability.</td>
<td>2019-10-15</td>
<td><a href="https://cloud.tencent.com/document/product/457/34183">Monitoring and alert metrics</a></td>
</tr>
</table>

## September 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<td>TKE cluster scaling group API 3.0</td>
    <td>TKE API 3.0 adds <b>support for all regions, improved API documentation, a unified parameter style and public error codes, and SDKs and CLI strictly consistent with the API documentation</b>. This provides a simpler and more convenient experience to users.</td>
<td>2019-09-12</td>
<td><a href="https://cloud.tencent.com/document/api/457/37977">Cluster scaling group APIs</a></td>
<tr>
<td>TKE Kubernetes 1.14 is generally available and has passed the conformance verification.</td>
    <td>TKE<b> Kubernetes 1.14 is now generally available</b> and has passed conformance verification.</td>
<td>2019-09-07</td>
<td><a href="https://github.com/cncf/k8s-conformance/tree/master/v1.14/tencentcloud">Conformance verification</a></td>
</tr>
<tr>
<td>TKE now supports Tencent Cloud Tags and authorization by tag.</td>
    <td>Users can add Tencent Cloud Tags to clusters when they are created. All resources created in the clusters, such as cloud services, cloud disks, and load balancers, automatically inherit the cluster tags. Through these tags, users can quickly and intuitively categorize resources.</td>
<td>2019-09-06</td>
<td>-</td>
</tr>
<tr>
<td>The default instance type for LoadBalancer services is now Cloud Load Balancer.</td>
    <td>The default instance type for LoadBalancer services is now Cloud Load Balancer. <b>The new instance type covers all the capabilities of a traditional load balancer</b>:<li>It supports TCP/UDP/HTTP/HTTPS.</li><li>It provides flexible traffic redirection using domain names and URLs.</li></td>
<td>2019-09-06</td>
<td><a href="https://cloud.tencent.com/document/product/214/8847">A Comparison of Cloud Load Balancers and Traditional Load Balancers</a></td>
</tr>
<tr>
<td>TKE self-deployed clusters now support viewing only Master and Etcd nodes.</td>
    <td>Users can now <b>inspect all Master and Etcd nodes of a self-deployed cluster and their details</b>, allowing users to easily differentiate between nodes and Master nodes, which was a problem in the past.</td>
<td>2019-09-05</td>
<td><a href="https://cloud.tencent.com/document/product/457/32186">Managing Nodes</a></td>
</tr>
</table>


## August 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
<td>
The system automatically assigns security groups to the Master node when creating a self-deployed cluster.</td>
    <td>This feature <b>automatically assigns the appropriate security groups to the Master nodes of self-deployed clusters</b> to prevent Master node communication issues in security groups and improve the success rate of self-deployed cluster creation.</td>
<td>2019-08-27</td>
<td><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></td>
<tr>
<td>Visual TKE cluster creation process</td>
    <td>The visualized TKE cluster creation process <b>gives users a better understanding of wait times and where things go wrong if they do</b>, thus improving the creation success rate and service stability.</td>
<td>2019-08-23</td>
<td><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></td>
</tr>
<tr>
<td>Open-source components <a href="https://github.com/TencentCloud/tencentcloud-cloud-controller-manager">TencentCloud-controller-manager</a> and <a href="https://github.com/TencentCloud/kubernetes-csi-tencentcloud">cbs-csi</a> now support version 1.14.</td>
    <td>The open-source components Tencent Cloud-controller-manager and cbs-csi<b> now support Kubernetes 1.14</b>.</td>
<td>2019-08-12</td>
    <td><a href="https://cloud.tencent.com/document/product/457/18545">Open-source Components</a></td>
</tr>
<tr>
<td>Use existing CLB instances to create Ingress</td>
<td>Users no longer have to create new CLB instances in order to create a new Ingress. They can now use existing CLB instances to avoid addition costs.</td>
<td>2019-08-08</td>
<td><a href="https://cloud.tencent.com/document/product/457/31711">Basic Ingress Operations</a></td>
</tr>
<tr>
<td>TKE Kubernetes 1.14 is now in beta.</td>
    <td>Users can now use the TKE console to create clusters based on <b>Kubernetes 1.14</b>.</td>
<td>2019-08-04</td>
<td>-</td>
</tr>
<tr>
<td>TKE cluster node APIs can access APIs 3.0.
</td>
<td>TKE API 3.0 adds support for all regions, improved API documentation, a unified parameter style and public error codes, and SDKs and CLI strictly consistent with the API documentation. This provides a simpler and more convenient experience to users.</td>
<td>2019-08-04</td>
<td><a href="https://cloud.tencent.com/document/product/457/6787">API 3.0</a></td>
</tr>
<tr>
<td>TKE now supports application-level log collection.</td>
    <td>Users can use application-level logs to <b>inspect application statuses</b> and more accurately locate issues. This reduces the cost and time needed to troubleshoot and maintain service stability.</td>
<td>2019-08-01</td>
<td><a href="https://cloud.tencent.com/document/product/457/36771#.E9.87.87.E9.9B.86.E5.AE.B9.E5.99.A8.E5.86.85.E6.96.87.E4.BB.B6.E6.97.A5.E5.BF.97">Application-level Log Collection</a></td>
</tr>
</table>

## July 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
<tr>
<td>Fixed an issue where CLB health checks failed in IPVS mode.</td>
<td>Fixed a compatibility issue between the Linux kernel and IPVS load balancing, which caused CLB health checks to fail.</td>
<td>2019-07-16</td>
<td>-</td>
<tr>
<td>TKE scaling groups now support spot instances.</td>
    <td>TKE scaling groups now support spot instances. <b>Spot instance can be purchased at a discounted price</b>. However, they can also be repossessed by the system automatically.
</td>
<td>2019-07-10</td>
<td><a href="https://cloud.tencent.com/document/product/213/17816">Spot Instances</a></td>
</tr>
<tr>
<td>TKE now supports Containerd as a runtime component.</td>
    <td>Containerd only <b>runs necessary features to manage image and container lifecycles</b>, which provides a more stable and resource-efficient container runtime environment.
</td>
<td>2019-07-05</td>
<td><a href="https://cloud.tencent.com/document/product/457/35747">How to choose between Containerd and Docker</a></td>
</tr>
</table>

## June 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
<td>TKE support for VPC-CNI is now in beta.</td>
    <td>TKE now supports VPC-CNI extended network mode, which can assign VPC IP addresses to pods. Under VPC-CNI mode, clusters can create StatefulSets with static IP addresses, which do not change with pods restarts and migrations.</td>
<td>2019-06-29</td>
<td><a href="https://cloud.tencent.com/document/product/457/34993">Enabling VPC-CNI Network Mode</a></td>
<tr>
<td>StatefulSet static IP addresses are now in beta.</td>
    <td> StatefulSet static IP addresses solve the problem of IP address changes due to pod restart or migration. Users can use static IP StatefulSet to implement source IP authentication, IP-based process auditing, and log query by pod IP.</td>
<td>2019-06-29</td>
<td><a href="https://cloud.tencent.com/document/product/457/34994">Managing StatefulSets with Static Pod IPs</a></td>
</tr>
<tr>
<td>The new TKE console is now the default choice.</td>
    <td>In order to provide a better product experience, TKE now uses <b>the new Kubernetes-compatible console</b>.</td>
<td>2019-06-17</td>
<td><a href="https://console.cloud.tencent.com/tke2">The New Console</a></td>
</tr>
<tr>
<td>Fixed an issue where cordoning a node while it was being created caused the process to freeze.</td>
<td>Fixed an issue where cordoning a node while it was being created caused the process to freeze.</td>
<td>2019-06-13</td>
    <td><a href="https://github.com/kubernetes/kubernetes/pull/69047">pr69047</a></td>
</tr>
<tr>
<td>Fixed an issue where too many secrets resulted in a pod creation failure.</td>
<td>Fixed an issue where too many secrets resulted in a pod creation failure.</td>
<td>2019-06-13</td>
    <td><a href="https://github.com/kubernetes/kubernetes/pull/74755">pr74755</a></td>
</tr>
<tr>
<td>New console now live on the international site.</td>
    <td>The new console on the international site offers a better native user experience to help users develop, test, and maintain services with ease and efficiency.</td>
<td>2019-06-05</td>
    <td><a href="https://console.cloud.tencent.com/tke2?language=en">International TKE Console</a></td>
</tr>
<tr>
<td>Managed cluster public network access now supports ACL.</td>
<td>Managed clusters with public network access can now use security groups to regulate traffic.</td>
<td>2019-06-05</td>
    <td><a href="https://cloud.tencent.com/document/product/457/9084">TKE Security Group Settings</a></td>
</tr>
</table>

## May 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
<td>Nodes in a scaling group now tolerate drain failures during automatic scaling in.</td>
    <td>When conditions, such as the number of idle nodes, are met, the cluster automatically scales in. However, only when all pods on a node can be successfully scheduled to other nodes are the pods drained and the scaling process completed</b>.</td>
<td>2019-05-20</td>
<td><a href="https://cloud.tencent.com/document/product/457/32190">Cluster Scaling</a></td>
</tr>
<tr>
<td>Supports registering TKE network to CCN</td>
    <td>TKE clusters can now be registered with CCN. CCN then can be used to manage container networks. After the registration, you can use CCN to enable or disable container network routing, allowing resources on container networks and CCN to interconnect.</td>
<td>2019-05-17</td>
<td><a href="https://cloud.tencent.com/document/product/457/35087">Register Container Clusters with CCN</a></td>
</tr>
<tr>
<td>Supports GPU virtualization</td>
<td><ul  class="params"><li>GPU virtualization is now part of the extension components.</li><li>Clusters with GPU nodes and gpu_manager now support extended GPU settings when creating workloads.</li></ul></td>
<td>2019-05-17</td>
    <td><a href="https://cloud.tencent.com/document/product/457/32207">Using GPU Nodes</a></td>
</tr>
</table>


## April 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
<td>Kubelet uses CNI mode by default.</td>
<td>TKE Kubelet defaults to VPC-CNI.</td>
<td>2019-04-24</td>
<td>-</td>
</tr>
<tr>
<td>Docker 18.06 canary release</td>
<td>Docker 18.06 can now be used as a runtime component when creating clusters.</td>
<td>2019-04-22</td>
<td>-</td>
</tr>
<tr>
<td>The new alarm system is now live and available in all regions.</td>
    <td>Alarms can alert users to issues with their TKE service to improve the stability and reliability of their businesses. <b>The new alarm system offers more alarm metrics</b>. We recommend that you configure all production clusters to use alarms.</td>
<td>2019-04-22</td>
<td><a href="https://cloud.tencent.com/document/product/457/34182">Configuring Alarms</a></td>
</tr>
<tr>
<td>Cluster hosting - Kubernetes online updates - Managed Master nodes</td>
    <td>Master and Etcd nodes in managed Kubernetes clusters are manged and maintained by Tencent Cloud professional teams. <b>Kubernetes online update improves service stability</b>.</td>
<td>2019-04-11</td>
    <td><a href="https://cloud.tencent.com/document/product/457/31013">Managed Clusters</a></td>
</tr>
<tr>
<td>Monitoring Master and Etcd nodes in self-deployed clusters</td>
<td>Use the <b>Node Management</b> page to monitor Master and Etcd nodes.</td>
<td>2019-04-11</td>
    <td><a href="https://cloud.tencent.com/document/product/457/34181">Viewing Monitoring Data</a></td>
</tr>
</table>


## March 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
<td>TKE now supports bare metal (BM 2.0) nodes.</td>
<td>BM physical servers is an on-demand purchase and pay-as-you-go physical server rental service that offers high performance and secure clusters for your cloud computing needs.</td>
<td>2019-03-28</td>
<td>-</td>
</tr>
<tr>
<td>Use existing CVM instances to create clusters.</td>
    <td>Use existing CVM instances to create clusters. <b>The helps reduce costs and reuse resources</b>.</td>
<td>2019-03-28</td>
<td><a href="https://cloud.tencent.com/document/product/457/32189#UseExistingCVMCreateCluster">Use Existing CVM Instances to Create Clusters</a></td>
</tr>
<tr>
<td>Cluster Autoscaler (CA) now supports pod shutdown and draining.</td>
<td>When the number of idle pods reaches the limit, scaling is triggered. CA shuts idle pods down and drains them.</td>
<td>2019-03-16</td>
<td><a href="https://cloud.tencent.com/document/product/457/32190">Cluster Scaling</a></td>
</tr>
<tr>
<td>Cluster scaling groups now support GPU node scaling.</td>
    <td>If there is a lack of resource and schedulable pods in the cluster, the auto scaling policy is triggered. You can now <b>add GPU nodes</b> when scaling up the cluster.</td>
<td>2019-03-12</td>
<td><a href="https://cloud.tencent.com/document/product/457/32190">Cluster Scaling</a></td>
</tr>
</table>

## February 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
<td>Releases new monitoring system</td>
    <td>Tencent Cloud’s strong monitoring system is the foundation of our highly reliable, highly available, and high performance service. It enables users to <b>collect different metric data on different resources</b> so they can easily see the state of their resources and quickly resolve issues.</td>
<td>2019-02-18</td>
<td><a href="https://cloud.tencent.com/document/product/457/34180">Monitoring and Alarms Overview</a></td>
</tr>
<tr>
<td>Self-deployed clusters now support Kubernetes 1.12.</td>
    <td>Users can now <b>create Kubernetes 1.12 self-deployed clusters</b> in TKE console.</td>
<td>2019-02-15</td>
<td>-</td>
</tr>
<tr>
<td>Fixes the runC vulnerability CVE-2019-5736</td>
<td>The lightweight container runtime environment runc was shown to have a container escape vulnerability, which allows attackers to overwrite the host runc file (and consequently obtain host root access).</td>
<td>2019-02-13</td>
    <td><a href="https://cloud.tencent.com/announce/detail/457">**Security Alert** Notification on runc container escape vulnerability</a></td>
</tr>
</table>

## January 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
<td>Use existing CLB instances to create Services</td>
<td>Users can use existing CLB instances to create Services to avoid addition resource costs.</td>
<td>2019-01-24</td>
<td><a href="https://cloud.tencent.com/document/product/457/31710">Service Management</a></td>
</tr>
<tr>
<td>Use custom images to create clusters</td>
<td>You can now use the basic images provided by TKE to make custom images and use them to create clusters. To enable this feature, submit a <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1">ticket</a>.</td>
<td>2019-01-24</td>
    <td><a href="https://cloud.tencent.com/document/product/457/39563">Custom Images</a></td>
</tr>
<tr>
<td>Use affinity settings to schedule pods when creating a workload</td>
    <td>Kubernetes issues workload scheduling rules to clusters through YAML and <b>its affinity and anti-affinity mechanism allows pods to be scheduled according to rules</b>.</td>
<td>2019-01-24</td>
<td><a href="https://cloud.tencent.com/document/product/457/32814">Configuring Workload Scheduling Rules</a></td>
</tr>
<tr>
<td>TKE now allows multiple Services to use the same CLB instance.</td>
<td>Multiple Services can now use the same CLB instance in order to avoid additional resource costs.</td>
<td>2019-01-10</td>
<td><a href="https://cloud.tencent.com/document/product/457/31710">Service Management</a></td>
</tr>
</table>

## December 2018
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
	<td>TKE now supports Helm.</td>
        <td>Helm is a Kubernetes application package manager. <b>Tencent Cloud TKE now supports Helm, including Helm Chart, which helps you define, install, and upgrade even the most complex Kubernetes applications</b>.</td>
  <td>2018-12-26</td>
	<td><a href="https://cloud.tencent.com/document/product/457/32730">Helm Application Management</a></td>
	</tr>
	<tr>
	<td>Fixed a Kubernetes permission vulnerability.</td>
	<td>Tencent Cloud Security Center discovered the CVE-2018-1002105 permission vulnerability. Fixing this vulnerability prevented attackers from being able to access Kubernetes cluster resources with authorization, raise their permissions, and send malicious results to compromise system security.</td>
	<td>2018-12-04</td>
        <td><a href="https://cloud.tencent.com/announce/detail/362">**Security Alert** Notification on Kubernetes permission vulnerability</a></td>
	</tr>
	<tr>
	<td>Removed Kubernetes 1.7.8 as an option for creating clusters.</td>
	<td>You can now use the console to submit a <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1">ticket</a> to remove Kubernetes 1.7.8 as an option for creating clusters.</td>
	<td>2018-12-04</td>
        <td>-</td>
	</tr>
	<tr>
	<td>Merged pr71415, which fixed CVE-2018-1002105.</td>
	<td>Fixed CVE-2018-1002105 to handle incorrect responses at the backend.</td>
	<td>2018-12-04</td>
        <td><a href="https://github.com/kubernetes/kubernetes/pull/71415">pr71415</a></td>
	</tr>
	<tr>
	<td>Disabled Kubelet kmem accounting to prevent kernel cgroup leakage.</td>
	<td>Disabled Kubelet kmem accounting to prevent kernel cgroup leakage.</td>
	<td>2018-12-04</td>
	<td>-</td>
	</tr>
</table>

## November 2019
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
	<td>Fixed the kubelet inotify leakage issue.</td>
	<td>The kubelet inotify leakage issue is now fixed.</td>
	<td>2018-11-12</td>
	<td>-</td>
	</tr>
</table>

## October 2018
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
	<td>The new TKE console is now in beta.</td>
        <td>The new console offers a better native user experience and is <b>fully compatible</b> with the old console. Switching to the new console does not affect your service, and you can use it to manage existing clusters.</td>
	<td>2018-10-31</td>
        <td><a href="https://cloud.tencent.com/document/product/457/31699">The New Console</a></td>
	</tr>
	<tr>
	<td>Service can now specify which nodes an CLB instance is bound to.</td>
	<td>When the cluster is large enough, ingress applications are scheduled to certain nodes according to the affinity setting. You can now configure Service to specify which nodes CLB instances are bound to.</td>
	<td>2018-10-31</td>
	<td>-</td>
	</tr>
	<tr>
	<td>Fixed an issue where pod creation failed due to conflicts caused by quota controller updating quota status too frequently.</td>
	<td>Fixed an issue where pod creation failed due to conflicts caused by quota controller updating quota status too frequently.</td>
	<td>2018-10-22</td>
	<td>-</td>
	</tr>
</table>

## September 2018
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>TKE now defaults to Kubernetes 1.10.</td>
		<td>Kubernetes 1.10 is now the default option when creating a cluster. You can choose other versions as needed.</td>
		<td>2018-09-10</td>
        <td><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></td>
	</tr>
	<tr>
		<td>BM clusters now support Kubernetes 1.10.</td>
		<td>TKE now supports BM clusters based on Kubernetes 1.10.</td>
		<td>2018-09-10</td>
		<td>-</td>
	</tr>
	<tr>
		<td>BM clusters now support Ubuntu 16.04.</td>
		<td>TKE now defaults to Ubuntu 16.04 when creating a BM cluster.</td>
		<td>2018-09-10</td>
		<td>-</td>
	</tr>
</table>

## July 2018
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>TKE added two new regions: Russia and India.</td>
		<td>TKE is now available in two new regions. Use the TKE console to switch to Russia or India.</td>
		<td>2018-07-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE cluster Master nodes now support private network access.</td>
		<td>Master nodes now support private network access after the feature is enabled.</td>
		<td>2018-07-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Released the open-source component tencentcloud-cloud-controller-manager.</td>
        <td>tencentcloud-cloud-controller-manager is an implementation of TKE Cloud Controller Manager. It is written for <b>Kubernetes clusters running on Tencent Cloud CM instances</b> and responsible for:<li>updating Kubernetes node addresses.</li><li>routecontroller: creating private network routing for pods.</li><li>servicecontroller: creating CLB instances when a load balancing service is created.</li></td>
		<td>2018-07-30</td>
		<td><a href="https://cloud.tencent.com/document/product/457/18545">Open-source Components</a></td>
	</tr>
	<tr>
		<td>Released the open-source component kubernetes-csi-tencentcloud.</td>
        <td>kubernetes-csi-tencentcloud is a CSI plug-in for Tencent Cloud CBS. <b>It allows Kubernetes clusters running on Tencent Cloud CVM instances to use CBS</b>.</td>
		<td>2018-07-30</td>
		<td><a href="https://cloud.tencent.com/document/product/457/18545">Open-source Components</a></td>
	</tr>
	<tr>
		<td>Released BM cluster ingress plug-in.</td>
		<td>`ingress-tke-bm` is the ingress controller for Tencent Cloud TKE BM clusters. This controller monitors ingress resources, creates BM CLBs, and binds them to the corresponding services.</td>
		<td>2018-07-30</td>
		<td>-</td>
	</tr>
</table>

## June 2018
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>Cloud Container Service (CCS) was renamed Tencent Kubernetes Engine (TKE).</td>
        <td>Tencent Kubernetes Engine (TKE) provides container-centric, highly scalable, and high-performance container management services. It allows you to easily you to easily run applications on managed CVM clusters.
		<td>2018-06-22</td>
        <td><a href="https://tcloud-doc.isd.com/document/product/457/6759">Tencent Kubernetes Engine</a></td>
	</tr>
	<tr>
		<td>Cluster auto scaling now supports custom configurations.</td>
		<td>TKE now lets users configure auto scaling policies according to their needs.</td>
		<td>2018-06-22</td>
		<td><a href="https://tcloud-doc.isd.com/document/product/457/32190">Cluster Scaling</a></td>
	</tr>
	<tr>
		<td>Scripts can be passed when initiating nodes.</td>
        <td><b>This feature allow users to configure a node using custom data</b>. As long as the script can be re-input and has a clear retry pattern, it will be used to configure the node after startup.</td>
		<td>2018-06-22</td>
        <td><a href="https://cloud.tencent.com/document/product/457/32203">Adding Nodes</a></td>
	</tr>
</table>

## May 2018
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>CCS now supports BM clusters.</td>
		<td>BM clusters extend Kubernetes plug-ins, such as BM physical servers and BM load balancers, and offer features, such as highly efficient deployment and resource scheduling to containerized applications. They are best suited for high-performance computing tasks such as gaming and AI.</td>
		<td>2018-05-01</td>
		<td>-</td>
	</tr>
	<tr>
		<td>CCS now supports GPU clusters.</td>
        <td>If you need a cloud platform for <b>deep learning and high-performance computing</b>, CCS GPU clusters is the perfect choice. This function allows you to create and deploy GPU containers quickly and with ease.</td>
		<td>2018-05-01</td>
		<td><a href="https://cloud.tencent.com/document/product/457/32194">Cluster GPU Scheduling</a></td>
	</tr>
</table>

## April 2018
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>CCS now uses the new Tencent Cloud UI.</td>
		<td>The new Tencent Cloud UI is elegant, easy to use, and fast. It offers a better container service experience.</td>
		<td>2018-04-01</td>
        <td><a href="https://console.cloud.tencent.com/tke2">TKE Console</a></td>
	</tr>
	<tr>
		<td>CCS now supports all CVM models.</td>
		<td>When creating a cluster or adding a node, you can now choose from all available CVM models.</td>
		<td>2018-04-01</td>
		<td><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></td>
	</tr>
</table>

## March 2018
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>CCS now supports auto scaling.</td>
        <td>Horizontal Pod Autoscaler (HPA) can automatically scale the number of pods for <b>services according to the average CPU utilization of target pods and other metrics</b>.</td>
		<td>2018-03-01</td>
		<td><a href="https://cloud.tencent.com/document/product/457/37384">Basic Auto Scaling Operations</a></td>
	</tr>
	<tr>
		<td>Improved CCS console</td>
		<td>Adjusted the functional modules of the CCS console.</td>
		<td>2018-03-01</td>
		<td>-</td>
	</tr>
</table>

## February 2018
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>CCS clusters now auto scale.</td>
        <td>Cluster auto scaling <b>adjusts the number of nodes dynamically according to resource demand</b>:<li>If pods become unschedulable due to a lack of resources, the cluster will automatically scale up without any manual intervention.</li><li>If there are enough idle nodes, the cluster will automatically scale down to reduce costs.</li></td>
		<td>2018-02-08</td>
		<td><a href="https://tcloud-doc.isd.com/document/product/457/32190">Cluster Scaling</a></td>
	</tr>
	<tr>
		<td>CCS now supports log collection.</td>
        <td>This feature allows <b>log files from services or specific node paths to be sent to Kafka, Elasticsearch, or CLS</b> so that users can store and analyze them.</td>
		<td>2018-02-06</td>
		<td><a href="https://cloud.tencent.com/document/product/457/36771">Log Collection</a></td>
	</tr>
	<tr>
		<td>New application management feature</td>
		<td>CCS now allows users to manager services like applications. This dramatically reduces the complexity of service management.</td>
		<td>2018-02-06</td>
		<td>-</td>
	</tr>
</table>


## December 2017
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>Use vouchers to purchase cluster nodes</td>
		<td>CCS now supports the use of vouchers to purchase nodes.</td>
		<td>2017-12-20</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Create empty clusters</td>
		<td>This feature allows users to create clusters with no nodes.</td>
		<td>2017-12-20</td>
		<td>-</td>
	</tr>
	<tr>
		<td>You can now set container paths and resource projects for existing nodes</td>
		<td><li>Container path: the container and image storage path. We recommend that you use data disks to store containers and images.</li><li>Resource project: the project to which resources belong. All new resources will be automatically assigned to the project.</li></td>
		<td>2017-12-20</td>
        <td><a href="https://cloud.tencent.com/document/product/457/32203#addExistingNode">Adding Existing Nodes</a></td>
	</tr>
</table>

## November 2017
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>Cluster reservation policy</td>
        <td><b>Reserve resources for system processes such as dockerd and kubelet</b>: through reservation policies, the cluster is able to reserve some resources for processes such as dockerd and kubelet to ensure their smooth operation.</td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Cluster drain policy</td>
        <td><b>Drain pods when the system is about to run out of resources</b>.</td>
		<td>2017-11-30</td>
        <td><a href="https://cloud.tencent.com/document/product/457/32205">Drain or Cordon Pods</a></td>
	</tr>
	<tr>
		<td>Dockerd log rotation</td>
        <td><b>Automatic log rotation ensures there is always enough storage space:</b>: when log files occupy a certain amount of space, automatic log rotation will reclaim some log files to make sure there is enough space for new logs.</td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Ingress forwarding rules now support wildcards.</td>
        <td><b>Ingress forwarding rules should meet the requirements for both public network load balancing domain name rules and Kubernetes Ingress domain name rules</b>:<li>Regular expressions with a length of 1 - 80 characters are supported.</li><li>Non-regular expression domain names can contain the following characters: a-z 0-9 . -.</li><li>Domain names with wildcards currently only support the *.example.com format, and each domain name can only use * once.</li></td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
</table>


## October 2017
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>The new CCS application management feature is now in beta.</td>
        <td>With the popularization of microservices and DevOps, users now faces the challenge of deploying and managing multiple services in multiple environments. <b>CCS now let users group and manage services like applications</b>. This dramatically reduces the complexity of service management.</td>
		<td>2017-10-31</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Image repositories are now available in multiple regions, including Hong Kong, China.</td>
        <td>Image repositories are used to store Docker images, which are used to deploy containers. Each image has a unique identifier (image repository address + image name + image tag). <b>Image repositories are now available in multiple regions, including Hong Kong, China</b>.</td>
		<td>2017-10-31</td>
        <td><a href="https://cloud.tencent.com/document/product/457/9118">Image Repository Overview</a></td>
	</tr>
	<tr>
		<td>CCS goes international</td>
		<td>With the launch of our international site, CCS is now available in English. International users can now use CCS to develop, test, and maintain cluster services.</td>
		<td>2017-10-31</td>
		<td><a href="https://console.cloud.tencent.com/tke2?language=en">International CCS Console</a></td>
	</tr>
</table>

## September 2017
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>Container image repositories now support access permission management.</td>
        <td>Tencent Cloud container images use the following address format:<code>ccr.ccs.tencentyun.com/${namespace}/${name}:${tag}</code>. <b>Image repository permissions involves the following fields</b>:<li>${namespace}: the namespace of the image repository.</li><li>${name}: name of the image repository.</li></td>
		<td>2017-09-26</td>
		<td><a href="https://cloud.tencent.com/document/product/457/11527">CCS Image Repository Resource-level Permission Management</a></td>
	</tr>
	<tr>
		<td>CCS now supports labels.</td>
        <td>CCS now supports service instance labeling. <b>You can use labels to search instances</b>.</td>
		<td>2017-09-26</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Use container configurations as environment variables</td>
		<td>You can use ConfigMap/Secret as environment variables when deploying containers.</td>
		<td>2017-09-26</td>
        <td><a href="https://cloud.tencent.com/document/product/457/31716">Configuration Items</a></td>
	</tr>
	<tr>
		<td>New cluster resource property</td>
        <td><li>Added a new property denotes the project to which a resource belongs. Only resources such as CVM instances and CLB instances, but not clusters, have this property.</li><li>Only new resources are assigned to the project.</li></td>
		<td>2017-09-26</td>
		<td><a href="https://cloud.tencent.com/document/product/457/11185">Project of New Resources</a></td>
	</tr>
	<tr>
		<td>CCS now available in Singapore</td>
		<td>CCS is now available in the Singapore region.</td>
		<td>2017-09-26</td>
        <td><a href="https://console.cloud.tencent.com/tke2">CCS Console</a></td>
	</tr>
</table>

## August 2017
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>Integrated CCS with the alarm platform</td>
        <td>You can now use many metrics to set alarms for clusters. <b>They help you to quickly locate issues and solve them to ensure service stability</b>.</td>
		<td>2017-08-23</td>
		<td><a href="https://cloud.tencent.com/document/product/436/13319">Configuring Alarms</a></td>
	</tr>
	<tr>
		<td>Support for Kubernetes 1.7</td>
        <td><b>CCS now supports using Kubernetes 1.7 to create clusters</b>.</td>
		<td>2017-08-23</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Image repository triggers</td>
        <td>Image repository triggers help users initiate actions such as auto update, webhook push, or notification push. <b>Use these triggers along with continuous integration to implement continuous deployment</b>.</td>
		<td>2017-08-23</td>
		<td><a href="https://cloud.tencent.com/document/product/457/10155">Trigger Overview</a></td>
	</tr>
	<tr>
		<td>Operation logs for image repositories</td>
		<td>Operation logs record actions such as image upload and download to help users troubleshoot problems.</td>
		<td>2017-08-23</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Using kubectl from public networks</td>
        <td>Kubectl is a command line tool for controlling Kubernetes clusters. <b>Now, you can use kubectl from your local client machine to connect to CCS clusters</b>.</td>
		<td>2017-08-04</td>
		<td><a href="https://cloud.tencent.com/document/product/457/32191">Connecting to Clusters</a></td>
	</tr>
	<tr>
		<td>CCS now supports CAM.</td>
        <td>CAM helps users manage resource access permissions under their Tencent Cloud accounts. <b>You can use CAM to create, manage, and terminate users and user groups. It allows you to manage your resources using identity and policy management</b>.</td>
		<td>2017-08-04</td>
        <td><a href="https://cloud.tencent.com/document/product/457/11528">CCS Resource-level Permission API List</a></td>
	</tr>
</table>


## July 2017
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>CCS supports configuration file management.</td>
        <td><li>Configuration file management helps you manage how different services running in different environments are configured. This feature supports multiple versions of configuration files in YAML.</li><li>Configuration files are versioned so you can easily update or rollback applications.</li><li>It also allows you to import your container configurations using files.</li></td>
		<td>2017-07-19</td>
		<td>-</td>
	</tr>
	<tr>
		<td>CCS now supports CI code builds.</td>
        <td>Tencent Cloud platforms offers continuous integration. You can build container images <b>manually or automatically</b>.</td>
		<td>2017-07-18</td>
		<td><a href="https://cloud.tencent.com/document/product/213/4940">Image Building Overview</a></td>
	</tr>
	<tr>
		<td>Added My Favorites to image repositories</td>
		<td>Use My Favorites to find all bookmarked images. This feature helps users to quickly find and use images they bookmark.</td>
		<td>2017-07-18</td>
        <td><a href="https://cloud.tencent.com/document/product/457/9118">Image Repository Overview</a></td>
	</tr>
	<tr>
		<td>Image repositories now support multiple namespaces.</td>
        <td><b>Image repositories now support multiple namespaces. <b>Each namespace is unique in the system</b>. If the name of the namespace you wish to use is already taken, try something else.</td>
		<td>2017-07-18</td>
		<td><a href="https://cloud.tencent.com/document/product/457/9117#.E5.88.9B.E5.BB.BA.E5.91.BD.E5.90.8D.E7.A9.BA.E9.97.B4">Creating a Namespace</a></td>
	</tr>
</table>

## June 2017
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>CCS now supports NFS volumes.</td>
		<td>NFS volumes are suitable for read-many write-many persistent storage and big data analysis, media processing, and content management.</td>
		<td>2017-06-24</td>
		<td><a href="https://cloud.tencent.com/document/product/457/31713">Volume Management</a></td>
	</tr>
	<tr>
		<td>CCS now supports privileged containers and working directory configuration.</td>
        <td><li>Privileged containers have higher priority.</li><li>WorkingDir: the current working directory. If the specified directory does not exist, it is created. If it is not specified, the default value is used. If the image does not specify a WorkingDir and the console does not specify one either, the default `/` is used.</li></td>
		<td>2017-06-24</td>
		<td>-</td>
	</tr>
	<tr>
		<td>CCS now supports cluster namespaces.</td>
		<td>A cluster is the collective of cloud resources for running containers, including Tencent Cloud resources such as CVM instances and CLB instances. You can run containerized applications in a cluster.</td>
		<td>2017-06-07</td>
		<td><a href="https://cloud.tencent.com/document/product/457/32187">Cluster Overview</a></td>
	</tr>
	<tr>
		<td>Automatically format data disks and assign a container directory when creating clusters or adding CVM instances</td>
		<td>For CVM instances with data disks or small system disks, you need to format the data disks and assigned a directory for storing containers and images.</td>
		<td>2017-06-07</td>
        <td><li><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></li><li><a href="https://cloud.tencent.com/document/product/457/32203">Adding Nodes</a></li></td>
	</tr>
	<tr>
		<td>CCS now supports service redeployment</td>
		<td>Redeployment means deploying all containers and pulling images again.</td>
		<td>2017-06-07</td>
        <td><li><a href="https://cloud.tencent.com/document/product/457/31710">Service Management</a></li><li><a href="https://cloud.tencent.com/document/product/457/3171">Basic Ingress Operations</a></li></td>
	</tr>
</table>

## April 2017
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>CCS now supports adding existing CVM instances to a cluster.</td>
		<td>Adding existing CVM instances to a cluster helps with resources reuse and cost reduction.</td>
        <td>2017-04-27</td>
		<td><a href="https://cloud.tencent.com/document/product/457/32203#.E6.B7.BB.E5.8A.A0.E5.B7.B2.E6.9C.89.E8.8A.82.E7.82.B9">Adding Existing Nodes</a></td>
	</tr>
	<tr>
		<td>CCS now supports monitoring metrics for instances, services, and clusters.</td>
		<td>A healthy monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud Cloud Container Service (CCS). You can collect monitoring data of different dimensions for different resources, making it easy to understand each resource’s usage information and locate errors quickly.</td>
        <td>2017-04-27</td>
		<td><a href="https://cloud.tencent.com/document/product/457/34180">Monitoring and Alarms Overview</a></td>
	</tr>
	<tr>
		<td>CCS now supports container logs</td>
		<td>Using new log collection rules, CCS can provide internal logs to cluster users to help them maintain services and troubleshoot issues.</td>
        <td>2017-04-27</td>
		<td><a href="https://cloud.tencent.com/document/product/457/36771">Log Collection</a></td>
	</tr>
	<tr>
		<td>Upload and download files remotely using the CCS web interface</td>
		<td><ul class="params"><li>Upload specified files.</li><li>Download specified files.</li></ul></td>
        <td>2017-04-19</td>
		<td><a href="https://cloud.tencent.com/document/product/457/9120">Basic Remote Terminal Operations</a></td>
	</tr>
	<tr>
		<td>CCS now supports custom security groups when creating clusters.</td>
        <td>If the default security group does not meet your needs, refer to <a href="https://cloud.tencent.com/document/product/213/39739">Managing Security Groups</a> for details on how to use a custom security group.</td>
        <td>2017-04-19</td>
        <td><a href="https://cloud.tencent.com/document/product/457/32189">Creating Clusters</a></td>
	</tr>
</table>

## March 2017
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>CCS now supports remote login using the web terminal.</td>
        <td>The remote terminal can help users debug their containers quickly and connect to the containers for troubleshooting. It supports file copy/paste and file upload/download. The web terminal solves the problem of long container login paths and reduces the difficulty in debugging</b>.</td>
        <td>2017-03-15</td>
		<td><a href="https://cloud.tencent.com/document/product/457/9120">Basic Remote Terminal Operations</a></td>
	</tr>
	<tr>
		<td>CCS now supports third-party image creation.</td>
        <td>Third-party image creation <b>help users deploy services according to their actual needs</b>.</td>
        <td>2017-03-15</td>
		<td>-</td>
	</tr>
	<tr>
		<td>CCS now supports application-layer load balancing.</td>
        <td>An Ingress is a collection of rules that allows access to services within a cluster. You can configure different forwarding rules to allow different URLs to access different services.</td>
        <td>2017-03-06</td>
		<td><a href="https://cloud.tencent.com/document/product/457/40537">Ingress Management</a></td>
	</tr>
	<tr>
		<td>Inspect cluster, service, and instance monitoring information</td>
        <td>A healthy monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud Cloud Container Service (CCS). <b>You can collect monitoring data of different dimensions for different resources, making it easy to understand each resource’s usage information and locate errors quickly</b></td>.
        <td>2017-03-06</td>
		<td><a href="https://cloud.tencent.com/document/product/457/34180">Monitoring and Alarms Overview</a></td>
	</tr>
	<tr>
		<td>Support provided for native Kubernetes APIs. Tencent Cloud APIs can be used to request Kubernetes certificates and all native functionalities.</td>
        <td>CCS is ideal for cluster creation and maintenance. It seamlessly integrates with Tencent Cloud for computing power, storage capacity, network connection, monitoring, and security capabilities. <b>Refer to the API documentation for details on how to add/delete/modify scaling groups, networks, nodes, and clusters</b>.</td>
        <td>2017-03-06</td>
		<td><a href="https://cloud.tencent.com/document/product/457/31853">API Overview</a></td>
	</tr>
</table>

## December 2016
<table>
	<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
	<tr>
		<td>Cluster Management</td>
		<td>Add/delete/modify/query clusters, VPC container clusters, cross-availability-zone clusters, and native Kubernetes API support</td>
        <td>2016-12-26</td>
        <td><a href="https://cloud.tencent.com/document/product/457/32185">Cluster Management</a></td>
	</tr>
	<tr>
		<td>Service Management</td>
		<td>Service management includes adding/deleting/modifying/querying services, private image creation, official Docker image creation, and cross-availability-zone service scheduling.</td>
        <td>2016-12-26</td>
		<td><a href="https://cloud.tencent.com/document/product/457/32185">Service Management</a></td>
	</tr>
	<tr>
		<td>Image Management</td>
		<td>Official Docker images, my images, uploading/downloading private images, and official Docker image acceleration.</td>
        <td>2016-12-26</td>
        <td><a href="https://cloud.tencent.com/document/product/457/9103">Image Repositories</a></td>
	</tr>
	<tr>
		<td>Cluster and Container Monitoring</td>
		<td>CCS monitors all clusters by default.</td>
        <td>2016-12-26</td>
        <td><a href="https://cloud.tencent.com/document/product/457/34181">View Monitoring Data</a></td>
	</tr>
	<tr>
		<td>Service Creation, Events Update, and Service Rolling Update</td>
		<td>The rolling update function updates instances one by one, without interruption to you service.</td>
        <td>2016-12-26</td>
		<td>-</td>
	</tr>
</table> 

<style>
	.params{margin-bottom:0px !important;} 
</style>
