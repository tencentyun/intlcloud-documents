## April 2020
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
	<td>TKE removes Kubernetes 1.8 as an option</td><td>TKE no longer supports creating clusters using Kubernetes 1.8.</td><td>2020-04-03</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating Clusters</a></td>
</tr>
<tr>
	<td>Self-deployed cluster master update</td><td>You can now use the TKE console to perform rolling updates of Kubernetes masters on self-deployed clusters.</td><td>2020-04-02</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Updating Clusters</a></td>
</tr>
</table>

## March 2020
<table>
<tr><th style="width:20%">Updates</th><th style="width:50%">Details</th> 
<th style="width:15%">Date</th><th style="width:15%">Documentation</th> </tr>
<tr>
	<td>TKE now supports both GlobalRouter and VPC-CNI network modes</td>
	<td>TKE now supports GlobalRouter and VPC-CNI network modes for your business needs. Choose the one that fits your requirements.</td>
	<td>2020-03-30</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/35248">How to choose TKE Network Mode</a></td>
</tr>
<tr>
    <td>TKE Edge is now live</td> <td>TKE Edge is a centralized container system that manages edge cloud resources. You can use it to manage distributed nodes in the same cluster across multiple regions. TKE Edge is fully compatible with Kubernetes, supports one-click delivery, and provides edge autonomy, and distributed health checks.</td><td>2020-03-25</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/35390">TKE Edge</a></td>
</tr>
<tr>
    <td>Supports enabling "Local Disk Formatting" for BM and big data models</td> <td>TKE now allows you to enable "Local Disk Formatting" for BM and big data model nodes, and also allows mounting and setting container directories.</td><td>2020-03-02</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating Clusters</a></td>
</tr>
</table>

## February 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
    <td>TKE cluster scaling groups support the shutdown of scaled-down nodes.</td> <td>During scale-down of a cluster scaling group, <b>the scaled-down nodes can be shut down instead of draining or termination.</b> To enable this feature, submit a <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1">ticket</a> for application.</td> <td>2020-02-17</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
<tr>
    <td>TKE fully launched Kubernetes 1.16 and passed <a href="https://github.com/cncf/k8s-conformance/pull/879">conformance verification.</a></td><td><ul class="params"><li>Users can create self-deployed clusters and managed clusters of the Kubernetes 1.16 version.</li><li>Users can update a cluster from Kubernetes 1.14 to 1.16.</li></ul></td><td>2020-02-14</td>
    <td><ul  class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30640">Updating a Cluster</a></li></ul></td>
</table>

## January 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
    <td>TKE allows users to create clusters using a cluster template.</td> <td>The template-based cluster creation feature provides multiple templates for creating managed clusters, self-deployed clusters, and elastic clusters, <b>simplifying the current cluster creation process and improving the cluster creation experience</b>. It applies to various business scenarios such as HA clusters and GPU clusters.</td> <td>2020-01-12</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
</table>

## December 2019

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<td>Elastic Kubernetes Service (EKS) beta was launched. </td><td>EKS <b>allows users to deploy workloads without having to purchase nodes</b>. <b>It’s fully compatible with native Kubernetes</b> and supports resource purchase and management in native mode. Resources are billed based on the resource amount used by containers.</td> <td>2019-12-27</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/34040">EKS</a></td>
</tr>
<tr>
	<td>TKE supports PVs and PVCs of the Cloud File Storage (CFS) and Cloud Object Storage (COS) types.</td>
    <td>TKE supports PVCs and PVs of the CFS and COS types, <b>connecting storage resources with Kubernetes</b>. TKE makes it convenient for users to use basic Tencent Cloud products through the native Kubernetes mode and allows users to <b>manage file storage and object storage via PVs and PVCs</b>.</td> <td>2019-12-27</td>
	<td>-</td>
</tr>
<tr>
	<td>TKE Kubernetes 1.16 beta was launched.</td>
    <td><li>This allows users to create Kubernetes 1.16 self-deployed clusters and managed clusters via the console.</li><li>It allows users to upgrade the Kubernetes version of a cluster from 1.14 to 1.16.</li></td> <td>2019-12-18</td>
	<td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30640">Updating a Cluster</a></li></ul></td>
</tr>
<tr>
	<td>TKE supports the purchase of multiple data disks during node initialization as well as custom formatting.</td>
    <td>TKE allows users to purchase multiple data disks during node initialization and supports custom data disk formatting that allows users to isolate <b>data</b> and <b>format settings flexibly based on actual requirements</b>.</td> <td>2019-12-12</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding Nodes</a></td>
</tr>
<tr>
	<td>TKE nodes support the in-place rolling update of minor Kubernetes versions.</td>
    <td>Nodes in in-place updates support the rolling update mode. <li><b>Only one node is updated at a time, and </b>the next node is updated only after the current node is successfully updated. </li><li>Currently, in-place update only supports the <b>update of different minor versions of the same major version</b>.</li></td> <td>2019-12-03</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Updating a Cluster</a></td>
</tr>
</table>


## November 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
	<td>The beta custom Hostname supported by TKE was launched.</td>
    <td>The TKE custom Hostname feature provides the following advantages: <li><b>Helps clusters interwork with enterprises’ internal domain name service systems.</b></li><li><b>Makes it easier for users to quickly create nodes with a specified Hostname in batches</b>.</li></td>
    <td>2019-11-15</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding Nodes</a></td>
</tr>
<tr>
	<td>TKE Ingress performance optimization was released.</td>
    <td>TKE Ingress performance is optimized to better serve users. <li>CLB changes are optimized to <b>allow for batch calling APIs to process backend binding.</b></li><li>CVM backend query is optimized to help users <b>avoid unnecessary repeated queries</b>.</li></td>
    <td>2019-11-07</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30673">Ingress Management</a></td>
</tr>
</table>

## October 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<td>Cluster worker nodes can configure several security groups simultaneously and use the default security group.</td>
    <td>TKE allows <b>a cluster worker nodes to bind multiple security groups</b> and provides a default security group. In this way, users can <b>quickly configure available security groups</b>.</td>
<td>2019-10-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/9084">TKE Security Group Settings</a></td>
</tr>
<td>Node labels can be added in batches during cluster or node creation.</td>
    <td>When a cluster is created or new nodes are added to an existing cluster, TKE allows users to <b>add labels for nodes that run the same business or have the same configuration</b>. The labels help users divide resources, label resource attributes, and filter and batch process massive resource volumes.</td>
<td>2019-10-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30635">Cluster Management</a></td>
</tr>
<tr>
<td>Runtime component Containerd supports the GPU model.</td>
    <td>The TKE runtime component Containerd supports the GPU model. When users need to <b>create a GPU application in a cluster, they can choose Containerd as the runtime component</b>.</td>
<td>2019-10-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/31088">How to Choose Containerd and Docker</a></td>
</tr>
<tr>
<td>The beta for rolling Kubernetes reinstallation and upgrade of TKE nodes was launched.</td>
    <td>TKE supports the batch update of nodes <b>in a cluster from an earlier version to a later version</b>. This feature applies to clusters whose <b>Kubernetes version is outdated and clusters whose nodes do not have relevant custom configurations</b>. Custom configurations will become invalid after the rolling reinstallation and upgrade of nodes.</td>
<td>2019-10-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Updating a Cluster</a></td>
</tr>
<tr>
<td>TKE supports GPU monitoring metrics.</td>
    <td>TKE supports GPU monitoring metrics, <b>enabling users to monitor GPU-related resources</b>. By checking monitoring data, users can precisely identify specific problems, shorten troubleshooting time, and reduce OPS costs, ensuring continuous and stable business operation.</td>
<td>2019-10-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30691">List of Monitoring and Alarm Metrics</a></td>
</tr>
</table>

## September 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<td>Related APIs of the TKE cluster scaling group have been updated to API 3.0.</td>
    <td>TKE APIs have been updated to 3.0 and support all-region access. <b>The new API documentation is more standardized and comprehensive, with unified parameter styles and common error codes. The SDK/CLI version is consistent with that in the API documentation</b>, providing a simple and convenient use experience.</td>
<td>2019-09-12</td>
<td>Related APIs of the Scaling Group</td>
<tr>
<td>TKE Kubernetes 1.14 was fully launched and has passed conformance verification.</td>
    <td>TKE <b>Kubernetes 1.14 was fully launched</b> and has passed conformance verification to ensure that the latest Kubernetes version is available.</td>
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
<td><a href="https://intl.cloud.tencent.com/document/product/214/8847">CLB and Traditional Load Balancer Instance Comparison</a></td>
</tr>
<tr>
<td>TKE self-deployed clusters support separate viewing of Master and Etcd nodes.</td>
    <td>This feature allows users to <b>intuitively view the list of all Master and Etcd nodes of a self-deployed cluster and the details of such nodes</b>. Users no longer have trouble distinguishing Master and Etcd nodes in self-deployed clusters.</td>
<td>2019-09-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30650">Node Overview</a></td>
</tr>
</table>


## August 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<td>
When a “self-deployed cluster” is created, a security group is automatically bound to the Master node.</td>
    <td>This feature can <b>automatically bind an applicable security group to the Master node in a self-deployed cluster</b>. This prevents the Master node from being associated with a security group with communication problems and improves the success rate of creating self-deployed clusters.</td>
<td>2019-08-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
<tr>
<td>TKE supports the visualized display of the cluster creation progress.</td>
    <td>The visualized display of the cluster creation progress <b>enables users to see the waiting time for cluster creation and the steps with exceptions</b>. This improves the success rate of cluster creation and ensures the continuous, stable running of businesses.</td>
<td>2019-08-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
<tr>
<td>Open source components: <a href="https://github.com/TencentCloud/tencentcloud-cloud-controller-manager">TencentCloud-controller-manager</a> and <a href="https://github.com/TencentCloud/kubernetes-csi-tencentcloud">cbs-csi</a> support Kubernetes 1.14.</td>
    <td>The open source components Tencent Cloud-controller-manager and cbs-csi<b> support Kubernetes 1.14</b>.</td>
<td>2019-08-12</td>
    <td>Open Source Components</td>
</tr>
<tr>
<td>Ingress supports existing CLBs.</td>
<td>TKE allows users to use existing CLBs to create Ingress. Users do not need to create a CLB when an applicable CLB is available. This helps users reduce costs.</td>
<td>2019-08-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30673">Ingress Management</a></td>
</tr>
<tr>
<td>TKE Kubernetes 1.14 beta was launched.</td>
    <td>Users can <b>create Kubernetes 1.14 clusters in the TKE console</b>.</td>
<td>2019-08-04</td>
<td>-</td>
</tr>
<tr>
<td>Related APIs of TKE cluster nodes have been updated to API 3.0.
</td>
<td>TKE APIs have been updated to 3.0 and support all-region access. The new API documentation is more standardized and comprehensive, with unified parameter styles and common error codes. The SDK/CLI version is consistent with that in the API documentation, providing a simple and convenient use experience.</td>
<td>2019-08-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/6787">API 3.0</a></td>
</tr>
<tr>
<td>TKE supports the collection of file logs in the container.</td>
    <td>By checking the collected file logs in the container, <b>users can view the running status of applications in the container</b>, precisely identify specific problems, shorten the troubleshooting time, and reduce OPS costs to ensure continuous and stable business operations.</td>
<td>2019-08-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/32419">Log Collection</a></td>
</tr>
</table>

## July 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<tr>
<td>The CLB health check failure issue in IPVS mode was fixed.</td>
<td>The linux kernel version and IPVS compatibility issue was resolved, and the CLB health check failure issue in IPVS mode was fixed.</td>
<td>2019-07-16</td>
<td>-</td>
<tr>
<td>TKE scaling groups support spot models.</td>
    <td>When TKE creates a scaling group, users can choose spot instances <b>and purchase pods at a certain discount</b>. However, the system may automatically recall these pods sold at a discount.
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
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<td>The beta VPC-CNI network mode was launched.</td>
    <td>TKE provides the VPC-CNI extended network mode, which <b>can assign intra-VPC IP addresses to Pods in a cluster</b>. In the VPC-CNI mode, clusters can create StatefulSet that supports fixed IP address types, and the Pod IP addresses will not change with restart or migration.</td>
<td>2019-06-29</td>
<td>VPC-CNI Mode Networks for Clusters</td>
<tr>
<td>The beta StatefulSet with fixed IP addresses was launched.</td>
    <td> The StatefulSet fixed IP addresses help <b>resolve IP address change issues due to Pod restart or migration</b>. Users can create StatefulSet with fixed IP addresses for source IP address authorization, IP-based process review, log query based on Pod IP addresses, and other business requirements to ensure continuous and stable business operations.</td>
<td>2019-06-29</td>
<td>Management of StatefulSet of Fixed Pod IP Addresses</td>
</tr>
<tr>
<td>TKE uses the new console version by default.</td>
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
<td>The new version of the TKE International console was launched.</td>
    <td>The new version of TKE International console adjusts a series of functional modules and <b>provides a native, easier-to-use platform</b>, which helps users resolve environmental issues in development, testing, and OPS, reduce costs, and improve efficiency.</td>
<td>2019-06-05</td>
    <td><a href="https://console.cloud.tencent.com/tke2?language=en">CCS International Console</a></td>
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
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<td>Nodes in a scaling group tolerate drain failures during automatic scaling in.</td>
    <td>When scale-in conditions, such as the number of idle nodes, are met, the cluster automatically scales in. <b>However, only when all pods of a node are successfully scheduled to other nodes, the pods can be drained successfully and scale-in is successful</b>.</td>
<td>2019-05-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
<tr>
<td>TKE container networks can now be registered with CCN.</td>
    <td>TKE allows users to <b>register existing clusters to CCN, and CCN can manage the container’s network</b>. After the container’s network is registered, you can enable or disable its IP range routing on the CCN side to achieve interconnection between the container’s cluster and resources in CCN.</td>
<td>2019-05-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/34021">Register Container Clusters with CCN</a></td>
</tr>
<tr>
<td>TKE supports GPU virtualization.</td>
<td><ul  class="params"><li>Extension components support installation and deployment of GPU visualization components.</li><li>Clusters that have deployed GPU nodes and gpu_manager can extend GPU-related settings during workload creation.</li></ul></td>
<td>2019-05-17</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/30656">Using a GPU Node</a></td>
</tr>
</table>


## April 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<td>Kubelet uses the CNI mode by default.</td>
<td>TKE Kubelet uses the VPC-CNI network mode by default.</td>
<td>2019-04-24</td>
<td>-</td>
</tr>
<tr>
<td>Docker 18.06 was launched in the phased manner.</td>
<td>Runtime components that use Docker 18.06 can create clusters.</td>
<td>2019-04-22</td>
<td>-</td>
</tr>
<tr>
<td>The new alarm version was launched and supports all regions.</td>
    <td>Alarms enable users to discover exceptions in TKE in a timely manner to ensure business stability and reliability. <b>The new alarm version provides more alarm metrics</b>. We recommend that you configure necessary alarms for all production clusters.</td>
<td>2019-04-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30690">Setting Alarms</a></td>
</tr>
<tr>
<td>Cluster management - Kubernetes online update - Managed master nodes</td>
    <td>In managed cluster mode, the Master and Etcd nodes of your Kubernetes cluster will be centrally managed and maintained by the Tencent Cloud technical team. <b>Online update of the Kubernetes version ensures business stability</b>.</td>
<td>2019-04-11</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/31417">Introduction to Cluster Hosting Modes</a></td>
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
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<td>TKE supports Bare Metal (BM 2.0) nodes.</td>
<td>BM physical servers are a type of on-demand pay-as-you-go physical server rental service that provide high-performance and securely isolated physical server clusters for cloud users.</td>
<td>2019-03-28</td>
<td>-</td>
</tr>
<tr>
<td>Users can use a purchased CVM to create clusters.</td>
    <td>Using existing CVMs to create clusters helps users <b>reuse existing resources and reduce costs</b>.</td>
<td>2019-03-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30637#UseExistingCVMCreateCluster">Creating a Cluster Using Existing CVMs</a></td>
</tr>
<tr>
<td>Cluster auto-scaling (CA) supports disabling pod draining.</td>
<td>When there are multiple idle nodes in a cluster, scale-in will be triggered. CA supports disabling pod draining.</td>
<td>2019-03-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
<tr>
<td>Cluster scaling groups support scale-out of GPU nodes.</td>
    <td>When a pod in a cluster cannot be scheduled due to a lack of resources in the cluster, the previously set auto scale-out policy will be triggered. During scaling out, <b>GPU nodes can be added</b>.</td>
<td>2019-03-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
</table>

## February 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<td>A new monitoring system was released.</td>
    <td>A good monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud TKE. <b>You can collect monitoring data in different dimensions for different resources</b> to quickly master resource usage and easily locate errors.</td>
<td>2019-02-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
</tr>
<tr>
<td>Self-deployed clusters support Kubernetes 1.12.</td>
    <td>Users can <b>create self-deployed clusters with Kubernetes 1.12 in the TKE console</b>.</td>
<td>2019-02-15</td>
<td>-</td>
</tr>
<tr>
<td>runC vulnerability CVE-2019-5736 was fixed.</td>
<td>The lightweight container runtime environment runc was shown to have a container escape vulnerability, which allows attackers to overwrite the host runc file (and consequently obtain host root access).</td>
<td>2019-02-13</td>
    <td>[WARNING] runC Container Escape Vulnerability</td>
</tr>
</table>

## January 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
<tr>
<td>Existing CLBs can be used to create Service.</td>
<td>Using existing CLBs to create Service can save resources and help users reduce costs.</td>
<td>2019-01-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30672">Service Management</a></td>
</tr>
<tr>
<td>Custom images can be used to create clusters.</td>
<td>TKE allows users to create custom images based on the basic image provided by TKE and use these custom images to create clusters. To enable this feature, submit a <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1">ticket</a> to apply.</td>
<td>2019-01-24</td>
    <td>Custom Image Description</td>
</tr>
<tr>
<td>Affinity scheduling can be set during workload creation.</td>
    <td>YAML is delivered to the Kubernetes cluster to schedule pods in a workload. <b>The affinity and anti-affinity mechanism of Kubernetes ensure that Pods are scheduled according to a specific rule</b>.</td>
<td>2019-01-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30668">Setting the Scheduling Rule for a Workload</a></td>
</tr>
<tr>
<td>TKE allows multiple Services to use the same CLB instance.</td>
<td>Multiple Services can now use the same CLB instance in order to avoid additional resource costs.</td>
<td>2019-01-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30672">Service Management</a></td>
</tr>
</table>

## December 2018
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
	<td>TencentHub supports Helm Chart management.</td>
	<td>Helm is a package management tool of Kubernetes. Chart is a collection of files describing Kubernetes resources. Tencent Hub provides an address for users to store Helm Chart.</td>
	<td>2018-12-26</td>
	<td>Helm Chart Introduction</td>
	</tr>
	<tr>
	<td>TKE supports Helm application installation.</td>
        <td>Helm is a packaging tool for managing Kubernetes applications. <b>TKE has integrated Helm-related features to visually add, delete, modify, and query Helm Charts in a specified cluster.</b></td>
  <td>2018-12-26</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30683">Helm Application Management</a></td>
	</tr>
	<tr>
	<td>The privilege escalation vulnerability in Kubernetes was fixed.</td>
	<td>Tencent Cloud Security Center detected that a severe privilege escalation vulnerability existed in Kubernetes (vulnerability ID: CVE-2018-1002105). This vulnerability has been fixed. Now, TKE can effectively prevent attackers from using the vulnerability to access unauthorized Kubernetes cluster resources and initiating malicious requests that can ultimately jeopardize the business system security.</td>
	<td>2018-12-04</td>
        <td>[WARNING] Privilege Escalation Vulnerability in Kubernetes</td>
	</tr>
	<tr>
	<td>Removed Kubernetes 1.7.8 as an option for creating clusters.</td>
	<td>Users can disable the entry for creating clusters of Kubernetes 1.7.8 in the console. To enable this feature, submit a <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1">ticket</a> to apply.</td>
	<td>2018-12-04</td>
        <td>-</td>
	</tr>
	<tr>
	<td>pr71415 was merged to fix CVE-2018-1002105.</td>
	<td>CVE-2018-1002105 was fixed, and backend error responses are processed.</td>
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
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
	<td>The kubelet inotify leakage issue was fixed.</td>
	<td>The kubelet inotify leakage problem was fixed.</td>
	<td>2018-11-12</td>
	<td>-</td>
	</tr>
</table>

## October 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
	<td>The beta TKE console was launched.</td>
        <td>The new TKE console adjusts a series of functional modules to<b> provide you with a native and easier-to-use platform</b>. <b>The new and old consoles are fully compatible in terms of features</b>. Switching consoles will not affect your business. You can use the new console to continue to operate existing clusters.</td>
	<td>2018-10-31</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30633">Notes on the New Console</a></td>
	</tr>
	<tr>
	<td>Service CLB can be bound to specified nodes.</td>
	<td>If your cluster is large, you will need to set affinity for entry-type applications to schedule them to certain nodes. You can configure the Service CLB to be bound only to specified nodes.</td>
	<td>2018-10-31</td>
	<td>-</td>
	</tr>
	<tr>
	<td>Conflicts and Pod creation failures caused by the frequent update of quota statuses by the quota controller are resolved.</td>
	<td>Previously, if the quota controller frequently updated the quota status, conflicts and even Pod creation failures would occur. This problem has been resolved.</td>
	<td>2018-10-22</td>
	<td>-</td>
	</tr>
</table>

## September 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>The default Kubernetes version in TKE is 1.10.</td>
		<td>When a new cluster is created, the default Kubernetes version is 1.10. You can change it based on actual requirements.</td>
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
		<td>When TKE creates a BM cluster, the default operating system chosen is Ubuntu 16.04.</td>
		<td>2018-09-10</td>
		<td>-</td>
	</tr>
</table>

## July 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>TKE supports the regions of Russia and India.</td>
		<td>The TKE console supports the regions of Russia and India. You can go to the console and switch to these regions.</td>
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
		<td>The open source component tencentcloud-cloud-controller-manager was released.</td>
        <td>This component is the Cloud Controller Manager implementation for TKE, <b>allowing the following features to be implemented on Kubernetes clusters built by Tencent Cloud CVMs</b>:<li>Updates relevant addresses information of Kubernetes nodes.</li><li>routecontroller: creates routes within pod IP ranges in a VPC. </li><li>servicecontroller: creates a corresponding CLB when a load balancer-type service is created in a cluster.</li></td>
		<td>2018-07-30</td>
		<td>Open Source Components</td>
	</tr>
	<tr>
		<td>The open source component kubernetes-csi-tencentcloud was released.</td>
        <td>This component is a plug-in for the Tencent Cloud CBS service, which complies with CSI standards. <b>It allows users to use CBS on Kubernetes clusters built by Tencent Cloud CVMs</b>.</td>
		<td>2018-07-30</td>
		<td>Open Source Components</td>
	</tr>
	<tr>
		<td>The BM cluster ingress plug-in was released.</td>
		<td>ingress-tke-bm is the ingress controller for Tencent Cloud TKE BM clusters. This controller monitors ingress resources, creates BM CLBs, and binds them to the corresponding services.</td>
		<td>2018-07-30</td>
		<td>-</td>
	</tr>
</table>

## June 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS was renamed TKE.</td>
        <td><b>Tencent Kubernetes Engine (TKE) </b>is a highly scalable and high-performance container management service. It allows you to easily run applications on a managed CVM instance cluster.</td>
		<td>2018-06-22</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/6759">TKE</a></td>
	</tr>
	<tr>
		<td>Cluster autoscaling supports custom configurations.</td>
		<td>CCS allows users to customize cluster scaling settings based on their actual requirements, making it easier for them to configure businesses flexibly.</td>
		<td>2018-06-22</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
	</tr>
	<tr>
		<td>Node initialization supports the import of scripts.</td>
        <td><b>This feature allow users to configure a node using custom data</b>. As long as the script can be re-input and has a clear retry pattern, it will be used to configure the node after startup.</td>
		<td>2018-06-22</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding Nodes</a></td>
	</tr>
</table>

## May 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS supports BM clusters.</td>
		<td>BM container clusters extend Tencent Cloud’s CPM, BM Load Balancer, and other Kubernetes plug-ins, providing a series of complete features such as high-efficient deployment and resource scheduling for containerized applications. This helps industries such as gaming and AI easily cope with the challenges of high-performance computing business scenarios.</td>
		<td>2018-05-01</td>
		<td>-</td>
	</tr>
	<tr>
		<td>CCS supports GPU clusters.</td>
        <td>If your business <b>involves scenarios such as deep learning and high-performance computing</b>, you can use the GPU feature supported by CCS, which can help you quickly use a GPU container.</td>
		<td>2018-05-01</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30642">Enabling GPU Scheduling for a Cluster</a></td>
	</tr>
</table>

## April 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS integrated the new Tencent Cloud UI version.</td>
		<td>The new Tencent Cloud UI is elegant, easy to use, and fast. It offers a better container service experience.</td>
		<td>2018-04-01</td>
        <td><a href="https://console.cloud.tencent.com/tke2">CCS Console</a></td>
	</tr>
	<tr>
		<td>CCS models support all types of CVMs.</td>
		<td>During cluster creation or addition of nodes, the models available for selection on the CCS console are consistent with those on the CVM platform.</td>
		<td>2018-04-01</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
	</tr>
</table>

## March 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS supports auto-scaling of services.</td>
        <td>Horizontal Pod Autoscaler (HPA) can <b>automatically scale the number of pods for services according to the average CPU utilization and other metrics of target pods</b>.</td>
		<td>2018-03-01</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32424">Automatic Scaling Basic Operations</a></td>
	</tr>
	<tr>
		<td>The CCS console interface was updated.</td>
		<td>The functions modules of the CCS console were adjusted.</td>
		<td>2018-03-01</td>
		<td>-</td>
	</tr>
</table>

## February 2018
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS supports auto-scaling of clusters.</td>
        <td>Cluster auto scaling <b>adjusts the number of nodes dynamically according to resource demand</b>:<li>If pods become unschedulable due to a lack of resources, the cluster will automatically scale out without any manual intervention.</li><li>If there are enough idle nodes, the cluster will automatically scale in to reduce costs.</li></td>
		<td>2018-02-08</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
	</tr>
	<tr>
		<td>CCS supports log collection.</td>
        <td>This feature allows <b>log files from services or specific node paths to be sent to Kafka, Elasticsearch, or CLS</b> so that users can store and analyze them.</td>
		<td>2018-02-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32419">Log Collection</a></td>
	</tr>
	<tr>
		<td>CCS supports application management.</td>
		<td>CCS supports the group management of services via applications, which significantly simplifies service management.</td>
		<td>2018-02-06</td>
		<td>-</td>
	</tr>
</table>


## December 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>Vouchers can be used to purchase cluster nodes.</td>
		<td>CCS allows users to use vouchers in their accounts to purchase nodes.</td>
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
		<td>Users can set the container directory and project of resources when adding existing nodes.</td>
		<td><li>Container directory: users can set the directory for storing containers and images. We recommend that they be stored in data disks.</li><li>Project: newly added resources will be automatically assigned to this project.</li></td>
		<td>2017-12-20</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30652#addExistingNode">Adding an Existing Node</a></td>
	</tr>
</table>

## November 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>Cluster retention policy</td>
        <td><b>Reserves system process resources such as dockerd and kubelet</b>: when a cluster runs the retention policy, certain resources are reserved to ensuring the proper running of system processes, such as dockerd and kubelet.</td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Cluster drain policy</td>
        <td><b>To ensure sufficient resources for system processes, pods will be drained when necessary</b>.</td>
		<td>2017-11-30</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30654">Draining or Cordoning a Node</a></td>
	</tr>
	<tr>
		<td>Dockerd log rollback</td>
        <td><b>Logs are recycled automatically to ensure sufficient disk space</b>: when log files occupy certain memory, the log rollback feature will be triggered to automatically recycle logs to ensure sufficient disk space.</td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Ingress forwarding rules support wildcards.</td>
        <td><b>Ingress forwarding rules must comply with both the rules for the public network load balancing domain names and the Kubernetes rules for Ingress domain names</b>. <li>They support regular expressions with a length of 1-80 characters.</li><li>Other than regular expressions, they also support `a - z, 0 - 9, and -`. </li><li>For domain names with wildcards, currently only one `*` can be used in a domain name, such as `*.example.com`.</li></td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
</table>


## October 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>The beta CCS application management feature was launched.</td>
        <td>With the rise of micro-service and Devops, users need to develop and manage multiple services in multiple environments. <b>CCS supports group management of services via applications</b>, which significantly simplifies service management.</td>
		<td>2017-10-31</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Multi-region deployment of Image Registry supports the new region Hong Kong (China).</td>
        <td>Image Registry is used to store Docker images which are used to deploy CCS. Each image has a unique ID (image's repository address + image name + image Tag). <b>Image Registry can be deployed in multiple regions, and now Hong Kong (China) is also supported</b>.</td>
		<td>2017-10-31</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/9118">Image Registry Overview</a></td>
	</tr>
	<tr>
		<td>CCS supports Tencent Cloud International.</td>
		<td>The CCS international console was launched, which can help users solve environmental issues in development, testing, and OPS, reduce costs, and improve efficiency.</td>
		<td>2017-10-31</td>
		<td><a href="https://console.cloud.tencent.com/tke2?language=en">CCS International Console</a></td>
	</tr>
</table>

## September 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS Image Registry integrates access permission management.</td>
        <td>The address format of a CCS image is as follows: <code>ccr.ccs.tencentyun.com/${namespace}/${name}:${tag}</code>. <b>The following fields are required for configuring the permissions of Image Registry</b>:<li>${namespace}: namespace of the image repository</li><li>${name}: name of the image repository</li></td>
		<td>2017-09-26</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/11527">CCS Image Registry Resource-level Permission Settings</a></td>
	</tr>
	<tr>
		<td>CCS supports setting labels for services.</td>
        <td>CCS supports setting labels for service pods. <b>When searching services, you can filter services by label.</b>.</td>
		<td>2017-09-26</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Configuration items can be imported to environment variables.</td>
		<td>When deploying a container in a pod, users can import the configuration items ConfigMap and Secret to environment variables.</td>
		<td>2017-09-26</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30675">ConfigMap Management</a></td>
	</tr>
	<tr>
		<td>Clusters support the Project attribute.</td>
        <td><li>Clusters are not project-specific, but CVMs, CLBs, and other resources in a cluster are project-specific.</li><li>Project: new resources added to the cluster will be allocated to the project.</li></td>
		<td>2017-09-26</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/11185">Project of New Resources</a></td>
	</tr>
	<tr>
		<td>CCS supports the region of Singapore.</td>
		<td>CCS now supports resource purchase and business deployment in Singapore.</td>
		<td>2017-09-26</td>
        <td><a href="https://console.cloud.tencent.com/tke2">CCS Console</a></td>
	</tr>
</table>

## August 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS integrates the alarm platform.</td>
        <td>CCS allows users to set multi-dimensional alarms for clusters to <b>discover cluster exceptions quickly and reduce business risks</b>.</td>
		<td>2017-08-23</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30690">Setting Alarms</a></td>
	</tr>
	<tr>
		<td>CCS clusters support Kubernetes 1.7.</td>
        <td>CCS allows users to create <b>clusters with Kubernetes 1.7</b>. </td>
		<td>2017-08-23</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Continuous integration and deployment based on TencentHub</td>
		<td>TencentHub is a management platform created by Tencent Cloud for storing R&D process files and creating DevOps workflows. TencentHub allows users to quickly and conveniently perform operations, such as storage, query, and calls, for files generated during the full project cycle.</td>
		<td>2017-08-23</td>
        <td>TencentHub Product Overview</td>
	</tr>
	<tr>
		<td>Image Registry adds the trigger feature.</td>
        <td>The Image Registry trigger feature allows users to trigger actions, such as service update and webhook and message push after creating an image. <b>The trigger feature can be combined with continuous integration for continuous deployment</b>.</td>
		<td>2017-08-23</td>
		<td>Trigger Overview</td>
	</tr>
	<tr>
		<td>Image Registry supports operation logs.</td>
		<td>Operation logs allow users to view image upload and download records, which helps troubleshoot problems.</td>
		<td>2017-08-23</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Kubectl is used to operate clusters on public networks.</td>
        <td>Kubectl is a CLI tool for Kubernetes cluster operations. <b>You can use Kubectl to connect a local client to a CCS cluster</b>.</td>
		<td>2017-08-04</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30639">Connecting to a Cluster</a></td>
	</tr>
	<tr>
		<td>CCS clusters integrate access permission management.</td>
        <td>Access management is mainly used to help you securely manage and control access to resources under your Tencent Cloud accounts. <b>By using CAM, you can create, manage, and terminate users (or user groups) and manage the use of Tencent Cloud resources through identity management and policies</b>.</td>
		<td>2017-08-04</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/11528">CCS Resource-level Permission API List</a></td>
	</tr>
</table>


## July 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS supports configuration file management.</td>
        <td><li>The configuration file management feature can help you manage the configurations of different businesses under different environments. It supports multiple versions and YAML format.</li><li>The configuration file supports multiple versions, allowing you to update and roll back applications. </li><li>It also allows you to quickly import configurations, in the form of files, into containers.</li></td>
		<td>2017-07-19</td>
		<td>-</td>
	</tr>
	<tr>
		<td>CCS supports CI source code building.</td>
        <td>Continuous container integration <b>enables the automatic and manual creation of container images on the Tencent CCS Platform.</b></td>
		<td>2017-07-18</td>
		<td>Image Building Overview</td>
	</tr>
	<tr>
		<td>Image Registry added TencentHub images.</td>
		<td>Image Registry allows users to view and use TencentHub images.</td>
		<td>2017-07-18</td>
		<td>TencentHub Product Overview</td>
	</tr>
	<tr>
		<td>Image Registry added "My Favorites".</td>
		<td>"My Favorites" will display the images bookmarked by users, allowing users to query and use specific images.</td>
		<td>2017-07-18</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/9118">Image Registry Overview</a></td>
	</tr>
	<tr>
		<td>Image Registry supports multiple namespaces.</td>
        <td><b>Image Registry supports the creation of multiple namespaces. The names of namespaces are globally unique. </b>If the namespace name you want to use is already being used by another user, try using another appropriate name.</td>
		<td>2017-07-18</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/9117">Creating a Namespace</a></td>
	</tr>
</table>

## June 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS supports NFS volumes.</td>
		<td>NFS volumes are used for the persistent storage of data that is read and written many times. They can also be used in scenarios such as big data analysis, media processing, and content management. </td>
		<td>2017-06-24</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30678">Volume Management</a></td>
	</tr>
	<tr>
		<td>CCS supports privileged containers and working directory configurations.</td>
        <td><li>A privileged container has a certain priority. </li><li>WorkingDir: specifies the current working directory. If it does not exist, one will be automatically created. If no directory is specified, the default directory when the container runs is used. If workdir is not specified in the image or through the console, the default workdir is `/`.</li></td>
		<td>2017-06-24</td>
		<td>-</td>
	</tr>
	<tr>
		<td>CCS supports cluster capacity.</td>
		<td>A cluster is a collection of cloud resources required for running a container, including several CVMs and CLBs. You can run your applications in your cluster.</td>
		<td>2017-06-07</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30635">Cluster Overview</a></td>
	</tr>
	<tr>
		<td>CCS supports the auto-formatting data disks and specifying of container directories while creating/adding CVMs in container clusters.</td>
		<td>If the system disk capacity is small or a server with a data disk needs to format the data disk, you can set the storage directory of containers and images.</td>
		<td>2017-06-07</td>
        <td><li><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding Nodes</a></li></td>
	</tr>
	<tr>
		<td>CCS supports service re-deployment.</td>
		<td>Re-deployment means to re-deploy containers under a service and re-fetch images.</td>
		<td>2017-06-07</td>
        <td><li><a href="https://intl.cloud.tencent.com/document/product/457/30672">Service Management</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30673">Ingress Management</a></li></td>
	</tr>
</table>

## April 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS supports adding existing CVMs to container clusters.</td>
		<td>CCS allows users to add existing CVMs to container clusters, which helps users reuse existing resources and effectively reduce costs.</td>
        <td>2017-04-27</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30652#.E6.B7.BB.E5.8A.A0.E5.B7.B2.E6.9C.89.E8.8A.82.E7.82.B9">Adding a Existing Node</a></td>
	</tr>
	<tr>
		<td>CCS supports the query of monitoring metrics for instances, services, and clusters.</td>
		<td>A good monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud CCS. You can collect monitoring data in different dimensions for different resources to quickly master resource usage and easily locate errors.</td>
        <td>2017-04-27</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
	</tr>
	<tr>
		<td>CCS supports viewing container logs.</td>
		<td>By creating log collection rules, CCS can provide users with log information from within a cluster, making it easier for them to maintain and troubleshoot containers.</td>
        <td>2017-04-27</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32419">Log Collection</a></td>
	</tr>
	<tr>
		<td>CCS web remote terminal supports file upload and download.</td>
		<td><ul class="params"><li>To upload a file, you need to specify the directory to which the file is uploaded.</li><li>To download a file, you need to specify the path for storing the file.</li></ul></td>
        <td>2017-04-19</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/9120">Remote Terminal Basic Operations</a></td>
	</tr>
	<tr>
		<td>CCS supports custom security groups when creating a cluster.</td>
        <td>If the current default security group cannot meet your business requirements, you can refer to <a href="https://intl.cloud.tencent.com/document/product/213/34826">Managing Security Group Rules</a> to customize cluster security groups.</td>
        <td>2017-04-19</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
	</tr>
</table>

## March 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>CCS allows remote web terminals to log in to containers.</td>
        <td>Remote terminals can help you debug containers quickly and connect to the containers for troubleshooting. <b>It supports file copy, paste, upload, and download operations. This helps solve the problems of long container login paths and difficult debugging</b>.</td>
        <td>2017-03-15</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/9120">Remote Terminal Basic Operations</a></td>
	</tr>
	<tr>
		<td>CCS supports third-party image creation services.</td>
        <td>The third-party image creation service <b>can help users deploy applications flexibly based on actual business requirements</b>.</td>
        <td>2017-03-15</td>
		<td>-</td>
	</tr>
	<tr>
		<td>CCS supports Layer-7 CLBs.</td>
        <td>An Ingress is a collection of rules that allow access to services within a cluster. You can configure different forwarding rules to <b>allow different URLs to access different services within the cluster</b>.</td>
        <td>2017-03-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30673">Ingress Management</a></td>
	</tr>
	<tr>
		<td>Users can query monitoring information about clusters, services, and pods.</td>
        <td>A good monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud CCS. <b>You can collect monitoring data in different dimensions for different resources </b>to quickly master resource usage and easily locate errors.</td>
        <td>2017-03-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
	</tr>
	<tr>
		<td>CCS supports native Kubernetes APIs, requesting Kubernetes certificates via Tencent Cloud APIs, and all Kubernetes features.</td>
        <td>CCS makes it easy for you to build, operate, and manage container clusters by seamlessly utilizing Tencent Cloud computing, networking, storage, monitoring, and security capabilities. <b>You can refer to corresponding examples in the API documentation to perform operations such as adding, deleting, modifying, and querying scaling groups, networks, nodes, and clusters</b>.</td>
        <td>2017-03-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32029">API Overview</a></td>
	</tr>
</table>

## December 2016
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Release Time</th><th style="width:15%">Related Document</th> </tr>
	<tr>
		<td>Cluster Management</td>
		<td>Cluster management supports cluster addition, deletion, modification, and query, VPC-based container clusters, cross-AZ clusters, and open-source native Kubernetes APIs.</td>
        <td>2016-12-26</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30635">Cluster Management</a></td>
	</tr>
	<tr>
		<td>Service Management</td>
		<td>Service management supports service addition, deletion, modification, and query, creation of services via private images and official Docker images, and cross-zone scheduling of services.</td>
        <td>2016-12-26</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30635">Service Management</a></td>
	</tr>
	<tr>
		<td>Image Management</td>
		<td>Image management supports official Docker images, My Images, upload and download of private images, and official Docker image acceleration.</td>
        <td>2016-12-26</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/9118">Image Registry Overview</a></td>
	</tr>
	<tr>
		<td>Cluster monitoring and container monitoring</td>
		<td>CCS provides the basic monitoring feature for all clusters by default.</td>
        <td>2016-12-26</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30689">Viewing Monitoring Data</a></td>
	</tr>
	<tr>
		<td>Service creation, event update, and rolling update for services</td>
		<td>Rolling update indicates that pods are updated one by one, which allows you to update the service without interrupting your business.</td>
        <td>2016-12-26</td>
		<td>-</td>
	</tr>
</table> 

<style>
	.params{ margin-bottom:0px!important; } 
</style>

