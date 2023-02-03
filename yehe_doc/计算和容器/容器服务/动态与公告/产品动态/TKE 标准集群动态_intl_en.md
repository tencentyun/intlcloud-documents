## December 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody>
	  <tr>
    <td>Supports upgrading a Kubernetes version to 1.22</td>
    <td>You can upgrade a cluster Kubernetes version from 1.20 to 1.22.</td>
    <td>2022-12-08</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38179">Update Notes of TKE Kubernetes Major Versions</a></td>
  </tr>
</tbody>
</table>

## November 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody>
	  <tr>
    <td>Launches the imc-operator component</td>
    <td>You can cache super nodes in clusters on images with CRD.</td>
    <td>2022-11-10</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/44484">Image Cache</a></td>
  </tr>
  <tr>
    <td>Enhanced the dedicated scheduler for native nodes</td>
    <td>Supports virtually expanding the capacity of native nodes and configuring scheduling and running thresholds for the nodes.</td>
    <td>2022-11-01</td>
    <td>-</td>
  </tr>
</tbody>
</table>

## September 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody>
	  <tr>
    <td>Launched the Ceberus enhanced add-on</td>
    <td>Signature images in the TCR repository can be verified for trustworthiness, reducing the security risks of invalid images being deployed in the container environment.</td>
    <td>2022-09-29</td>
    <td>-</td>
  </tr>
  <tr>
    <td>Enabled all custom kubelet parameters</td>
    <td>It provides an entry for you to modify parameters.</td>
    <td>2022-09-29</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38139">Custom Kubernetes Component Launch Parameters</a></td>
  </tr>
  <tr>
    <td>Defined the error codes of Service/Ingress events</td>
    <td>It helps quickly troubleshoot business exceptions and provides solutions.</td>
    <td>2022-09-28</td>
    <td>-</td>
  </tr>
	<tr>
    <td>Supported scheduling Pods in kube-system to monthly subscribed super nodes</td>
    <td>It helps reduce resource use costs.</td>
    <td>2022-09-26</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/39760">Pod Schedulable to Super Node</a></td>
  </tr>
  <tr>
    <td>Integrated the basic monitoring add-on `tke-monitor-agent` into the add-on management module for maintenance</td>
    <td>You can upgrade the add-on in the console.</td>
    <td>2022-09-22</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/48894">Upgrading tke-monitor-agent</a></td>
  </tr>
  <tr>
    <td>Launched the `SecurityGroupPolicy` enhanced add-on</td>
    <td>You can bind a Pod not matching a policy to a security group to control the inbound and outbound network traffic of the Pod.</td>
    <td>2022-09-08</td>
    <td>-</td>
  </tr>
  <tr>
    <td>Launched the in-place Pod configuration adjustment capabilities for TKE native nodes</td>
    <td>You can directly modify the Request/Limit values of CPU and memory without restarting a Pod, which helps handle traffic surges and reduce business costs.</td>
    <td>2022-09-08</td>
    <td>-</td>
  </tr>
</tbody>
</table>




## August 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody>
  <tr>
    <td>Launched Request smart recommendation for native nodes<br></td>
    <td>It recommends the Request/Limit values of resources at the container level for Kubernetes workloads to reduce resource waste.</td>
    <td>2022-08-22</td>
    <td>-</td>
  </tr>
  <tr>
    <td>Launched the dedicated scheduler for native nodes</td>
    <td>It virtually expands the capacity of native nodes, solving the problem of resource occupation and low utilization.</td>
    <td>2022-08-19</td>
    <td>-</td>
  </tr>
  <tr>
    <td>Supported automatic update for the image cache feature</td>
    <td>Automatic update is supported for the image cache feature. After it is enabled, a cache update will be triggered when the updated image is uploaded to TCR, eliminating the need to recreate an image cache.</td>
    <td>2022-08-08</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/44484">Image Cache</a></td>
  </tr>
  <tr>
    <td>Supported edit operations for the image cache feature</td>
    <td>The image cache feature allows you to edit security groups, images, cache sizes, and expiration policies.<br></td>
    <td>2022-08-08</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/44484">Image Cache</a></td>
  </tr>
  <tr>
    <td>Released the brand-new native node.</td>
    <td>A native node is a brand-new node type of TKE. It supports declarative APIs and adopts the FinOps concept, facilitating cost reduction and efficiency improvement for Tencent Cloud resources through the "visual resource management dashboard", "smart request recommendation", and "dynamic dedicated scheduler".</td>
    <td>2022-08-04</td>
    <td>-</td>
  </tr>
	 <tr>
    <td>Supported managing image caches through CRD.</td>
    <td>Image caches can be managed through CRD on super nodes. Currently, management can be performed in the console and through TencentCloud API. With the image caching feature, Pods can be started within seconds.</td>
    <td>2022-08-04</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/44484">Image Cache</a></td>
  </tr>
	  <tr>
    <td>Supported declaring the size of resources required by a Pod.</td>
    <td>You can declare the size of the system disk required by a Pod through an annotation on super nodes. If the size exceeds 20 GiB, the excessive part will be billed based on the pay-as-you-go published price of CBS Premium Cloud Storage, meeting your requirements for system disk resources in special scenarios.</td>
    <td>2022-08-03</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/36162">Annotations</a></td>
  </tr>
  <tr>
    <td>Added third-party nodes.</td>
    <td>The TencentOS Server 2.4 (TK4) operating system is supported, which is compatible with the CentOS 7 user mode. The entry to create Cilium-Overlay clusters is added in the TKE console for easier use. In Cilium-Overlay network mode, the check for a conflict between the IP range of a container and that of another container in another cluster within the same VPC can be ignored, thereby solving your problem of IP resource insufficiency.</td>
    <td>2022-08-01</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/49152">Cilium-Overlay Mode</a></td>
  </tr>
</tbody>
</table>

## July 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody>
  <tr>
    <td>Released all the super nodes.</td>
    <td>A super node is a brand-new node form of TKE, which supports custom node size and flexible configuration adjustment. The monthly subscription mode is more cost-effective, while the pay-as-you-go mode eliminates the need to reserve resource buffer, contributing to your cost reduction and efficiency improvement. Node management and resource operations are simplified, so that you can concentrate on the business.</td>
    <td>2022-07-26</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/39759">Super Node Overview</a></td>
  </tr>
	  <tr>
    <td>Supported productized Nginx-ingress.</td>
    <td>The Nginx-ingress add-on can be quickly deployed for out-of-the-box Nginx services. By default, CM and CLS are integrated to meet the observability requirement.</td>
    <td>2022-07-25</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38981">Installing Nginx-ingress Instance</a></td>
  </tr>
	  <tr>
    <td>Quickly cleared invalid RBAC resources.</td>
    <td>RBAC resource objects can be quickly cleared. De-registered Tencent Cloud accounts can be automatically detected, which is suitable for scenarios where cluster permissions need to be reclaimed after personnel turnover.</td>
    <td>2022-07-15</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/48776">Clearing De-registered Tencent Cloud Account Resources</a></td>
  </tr>
  <tr>
    <td>Released the deletion protection feature for the node pool.</td>
    <td>This feature is suitable for node resource protection, fixing the issue where node resources were batched released due to maloperations.</td>
    <td>2022-07-13</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/35900">Node Pool Overview</a></td>
  </tr>
	<tr>
    <td>Supported associating with a TMP instance.</td>
    <td>A cluster can be associated with a TMP instance during creation, simplifying the association process.</td>
    <td>July 6, 2022</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/46736">Quick Migration from TPS to TMP</a></td>
  </tr>
</tbody>
</table>




## June 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody>
<tr>
    <td>TMP provides metrics recommended by experts</td>
    <td>Simplifies the metric selection.</td>
    <td>2022-06-21</td>
    <td>-</td>
  </tr>
<tr>
    <td>qGPU supports viewing GPU card resources with CRD</td>
    <td>Unifies and streamlines the GPU resource view.</td>
    <td>2022-06-07</td>
    <td>-</td>
  </tr>
  <tr>
    <td>qGPU supports scheduling at both the node and GPU card levels</td>
    <td>Realizes refined scheduling of GPU resources and solves fragmentation problems.</td>
    <td>2022-06-07</td>
    <td>-</td>
  </tr>
  <tr>
    <td>Unschedulable nodes can be bound to the CLB backend</td>
    <td>Solves the issue of unbalanced traffic load.</td>
    <td>2022-06-01</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/36836">Service Backend Selection</a></td>
  </tr>
</tbody>
</table>



## May 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody>
  <tr>
    <td>TKE provides audit/log/event APIs</td>
    <td>You can install relevant add-ons in TKE clusters by calling the audit/log/event APIs.</td>
    <td>2022-05-18</td>
    <td>-</td>
  </tr>
</td>
  </tr>
</tbody>
</table>



## April 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody>
  <tr>
    <td>Kubernetes versions are discontinued</td>
    <td>Kubernetes v1.14 and earlier versions cannot be created from May 20, 2022 (UTC +8).</td>
    <td>2022-04-26</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/48408" target="_blank" rel="noopener noreferrer">Discontinuing Kubernetes v1.14 and Earlier Versions</a></td>
  </tr>
  <tr>
    <td>The scaling group service is discontinued</td>
    <td>Starting from June 6, 2022 (UTC +8), no more TKE scaling groups can be created in the console and by using the API. The feature will be officially discontinued from June 13, 2022 (UTC +8). Existing scaling groups will be migrated to node pools automatically.</td>
    <td>2022-04-26</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/51206" target="_blank" rel="noopener noreferrer">Deactivation of Scaling Group Feature</a></td>
  </tr>
  <tr>
    <td>Updates CFS dynamic persistence storage</td>
    <td>TKE supports sharing a CFS storage instance when dynamically create a PVC.</td>
    <td>2022-04-18</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/38707" target="_blank" rel="noopener noreferrer">CFS-CSI</a></td>
  </tr>
  <tr>
    <td>Launches TMP</td>
    <td>Supports cross-region monitoring in multiple VPCs and supports checking multiple monitoring instances on a single Grafana instance.</td>
    <td>2022-04-01</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/46734" target="_blank" rel="noopener noreferrer">TMP Overview</a></td>
  </tr>
  <tr>
    <td>TPS instances can be migrated to TMP</td>
    <td>You can have enhanced cloud native monitoring capabilities with quick migration.</td>
    <td>2022-04-01</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/46734" target="_blank" rel="noopener noreferrer">Quick Migration of TPS Instances to TMP</a></td>
  </tr>
</tbody>
</table>


## March 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody><tr>
<td>Starts charging on managed clusters</td>
<td>For TKE managed clusters created before March 21, 2022 10:00 (UTC +8), select a specification for them in the console before April 1, 2022 10:00 (UTC +8). If you do not select a specification, they will be billed on the basis of the recommended specification.</td>
<td>2022-03-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/45156">Starting Charging on Managed Clusters</a></td>
</tr>
<tr>
<td>Backend architecture upgrade of TKE basic monitoring</td>
<td>Provides enhanced monitoring and HPA service.</td>
<td>2022-03-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/46740">Description of tke-monitor-agent</a></td>
</tr>
<tr>
<td>Supports upgrading of log collection add-on in the Ops center</td>
<td>Supports upgrading of log collection add-on in the Ops center. Please upgrade the add-on to the latest version.</td>
<td>2022-03-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/47686">Log Add-On Version Upgrade</a></td>
</tr>
<tr>
<td>Optimized user experience in the TKE console</td>
<td><li>On the <b>Pods management</b> details page, you can search by Pod status in the search box.</li><li>In the <b>Log</b> column of cluster workload details page, you can search by name in the drop-down list.</li></td>
<td>2022-03-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30635">Cluster Management</a></td>
</tr>
</tbody>
</table>




## February 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody><tr>
<td>Optimized the search feature in the console</td>
<td>You can filter clusters by status, and prompts are available when you search by node/node pool label.</td>
<td>2022-02-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30635">Cluster Overview</a></td>
</tr>
<tr>
<td>Upgraded the add-on architecture</td>
<td>Add-ons can be installed via cloud APIs after the add-on architecture upgrade.</td>
<td>2022-02-26</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/32029">Overview of APIs</a></td>
</tr>
<tr>
<td>Optimized CFS Turbo add-on</td>
<td>Fixed known mounting issues.</td>
<td>2022-02-25</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/43101">Static Mounting of CFS-Turbo for TKE Clusters</a></td>
</tr>
<tr>
<td>Optimized operations of log collection rules in the console</td>
<td>When Pod Labels are specified as the log source, you can add != label filter and optimize selection for namespaces in container standard output (multiple namespaces can be chosen and excluded).</td>
<td>2022-02-15</td>
<td>-</td>
</tr>
</tbody>
</table>




## January 2022
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tbody>
<tr>
<td>Configures the httpHeaders for health check in the TKE console</td>
<td>Health Check is a service provided by TKE to check the status and running of resources in the cluster.</td>
<td>2022-01-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/38428">Health Check</a></td>
</tr>
<tr>
<td>Optimized operations of node pool in the console</td>
<td>You can set cloud tags and configure instance creation policies in the node pool.</td>
<td>2022-01-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/35900">Node Pool Overview</a></td>
</tr>
<tr>
<td>Updates CFS add-on</td>
<td>CFS supports using V3 and V4 protocols for mounting.</td>
<td>2022-01-13</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/36153">CFS Instructions</a></td>
</tr>
<tr>
<td>Updates CBS-CSI add-on</td>
<td>Cloud disks dynamically created by CBS-CSI inherit the cluster cloud tags.</td>
<td>2022-01-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/39136">CBS-CSI</a></td>
</tr>
<tr>
<td>Updates Request Recommendation</td>
<td>Supports downloading of recommended Request values.</td>
<td>2022-01-10</td>
<td><a href="https://www.tencentcloud.com/document/product/457/41659">Resource Utilization Analysis and Optimization Suggestions</a></td>
</tr>
<tr>
<td>Supports connecting to the Pods in TKE clusters via the API gateway</td>
<td>Supports exposing services via API gateways. It can be specified when you create an Ingress.</td>
<td>2022-01-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/46001">API Gateway TKE Tunnel Configuration</a></td>
</tr>
</tbody>
</table>

## December 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Updates CFS-CSI add-on</td>
		<td>
		Cloud tags can be added when CFS instances are created dynamically through StorageClass.
		</td>
		<td>2021-12-25</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/36154">Managing CFS Templates by Using a StorageClass</a></td>
</tr>	
</table>




## November 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Enhances qGPU features</td>
		<td>
		<li>qGPU supports multiple GPU cards in one container. A container can be bound with multiple entire cards or a scorecard. In addition, GPU monitoring is supported.</li>
			<li>qGPU supports GPU monitoring. It supports GPU card/Pod/container utilization monitoring.</li>
			<li>qGPU supports TKE BM clusters and supports Ampere GPU cards.</li>
			<li>qGPU supports the online/offline hybrid deployment feature and supports the native priority scheduling capabilities of online inference and offline training.</li>
		</td>
		<td>2021-11-05</td>
		<td>-</td>
</tr>
	<tr>
    <td>Feature updates of CFS-CSI add-on</td>
		<td>
		The CFS-CSI add-on in clusters of v1.20 supports reading the fsgroup configuration of security context in workloads.
		</td>
		<td>2021-11-02</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/38707">CFS-CSI</a></td>
</tr>	
</table>

## October 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Launches Request Recommendation</td>
		<td>
		Request Recommendation is a resource recommendation feature launched by TKE. It recommends Request and Limit values for resources at the container level in TKE and TKE Serverless clusters.
		</td>
		<td>2021-10-27</td>
		<td>-</td>
</tr>
	<tr>
    <td>Launches the registered cluster feature</td>
		<td>
		Registered cluster is a new cluster type of TKE. It allows you to register Kubernetes clusters in your local infrastructure or those of other cloud vendors with TKE for unified management.
		</td>
		<td>2021-10-26</td>
		<td>-</td>
</tr>	
	<tr>
    <td>Launches the cloud-native AI service</td>
		<td>
		Cloud-native AI is a complete solution for AI scenarios launched by TKE, which has the characteristics of modularity, low coupling, and high scalability.
		</td>
		<td>2021-10-18</td>
		<td>-</td>
</tr>	
</table>



## September 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Launches qGPU add-on</td>
		<td>
		qGPU is a GPU sharing technique launched by Tencent Cloud. It supports sharing of GPU cards among multiple containers and provides the capacity to isolate the vRAM and computing resource among containers.
		</td>
		<td>2021-09-16</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/42973"> qGPU</a></td>
</tr>	
</table>


## August 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Uses pre-request script to add existing nodes</td>
		<td>
		When adding existing nodes, you can use pre-request scripts via API. The script is executed before the K8s node is initialized. You can customize the configuration such as data disk mounting.
		</td>
		<td>2021-08-01</td>
		<td>-</td>
</tr>	
</table>


## July 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Supports specifying the model when creating a GPU CVM in the console</td>
		<td>
		Chooses the GPU driver version, CUDA version and cuDNN version in the console.
		</td>
		<td>2021-07-13</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30656">Using a GPU Node</a></td>
</tr>	
<tr>
    <td>Supports MIG</td>
		<td>
		Once enabled, you can improve the GPU utilization in scenarios where multiple jobs are running in parallel.
		</td>
		<td>2021-07-13</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30656">Using a GPU Node</a></td>
</tr>	
<tr>
    <td>Enhances TKE console</td>
		<td>
		Supports formatting and mounting of multiple data disks when adding existing nodes.
		</td>
		<td>2021-07-05</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding an Existing Node</a></td>
</tr>	
</table>




## June 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Introduced the feature of adding external nodes</td>
		<td>
		External nodes allow users to add non-Tencent Cloud CVMs to a TKE cluster. Users provide computing resources and TKE manages cluster lifecycle.
		</td>
		<td>2021-06-28</td>
		<td>-</td>
</tr>	
</table>


## May 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Improves cloud native monitoring</td>
		<td>
		<li>Optimizes data collecting configuration.</li>
		<li>Displays status of collection targets.</li>
		<li>Optimizes interaction process.</li>
		<li>Tests the collection target.</li></td>
		<td>2021-05-28</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/48770">Log Collection</a>
</tr>
<tr>
    <td>Launches OLM add-on</td>
		<td>
	The OLM add-on helps users automatically install and upgrade Operator, and manage its lifecycle.
	  </td>
		<td>2021-05-28</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/40955">OLM</a>
</tr>
<tr>
    <td>Launches HPC add-on</td>
		<td>
	Developed by Tencent Cloud, HPC can help periodically modify the number of replicas of K8s workload. Used in conjunction with HPC CRD resources, it can support scheduled actions in seconds.
	  </td>
		<td>2021-05-28</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/40956">HPC</a>
</tr>
<tr>
    <td>Enhances TKE console</td>
		<td>
<li>Selects OS upon node creation.</li>
<li>Modifies desired number of nodes while scaling up a node pool.</li>
<li>Searches workloads by labels.</li>
	  </td>
		<td>2021-05-20</td>
		<td>
<a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding a Node</a>
		</td>
</tr>
</table>






## April 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Enhances TKE console</td>
		<td>
		<li>StatefulSet and DaemonSet can be redeployed with a few steps.</li>
		<li>Secret supports TLS certificate. You can import it from file or paste multiple key-value pairs to enter in a batch.</li>
		<li>The container health check readinessProbe supports configuration and naming of a port.</li>
		<li>Namespace supports the selection of “All namespaces” and can be searched by keyword.</li></td>
		<td>2021-04-30</td>
		<td><li><a href="https://intl.cloud.tencent.com/document/product/457/30663">StatefulSet Management</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30664"> DaemonSet Management</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30676">Secret Management</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30669">Setting the Health Check for a Workload</a></li>
		<li><a href="https://intl.cloud.tencent.com/document/product/457/30660"> Namespaces</a></li></td>
</tr>	
<tr>
    <td>Enhances log collection capability</td>
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
    <td>The beta ARM cluster starts.</td><td>The beta of ARM cluster starts. To join the beta, <a href="https://console.tencentcloud.com/workorder/category">submit a ticket</a>.</td><td>2021-03-31</td><td>-</td>
</tr>
<tr>
    <td>Enhances TKE console</td><td>
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
    <td>Enhances node search capability</td><td>The nodes can be searched in batch by label or IP address.</td><td>2021-03-19</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30650">Node Overview</a></td>
</tr>
<tr>
</tr>
</table>





## February 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Enhances the operations for nodes in the node pool</td><td>The node in the node pool can be cordoned and drained, and the node management capability of the node pool is improved.</td><td>2021-02-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35900">Node Pool Overview</a></td>
</tr>
<tr>
    <td>Users can mount data disk partition when adding an existing node</td><td>When adding an existing node to a cluster or node pool, users can select partition or logical volume name for the data disk mounting, which provides more flexible mount settings.</td><td>2021-02-20</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30652#.E6.B7.BB.E5.8A.A0.E5.B7.B2.E6.9C.89.E8.8A.82.E7.82.B9">Adding an Existing Node</a></td>
</tr>
</table>



## January 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Master version upgrade supports minor version</td><td>This feature provides a more flexible version upgrade mechanism.</td><td>2021-01-14</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading the Master Kubernetes Version</a></td>
</tr>
</table>


## December 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Node pool supports configuration of removal protection</td><td>Removal protection is used to prevent the nodes of important application from being scaled in or being removed from the node pool during manually size adjustment.</td><td>2020-12-30</td><td>-</td>
</tr>
<tr>
    <td>Node pool supports configuration of multiple alternative models that have the same specification</td><td>This feature can reduce the risk of scale-out failure caused by sold out single model resource.</td><td>2020-12-29</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35903">Adjusting a Node Pool</a></td>
</tr>
<tr>
    <td>Launches Descheduler add-on</td><td>Based on the actual node loads, this add-on supports automatic rescheduling of marked services on high-load nodes to maintain the cluster load balance.</td><td>2020-12-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39146">DeScheduler</a></td>
</tr>
<tr>
    <td>Fully launches Nginx-ingress add-on</td><td><ul class="params"><li>The issue of nginx-ingress-controller toleration scheduling is fixed.</li><li>Nginx-Ingress UI experience is improved, including the regular matching of forwarding rule, configuration of backend ClusterIP mode Service, and certificate supporting kubernetes.io/tls type Secret.</li></ul></td><td>2020-12-24</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39143">Nginx-ingress</a></td>
</tr>
<tr>
    <td>Launches CBS-CSI add-on</td><td>CBS-CSI add-on supports: <ul class="params"><li>Creating static volume/dynamic volume</li><li>Storage topology awareness</li><li>Scheduler awareness of node maxAttachLimit</li><li>Online volume expansion</li><li>Volume snapshot and restoration</li></ul></td><td>2020-12-22</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39136">CBS-CSI</a></td>
</tr>
<tr>
    <td>Enhances TKE console</td><td><ul class="params"><li>The console supports Resource Quota, which can be used to configure the resource quotas and default resource request values for the namespace.</li><li>The ConfigMap can be generated based on the imported file.</li></td><td>2020-12-09</td><td>-</td>
<tr>
   <td>Launches NetworkPolicy add-on</td><td>This add-on supports automatic synchronization of NetworkPolicy to make the network isolation policy effective.</td><td>2020-12-03</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39120">Network Policy</a></td>
</tr>
</table>



## November 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Launches beta for new TKE network solution</td><td>Leveraging intelligent ENI, TKE launches a new container network solution. In this solution, each pod is assigned a dedicated ENI. Pod-to-pod communications can be implemented without traveling through the node protocol stack (default namespace), so as to shorten the container access link and the access latency.</td><td>2020-11-27</td><td>-</td>
</tr>
<tr>
    <td>Launches beta for productized Nginx-Ingress</td><td>TKE extends and maintains native Nginx-ingress to help you quickly deploy and build a traffic access gateway in the production environment, and provide complete Nginx-ingress lifecycle management, automated cloud native monitoring, CLS and supporting OPS capabilities.</td><td>2020-11-26</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39143">Nginx-ingress</a></td>
</tr>
<tr>
    <td>Launches event dashboard</td><td>This feature implements the aggregation search and trend observation of top events and exception events.</td><td>2020-11-26</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38892">Event Dashboard</a></td>
</tr>
<tr>
    <td>Launches audit dashboard</td><td>This feature implements the aggregation search and direct observation of cluster global, nodes, K8s objects and other important operations.</td><td>2020-11-26</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38890">Audit Dashboard</a></td>
</tr>
<tr>
    <td>The node pool and cluster operating system can be modified</td><td>Users can create node pools of different operating systems as needed to facilitate the standardized management of nodes.</td><td>2020-11-23</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35901">Creating a Node Pool</a></td>
</tr>
<tr>
    <td>Adds DynamicScheduler add-on</td><td>This add-on performs scheduling based on actual node loads, so as to prevent traffic hotspots.</td><td>2020-11-21</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39119">DynamicScheduler</a></td>
</tr>
</table>


## October 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TPS supports using edge cluster as monitoring object to access the monitoring instance.</td><td>TPS supports the monitoring of edge clusters and the management of multiple clusters across VPCs.</td><td>2020-10-30</td><td><a href="https://intl.cloud.tencent.com/document/product/457/46739">PROM Instance Management</a></td>
</tr>
<tr>
    <td>TPS alarm policy supports webhook configuration.</td><td>The alarm policy supports webhook configuration, which enables users to troubleshoot abnormal services in time and improve service stability.</td><td>2020-10-30</td><td><a href="https://intl.cloud.tencent.com/document/product/457/46739">Alarm Configurations</a></td>
</tr>
<tr>
    <td>TKE node pool adds the capability of viewing scaling log</td><td>This feature helps users to more easily observe the change of node number in the node pool as well as the trigger cause and result of scaling, improving the node pool observability.</td><td>2020-10-13</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38370">Viewing Node Pool Scaling Logs</a></td>
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
    <td>Launches DNSAutoscaler add-on</td><td>This add-on can obtain number of nodes and cores of the cluster via Deployment, and auto-scaling the number of DNS replicas according to the preset scaling policy, so as to improve DNS availability.</td><td>2020-09-23</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39122">DNSAutoscaler</a></td>
</tr>
<tr>
    <td>Launches beta for cloud native ETCD</td><td>This feature enables you to one-click deploy the high-reliability and high-performance ETCD cluster, which is profusely verified through Tencent’s internal services. It also provides cross-AZ disaster recovery capabilities and optimal performance configuration.</td><td>2020-09-16</td><td>-</td>
</tr>
<tr>
    <td>Quick add-on configuration is available when creating the cluster</td><td>You can easily and quickly configure the required add-ons for the cluster.</td><td>2020-09-15</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
</table>

## August 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> 
</tr>
<tr>
    <td>Optimizes the monitoring capability of TPS</td><td><ul class="params"><li>The cluster monitoring collection items are preset, and a diverse Grafana dashboard is available.</li><li>The Targets list page is added to allow users to view the real-time status of monitoring tasks.</li></ul></td><td>2020-08-31</td><td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/48770">Data Collection Configurations</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/46732">Alarm Configurations</a></li></ul></td>
</tr>
<tr>
    <td>The alarm module of the cloud native monitoring service was upgraded.</td><td><ul class="params"><li>It can be associated with a local Alertmanager add-on.</li><li>It supports managing PROM instance rules with CRD.</li></ul></td><td>2020-08-31</td><td><a href="https://intl.cloud.tencent.com/document/product/457/46732">Alarm Configurations</a></td>
</tr>
<tr>
    <td>TKE launches NodeProblemDetectorPlus add-on</td><td>It supports configuring node self-healing policy on the basis of existing detection feature.</td><td>2020-08-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38784">Node-Problem-Detector-Plus</a></td>
</tr>
<tr>
    <td>TKE launches in-place major-version upgrade capabilities</td><td>The in-place major-version upgrade feature supports major-version upgrade without node reinstallation.</td><td>2020-08-25</td><td>-</td>
</tr>
<tr>
    <td>Fully launches TKE add-ons</td><td>The add-on feature enables users to install or uninstall multiple advanced add-ons for clusters.</td><td>2020-08-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/33988">Add-on Overview</a></td>
</tr>
<tr>
    <td>Fully launches TKE Kubernetes 1.18 version</td><td>Allows users to create clusters of the Kubernetes 1.18 version and upgrade clusters to the 1.18 version.</td><td>2020-08-24</td><td>-</td>
</tr>
</table>


## July 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Optimizes capabilities of storage plug-ins</td><td><ul class="params"><li>The TKE console supports PV creation without specifying StorageClass.</li><li>Users can set and mount COS sub-directories.</li></ul></td><td>2020-07-28</td><td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/37770">PV and PVC Binding Rules</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/36160">Using COS</a></li></ul></td>
</tr>
<tr>
    <td>Cluster creation supports setting node configuration placement groups</td><td>This feature enables disaster recovery and high availability for nodes when they are launched.</td><td>2020-07-15</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
<tr>
    <td>Cloud native monitoring is launched for beta testing.</td><td>It supports one-click deployment of the high-availability monitoring architecture and quick association with TKE clusters and TKE Serverless clusters.</td><td>2020-07-15</td><td>-</td>
</tr>
<tr>
    <td>The collection configuration and alarm configuration of TPS are implemented through products</td><td><ul class="params"><li>Three configuration modes are supported: service monitor, pod monitor, and raw job.</li><li>Alarm history rewinding is supported.</li></ul></td><td>2020-07-15</td><td>-</td>
</tr>
<tr>
    <td>Launches beta for RBAC-based permission control with finer granularity</td><td><ul class="params"><li>It allows cluster admins to configure management permissions for different roles regarding different resources in the cluster.</li><li>It supports certificate revocation.</li><li>It is suitable for enterprises’ compliance permission management scenarios.</li></ul></td><td>2020-07-10</td><td><a href="https://intl.cloud.tencent.com/document/product/457/37366">TKE Kubernetes Object-level Permission Control</a></td>
</tr>
</table>

## June 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Launches beta for IPVS-bpf mode</td><td>TKE uses eBPF to bypass conntrack and optimize the Kubernetes Service, improving the non-persistent connection performance by over 40% and reducing the p99 latency by over 31%.</td><td>2020-06-19</td><td>-</td>
</tr>
<tr>
    <td>TKE supports the creation of services in CLB-to-Pod direct access mode</td><td>The forwarding performance of pods with LoadBalancer directly connected to ENI can be improved by over 10%.</td><td>2020-06-18</td><td><a href="https://intl.cloud.tencent.com/document/product/457/36837">Using Services with CLB-to-Pod Direct Access Mode</a></td>
</tr>
<tr>
    <td>TKE supports balanced forwarding and local binding</td><td>TKE has strengthened the Loadbalancer Service and the LoadBalancer Ingress backend binding with the RS feature. TKE supports balanced forwarding and local binding.</td><td>2020-06-18</td><td><a href="https://intl.cloud.tencent.com/document/product/457/36836">Service Backend Selection</a></td>
</tr>
<tr>
    <td>Comprehensively upgrades The TKE app market</td><td>The app market provides an output window for Tencent Cloud’s practical cloud-native technologies and also provides a variety of great community apps that users can easily and quickly use.</td> <td>2020-06-10</td><td><a href="https://intl.cloud.tencent.com/document/product/457/37706">Application Market</a></td>
</tr>
</table>

## May 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TKE launches the ContainerNative network LoadBalancer (supports CLB-to-Pod direct access)</td><td>In TKE, you can use services and ingresses with LoadBalancer directly connected to pods, which provides higher performance and more robust product capabilities. This feature can resolve issues such as imbalanced load for persistent connections, health check session persistence configuration issues, and IPVS jitter.</td><td>2020-05-12</td><td>-</td>
</tr>
<tr>
    <td>Optimizes the cluster deletion feature</td><td><ul class="params"><li>When deleting a cluster, you can view the existing nodes, security groups, cloud disks, and other resources in the cluster.</li><li>A deletion risk reminder is added to prevent accidental deletion that may interrupt your business.</li><li>You can delete the nodes, cloud disks, and other resources in the cluster at the same time.</li></ul></td><td>2020-05-12</td><td><a href="https://intl.cloud.tencent.com/document/product/457/36280">Deleting Clusters</a></td>
</tr>
<tr>
    <td>TKE launches the open-source KMS plug-in</td><td><ul class="params"><li><a href="https://github.com/Tencent/tke-kms-plugin">The Tencent Cloud TKE-KMS plug-in</a> integrates the rich key management features of the Key Management Service (KMS) to provide robust encryption/decryption capabilities for secrets in Kubernetes clusters.</li><li>By using the TKE-KMS plug-in, you can perform KMS encryption on your business credential information stored in clusters to enhance your security.</li></ul></td><td>2020-05-08</td><td>-</td>
</tr>    
</table>



## April 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The TKE console supports multidimensional node filtering and node list export</td><td><ul class="params"><li>Cluster nodes can be filtered based on lock status.</li><li>Cluster nodes can be filtered based on CVM attributes such as node status and IP address.</li><li>Cluster nodes can be exported in batches.</li></ul></td><td>2020-04-22</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30650">Node Overview</a></td>
</tr>
<tr>
	<td>TKE Image Registry can configure a global image lifecycle management policy</td><td>TKE Image Registry adds the image lifecycle management feature, which allows users to configure a global image version clearing policy for the main account and supports independent version clearing policies retained for individual repositories.</td><td>2020-04-16</td><td><a href="https://intl.cloud.tencent.com/document/product/1051/38867">Image Lifecycle Management</a></td>
</tr>
<tr>
    <td>The TKE beta version supports the node pool feature</td><td>The node pool feature can be used in the following scenarios:
		<ul class="params">
		<li>When a cluster contains multiple heterogeneous nodes (different models), node pools can standardize node group management.</li><li>If a cluster needs to scale nodes in or out frequently, node pools can reduce the operation costs.</li><li>If application scheduling rules in a cluster are complex, node pool tags can quickly specify business scheduling rules.</li><li>During routine cluster node maintenance, node pools can conveniently manage Kubernetes and Docker version upgrades.</li></ul></td><td>2020-04-10</td><td>-</td>
</tr>
<tr>
	<td>TKE removes Kubernetes 1.8 as an option</td><td>TKE no longer supports creating clusters using Kubernetes 1.8.</td><td>2020-04-03</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
<tr>
	<td>Upgrades self-deployed cluster master</td><td>You can now use the TKE console to perform rolling updates of Kubernetes masters on self-deployed clusters.</td><td>2020-04-02</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading a Cluster</a></td>
</tr>
</table>

## March 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
	<td>TKE now supports both GlobalRouter and VPC-CNI network modes</td>
	<td>TKE now supports GlobalRouter and VPC-CNI network modes for your business needs. Choose the one that fits your needs.</td>
	<td>2020-03-30</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/38966">How to Choose TKE Network Mode</a></td>
</tr>
<tr>
	<td>TKE has stopped providing features related to TencentHub</td><td>We plan to discontinue support for TencentHub this month, so TKE has officially stopped providing features related to TencentHub and no longer supports related APIs.</td>
	<td>2020-03-25</td><td>-</td>
</tr>
<tr>
    <td>TKE supports enabling "Local Disk Formatting" for BM and big data models</td> <td>TKE now allows you to enable "Local Disk Formatting" for BM and big data model nodes and also allows you to mount and set container directories.</td><td>2020-03-02</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
</table>

## February 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
    <td>TKE cluster scaling groups support node shutdown when scaling in</td> <td>When scaling in, cluster scaling groups now support <b>shutting nodes down instead of terminating or draining them</b>. To enable this feature, <a href="https://console.tencentcloud.com/workorder/category">submit a ticket</a>.</td> <td>2020-02-17</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
<tr>
    <td>TKE fully launches Kubernetes 1.16 and passes <a href="https://github.com/cncf/k8s-conformance/pull/879">conformance verification</a></td><td><ul class="params"><li>Users can create self-deployed clusters and managed clusters of the Kubernetes 1.16 version.</li><li>Users can update a cluster from Kubernetes 1.14 to 1.16.</li></ul></td><td>2020-02-14</td>
    <td><ul  class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading a Cluster</a></li></ul></td>
</table>

## January 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TKE allows users to create clusters using a cluster template</td> <td>The template-based cluster creation feature provides multiple templates for creating managed clusters, self-deployed clusters, and serverless clusters, <b>simplifying the current cluster creation process and improving the cluster creation experience</b>. It applies to various business scenarios such as HA clusters and GPU clusters.</td> <td>2020-01-12</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
</table>

## December 2019

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
	<td>TKE supports the PVs and the PVCs of the Cloud File Storage (CFS) and Cloud Object Storage (COS) types</td>
    <td>TKE supports the PVCs and the PVs of the CFS and COS types <b>connecting storage resources with Kubernetes</b>, which makes it convenient for users to use basic Tencent Cloud products through the native Kubernetes mode and allows users to <b>manage file storage and object storage via PVs and PVCs</b>.</td> <td>2019-12-27</td>
	<td>-</td>
</tr>
<tr>
	<td>Launches beta for TKE Kubernetes 1.16</td>
    <td><li>This allows users to create Kubernetes 1.16 self-deployed clusters and managed clusters via the console.</li><li>It also allows users to upgrade the Kubernetes version of a cluster from 1.14 to 1.16.</li></td> <td>2019-12-18</td>
	<td><ul  class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading a Cluster</a></li></ul></td>
</tr>
<tr>
	<td>TKE supports purchasing multiple data disks during node initialization as well as custom formatting</td>
    <td>TKE allows users to purchase multiple data disks during node initialization and supports custom data disk formatting, allowing users to <b>isolate data</b> and <b>format settings flexibly based on their actual needs</b>.</td> <td>2019-12-12</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding a Node</a></td>
</tr>
<tr>
	<td>TKE nodes support the in-place rolling updates of minor Kubernetes versions</td>
    <td>Nodes in in-place updates support the rolling update mode. <li><b>Only one node is updated at a time, and </b>the next node will be updated only after the current node is successfully updated. </li><li>Currently, in-place updates only support <b>updating different minor versions of the same major version</b>.</li></td> <td>2019-12-03</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading a Cluster</a></td>
</tr>
</table>


## November 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
	<td>Launches beta for TKE custom Hostname</td>
    <td>The TKE custom Hostname feature provides the following advantages: <li><b>Helps clusters interwork with enterprises’ internal domain name service systems.</b></li><li><b>Makes it easier for users to quickly create nodes with a specified Hostname in batches</b>.</li></td>
    <td>2019-11-15</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding a Node</a></td>
</tr>
<tr>
	<td>Releases TKE Ingress performance optimization</td>
    <td>TKE Ingress performance is optimized to better serve users. <li>CLB changes are optimized to <b>allow batch calling APIs to process backend binding.</b></li><li>CVM backend query is optimized to help users <b>avoid unnecessary repeated queries</b>.</li></td>
    <td>2019-11-07</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30673">Basic Ingress Features</a></td>
</tr>
</table>

## October 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>Cluster worker nodes support configuring several security groups simultaneously and using the default security group</td>
    <td>TKE allows <b>a cluster worker node to bind multiple security groups</b> and provides a default security group, helping users <b>quickly configure available security groups</b>.</td>
<td>2019-10-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/9084">TKE Security Group Settings</a></td>
</tr>
<td>Node labels can be added in batches during creation of clusters/nodes</td>
    <td>When a cluster is created or new nodes are added to an existing cluster, TKE allows users to <b>add labels for nodes that run the same business or have the same configurations</b>. The labels help users divide resources, label resource attributes, and filter and batch process massive resource volumes.</td>
<td>2019-10-21</td>
<td>-</td>
</tr>
<tr>
<td>Runtime component Containerd supports the GPU model</td>
    <td>The TKE runtime component Containerd supports the GPU model. When users need to <b>create a GPU application in a cluster, they can choose Containerd as the runtime component</b>.</td>
<td>2019-10-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/31088">How to Choose Containerd and Docker</a></td>
</tr>
<tr>
<td>Launches beta for rolling Kubernetes reinstallation and upgrade of TKE nodes</td>
    <td>TKE <b>supports the batch update of nodes in a cluster from an earlier version to a later version</b>. This feature applies to clusters whose <b>Kubernetes version is outdated and clusters whose nodes do not have relevant custom configurations</b>. Custom configurations will become invalid after the rolling reinstallation and upgrade of nodes.</td>
<td>2019-10-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30640">Upgrading a Cluster</a></td>
</tr>
<tr>
<td>TKE supports GPU monitoring metrics</td>
    <td>TKE supports GPU monitoring metrics, <b>enabling users to monitor GPU-related resources</b>. By checking monitoring data, users can precisely identify specific problems, shorten troubleshooting time, and reduce OPS costs, ensuring the continuous and stable running of businesses.</td>
<td>2019-10-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30691">List of Monitoring and Alarm Metrics</a></td>
</tr>
</table>

## September 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<td>Related APIs of the TKE cluster scaling group have been updated to API 3.0</td>
    <td>TKE APIs have been updated to 3.0 and support all-region access. <b>The new API documentation is more standardized and comprehensive, with unified parameter styles and common error codes. The SDK/CLI version is consistent with the API documentation</b>, providing a simple and convenient user experience.</td>
<td>2019-09-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/51206">CreateClusterAsGroup</a></td>
<tr>
<td>TKE Kubernetes 1.14 is fully launched and has passed conformance verification</td>
    <td>TKE <b>Kubernetes 1.14 is fully launched</b> and has passed conformance verification to ensure that the latest Kubernetes version is available.</td>
<td>2019-09-07</td>
<td><a href="https://github.com/cncf/k8s-conformance/tree/master/v1.14/tencentcloud">Conformance Verification</a></td>
</tr>
<tr>
<td>TKE supports the Tencent Cloud tag, allowing authorization by tag</td>
    <td>If the Tencent Cloud tag is added to a cluster when the cluster is created, <b>the Tencent Cloud services, cloud disks, CLBs, and other resources created in the cluster will automatically inherit the cluster’s tag</b>, allowing users to clearly view resource categories.</td>
<td>2019-09-06</td>
<td>-</td>
</tr>
<tr>
<td>The default instance type for created LoadBalancer-type services is CLB</td>
    <td>When TKE creates a LoadBalancer-type service, the default instance type is CLB.<b> This instance type covers all features of a conventional CLB</b>. <li>The CLB instance type supports the TCP, UDP, HTTP, and HTTPS protocols.</li><li>It provides flexible forwarding capabilities based on domain names and URLs.</li></td>
<td>2019-09-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/214/8847">Instance Types</a></td>
</tr>
<tr>
<td>TKE self-deployed clusters support the separate viewing of Master and Etcd nodes</td>
    <td>This feature allows users to <b>intuitively view the list of all Master and Etcd nodes of a self-deployed cluster and the details of such nodes</b>. Users no longer have trouble distinguishing Master and Etcd nodes in self-deployed clusters.</td>
<td>2019-09-05</td>
<td>-</td>
</tr>
</table>


## August 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>
When a “self-deployed cluster” is created, a security group is automatically bound to the Master node</td>
    <td>This feature can <b>automatically bind an applicable security group to the Master node in a self-deployed cluster</b>. This prevents the Master node from being associated with a security group with communication problems and improves the success rate of creating self-deployed clusters.</td>
<td>2019-08-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
<tr>
<td>TKE supports the visualized display of the cluster creation progress</td>
    <td>The visualized display of the cluster creation progress <b>enables users to see the waiting time for cluster creation and troubleshoot the steps with exceptions</b>. This improves the success rate of cluster creation and ensures the continuous and stable running of businesses.</td>
<td>2019-08-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
</tr>
<tr>
<td>Open source components: <a href="https://github.com/TencentCloud/tencentcloud-cloud-controller-manager">TencentCloud-controller-manager</a> and <a href="https://github.com/TencentCloud/kubernetes-csi-tencentcloud">cbs-csi</a> support Kubernetes 1.14</td>
    <td>The open source components Tencent Cloud-controller-manager and cbs-csi<b> support Kubernetes 1.14</b>.</td>
<td>2019-08-12</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/32430">Open Source Components</a></td>
</tr>
<tr>
<td>Use existing CLB instances to create Ingress</td>
<td>Users no longer have to create new CLB instances in order to create a new Ingress. They can now avoid additional costs by using existing CLB instances to create a new Ingress.</td>
<td>August 8, 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30673">Basic Ingress Features</a></td>
</tr>
<tr>
<td>Launches beta for TKE Kubernetes 1.14</td>
    <td>Users can now use the TKE console to <b>create clusters based on Kubernetes 1.14</b>.</td>
<td>2019-08-04</td>
<td>-</td>
</tr>
<tr>
<td>Related APIs of TKE cluster nodes have been updated to API 3.0
</td>
<td>TKE APIs have been updated to 3.0 and support all-region access. The new API documentation is more standardized and comprehensive, with unified parameter styles and common error codes. The SDK/CLI version is consistent with the API documentation, providing a simple and convenient user experience.</td>
<td>2019-08-04</td>
<td><a href="https://www.tencentcloud.com/document/product/457/6787">API 3.0</a></td>
</tr>
<tr>
<td>TKE now supports application-level log collection</td>
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
<td>The CLB health check failure issue in IPVS mode is fixed</td>
<td>Fixed the compatibility issue between the TLinux kernel and IPVS and fixed the CLB health check failures in IPVS mode.</td>
<td>2019-07-16</td>
<td>-</td>
<tr>
<td>TKE scaling groups support spot models</td>
    <td>When TKE creates a scaling group, users can choose spot instances <b>and purchase pods at a certain discount</b>. However, the system may automatically recall these pods that are sold at a discount.
</td>
<td>2019-07-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/17816">Spot Instances</a></td>
</tr>
<tr>
<td>TKE supports choosing Containerd as the container runtime component</td>
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
<td>Launches beta for VPC-CNI network mode</td>
    <td>TKE provides the VPC-CNI extended network mode, which <b>can assign intra-VPC IP addresses to Pods in a cluster</b>. In the VPC-CNI mode, clusters can create StatefulSet that supports fixed IP address types, and the Pod IP addresses will not change because of restart or migration.</td>
<td>2019-06-29</td>
<td>-</td>
<tr>
<td>Launches beta for StatefulSet with fixed IP addresses</td>
    <td> The StatefulSet with fixed IP addresses help <b>resolve issues related to IP address changes caused by Pod restart or migration</b>. Users can create the StatefulSet with fixed IP addresses for source IP address authorization, IP-based process review, log query based on Pod IP addresses, and other business needs to ensure the continuous and stable running of businesses.</td>
<td>2019-06-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/38974">Managing StatefulSets with Static Pod IP Addresses</a></td>
</tr>
<tr>
<td>TKE uses the new console version by default</td>
    <td>In order to provide a better product user experience, TKE now uses <b>the new Kubernetes-compatible console</b>.</td>
<td>2019-06-17</td>
<td><a href="https://console.cloud.tencent.com/tke2">The New TKE Console</a></td>
</tr>
<tr>
<td>Fixes an issue where cordoning a node while it is being created causes the process to freeze</td>
<td>Fixes an issue where cordoning a node while it is being created causes the process to freeze.</td>
<td>2019-06-13</td>
    <td><a href="https://github.com/kubernetes/kubernetes/pull/69047">pr69047</a></td>
</tr>
<tr>
<td>Fixes an issue where too many secrets results in a pod creation failure</td>
<td>Fixes an issue where too many secrets results in a pod creation failure.</td>
<td>2019-06-13</td>
    <td><a href="https://github.com/kubernetes/kubernetes/pull/74755">pr74755</a></td>
</tr>
<tr>
<td>Launches the new version of the TKE international console</td>
    <td>The new version of the TKE international console adjusts a series of functional modules and <b>provides a native, easier-to-use platform</b>, which helps users resolve environmental issues in development, testing, and OPS, reduce costs, and improve efficiency.</td>
<td>2019-06-05</td>
    <td>TKE International Console</td>
</tr>
<tr>
<td>Managed clusters support configuring ACLs for public network access</td>
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
<td>Nodes in a scaling group tolerate drain failures during automatic scaling in</td>
    <td>When scale-in conditions such as the number of idle nodes are met, the cluster automatically scales in. <b>However, only when all pods of a node are successfully scheduled to other nodes can the pods be drained successfully and scale-in be performed successfully</b>.</td>
<td>2019-05-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
<tr>
<td>Supports registering the TKE network to CCN</td>
    <td>TKE allows users to <b>register existing clusters to CCN, which can manage the container’s network</b>. After the container’s network is registered, you can enable or disable its IP range routing on the CCN side to achieve interconnection between the container’s cluster and the resources in CCN.</td>
<td>2019-05-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/43391">Register Container Clusters with CCN</a></td>
</tr>
<tr>
<td>TKE supports GPU virtualization</td>
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
<td>Launches beta for Docker 18.06</td>
<td>Runtime components that use Docker 18.06 can create clusters.</td>
<td>2019-04-22</td>
<td>-</td>
</tr>
<tr>
<td>The new alarm version is launched and supports all regions</td>
    <td>Alarms enable users to discover exceptions in TKE in a timely manner to ensure business stability and reliability. <b>The new alarm version provides more alarm metrics</b>. We recommend that you configure necessary alarms for all production clusters.</td>
<td>2019-04-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Setting Alarms</a></td>
</tr>
<tr>
<td>Cluster management - Kubernetes online updates - managed master nodes</td>
    <td>In the managed cluster mode, the Master and Etcd nodes of your Kubernetes cluster will be centrally managed and maintained by the Tencent Cloud technical team. <b>The online updates of the Kubernetes version ensure business stability</b>.</td>
<td>2019-04-11</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/457/31417">Cluster Hosting Modes</a></td>
</tr>
<tr>
<td>Self-deployed clusters support Master and Etcd monitoring</td>
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
<td>TKE supports Bare Metal (BM 2.0) nodes</td>
<td>BM physical servers are a type of on-demand pay-as-you-go physical server rental service that provides high-performance and securely isolated physical server clusters for cloud users.</td>
<td>2019-03-28</td>
<td>-</td>
</tr>
<tr>
<td>Users can use a purchased CVM to create clusters</td>
    <td>Using existing CVMs to create clusters helps users <b>reuse existing resources and reduce costs</b>.</td>
<td>2019-03-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30637#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.96.B0.E5.BB.BA.E9.9B.86.E7.BE.A4.3Ca-id.3D.22customclustercreation.22.3E.3C.2Fa.3E">Creating a Cluster</a></td>
</tr>
<tr>
<td>Cluster auto-scaling (CA) supports disabling pod draining</td>
<td>When there are multiple idle nodes in a cluster, scale-in will be triggered. CA supports disabling pod draining.</td>
<td>2019-03-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
</tr>
<tr>
<td>Cluster scaling groups support the scale-out of GPU nodes</td>
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
<td>Release a new monitoring system</td>
    <td>A good monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud TKE. <b>You can collect monitoring data in different dimensions for different resources</b> to quickly understand the resource usage situation and easily locate errors.</td>
<td>2019-02-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
</tr>
<tr>
<td>Self-deployed clusters support Kubernetes 1.12</td>
    <td>Users can now <b>create Kubernetes 1.12 self-deployed clusters</b> in the TKE console.</td>
<td>2019-02-15</td>
<td>-</td>
</tr>
<tr>
<td>Fixes the runC vulnerability CVE-2019-5736</td>
<td>The lightweight container runtime environment runc was found to have a container escape vulnerability, which allowed attackers to overwrite the host runc file (and consequently obtain host root access). This vulnerability has been fixed.</td>
<td>2019-02-13</td>
    <td>-</td>
</tr>
</table>

## January 2019
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>Existing CLBs can be used to create Service</td>
<td>Using existing CLBs to create Service can save resources and help users reduce costs.</td>
<td>2019-01-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/36832">Service Management</a></td>
</tr>
<tr>
<td>Custom images can be used to create clusters</td>
<td>TKE allows users to create custom images based on the basic image provided by TKE and use these custom images to create clusters. To enable this feature, <a href="https://console.tencentcloud.com/workorder/category">submit a ticket </a>to apply.</td>
<td>2019-01-24</td>
    <td>-</td>
</tr>
<tr>
<td>Affinity scheduling can be set during workload creation</td>
    <td>YAML is delivered to the Kubernetes cluster to schedule pods in a workload. <b>The affinity and anti-affinity mechanism of Kubernetes ensures that pods are scheduled according to specific rules</b>.</td>
<td>2019-01-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/457/30668">Setting the Scheduling Rule for a Workload</a></td>
</tr>
<tr>
<td>TKE allows multiple Services to use the same CLB instance</td>
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
	<td>TencentHub supports Helm Chart management</td>
	<td>Helm is a package management tool of Kubernetes. Chart is a collection of files describing Kubernetes resources. Tencent Hub provides an address for users to store Helm Charts.</td>
	<td>2018-12-26</td>
	<td>-</td>
	</tr>
	<tr>
	<td>TKE supports Helm application installation</td>
        <td>Helm is a packaging tool for managing Kubernetes applications. <b>TKE has integrated Helm-related features to visually add, delete, modify, and query Helm Charts in a specified cluster.</b></td>
  <td>2018-12-26</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30683">Helm Application Management</a></td>
	</tr>
	<tr>
	<td>Fixes the privilege escalation vulnerability in Kubernetes</td>
	<td>Tencent Cloud Security Center detected that a severe privilege escalation vulnerability existed in Kubernetes (vulnerability ID: CVE-2018-1002105). This vulnerability has been fixed. Now, TKE can effectively prevent attackers from using the vulnerability to illegally access Kubernetes cluster resources, inducing privilege escalation and initiating malicious requests that ultimately jeopardize the security of the business system.</td>
	<td>2018-12-04</td>
        <td>-</td>
	</tr>
	<tr>
	<td>Removes Kubernetes 1.7.8 as an option for creating clusters</td>
	<td>The entry for creating clusters of Kubernetes 1.7.8 in the console is disabled. To enable it, <a href="https://console.tencentcloud.com/workorder/category">submit a ticket</a>.</td>
	<td>2018-12-04</td>
        <td>-</td>
	</tr>
	<tr>
	<td>pr71415 is merged to fix CVE-2018-1002105</td>
	<td>CVE-2018-1002105 is fixed and backend error responses are processed.</td>
	<td>2018-12-04</td>
        <td><a href="https://github.com/kubernetes/kubernetes/pull/71415">pr71415</a></td>
	</tr>
	<tr>
	<td>Kubelet disables kmem accounting to avoid kernel cgroup leakage</td>
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
	<td>Fixes the kubelet inotify leakage</td>
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
	<td>Launches beta for the new TKE console</td>
        <td>The new TKE console adjusts a series of feature modules to<b> provide you with a native and easy-to-use platform</b>. <b>The new and old consoles are fully compatible in terms of features</b>. Switching consoles will not affect your business. You can use the new console to continue to operate existing clusters.</td>
	<td>2018-10-31</td>
        <td>-</td>
	</tr>
	<tr>
	<td>Service CLB can be bound to specified nodes</td>
	<td>If your cluster is large, you will need to set affinity for entry-type applications to schedule them to certain nodes. You can configure the Service CLB to be bound only to specified nodes.</td>
	<td>2018-10-31</td>
	<td>-</td>
	</tr>
	<tr>
	<td>Conflicts and Pod creation failures caused by the frequent updates of quota statuses by the quota controller are resolved</td>
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
		<td>The default Kubernetes version in TKE is 1.10</td>
		<td>When a new cluster is created, the default Kubernetes version is 1.10. However, you can change the version based on your actual needs.</td>
		<td>2018-09-10</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
	</tr>
	<tr>
		<td>BM clusters support Kubernetes 1.10</td>
		<td>TKE allows users to create BM clusters with Kubernetes 1.10.</td>
		<td>2018-09-10</td>
		<td>-</td>
	</tr>
	<tr>
		<td>BM clusters support Ubuntu 16.04</td>
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
		<td>TKE supports the Russia and India regions</td>
		<td>The TKE console supports the Russia and India regions. You can go to the console to switch to and use these regions.</td>
		<td>2018-07-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE supports private network access to the Master node</td>
		<td>After the private network access entry is enabled, TKE allows private network access to the Master node.</td>
		<td>2018-07-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>The open source component tencentcloud-cloud-controller-manager is released</td>
        <td>This component is the Cloud Controller Manager implementation for TKE <b>and allows the following features to be implemented on the Kubernetes clusters built by Tencent Cloud CVMs</b>:<li>Updates the relevant addresses information of the Kubernetes nodes.</li><li>routecontroller: creates routes within pod IP ranges in a VPC. </li><li>servicecontroller: creates a corresponding CLB when a load balancer-type service is created in a cluster.</li></td>
		<td>2018-07-30</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32430">Open Source Components</a></td>
	</tr>
	<tr>
		<td>The open source component kubernetes-csi-tencentcloud is released</td>
        <td>This component is a plug-in for the Tencent Cloud CBS service and complies with CSI standards. <b>It allows users to use CBS on Kubernetes clusters built by Tencent Cloud CVMs</b>.</td>
		<td>2018-07-30</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32430">Open Source Components</a></td>
	</tr>
	<tr>
		<td>The BM cluster ingress plug-in is released</td>
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
		<td>CCS is renamed TKE</td>
        <td><b>Tencent Kubernetes Engine (TKE) </b>is a highly scalable and high-performance container management service. It allows you to easily run applications on a managed CVM instance cluster.</td>
		<td>2018-06-22</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/6759">Tencent Kubernetes Engine</a></td>
	</tr>
	<tr>
		<td>Cluster auto scaling supports custom configurations</td>
		<td>TKE allows users to customize cluster scaling settings based on their actual needs, making it easier for them to configure businesses flexibly.</td>
		<td>2018-06-22</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
	</tr>
	<tr>
		<td>Node initialization supports the import of scripts</td>
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
		<td>TKE supports BM clusters</td>
		<td>BM container clusters extend Tencent Cloud’s CPM, BM Load Balancer, and other Kubernetes plug-ins, providing a complete set of features such as high-efficient deployment and resource scheduling for containerized applications. This helps industries such as gaming and AI easily cope with the challenges of high-performance computing business scenarios.</td>
		<td>2018-05-01</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE supports GPU clusters</td>
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
		<td>TKE integrates the new Tencent Cloud UI version</td>
		<td>The new Tencent Cloud UI is elegant and easy to use, offering a better container service experience.</td>
		<td>2018-04-01</td>
        <td><a href="https://console.cloud.tencent.com/tke2">TKE Console</a></td>
	</tr>
	<tr>
		<td>TKE now supports all CVM models</td>
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
		<td>TKE supports the auto-scaling of services</td>
        <td>Horizontal Pod Autoscaler (HPA) can <b>automatically scale the number of pods for services according to the average CPU utilization and other metrics of target pods</b>.</td>
		<td>2018-03-01</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32424">Basic Operations of Automatic Scaling</a></td>
	</tr>
	<tr>
		<td>The TKE console interface is updated</td>
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
		<td>TKE supports the auto-scaling of clusters</td>
        <td>Cluster auto scaling <b>adjusts the number of nodes dynamically according to resource demand</b>:<li>If pods become unschedulable due to a lack of resources, the cluster will automatically scale out.</li><li>If there are enough idle nodes, the cluster will automatically scale in to reduce costs.</li></td>
		<td>2018-02-08</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster Scaling</a></td>
	</tr>
	<tr>
		<td>TKE supports log collection</td>
        <td>This feature allows <b>log files from services or specific node paths to be sent to Kafka, Elasticsearch, or CLS</b> so that users can store and analyze them.</td>
		<td>2018-02-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32419">Log Collection</a></td>
	</tr>
	<tr>
		<td>TKE supports application management</td>
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
		<td>Vouchers can be used to purchase cluster nodes</td>
		<td>TKE allows users to use vouchers in their accounts to purchase nodes.</td>
		<td>2017-12-20</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Empty clusters can be created</td>
		<td>This feature allows users to create clusters that do not contain nodes.</td>
		<td>2017-12-20</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Users can set the container directory and the project of the resources when adding existing nodes</td>
		<td><li>Container directory: users can set the directory for storing containers and images. We recommend that they be stored in data disks.</li><li>Project: newly added resources will be automatically assigned to this project.</li></td>
		<td>2017-12-20</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding an Existing Node</a></td>
	</tr>
</table>

## November 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>Cluster reservation policy</td>
        <td><b>Reserves system process resources such as dockerd and kubelet</b>: when a cluster runs the retention policy, certain resources are reserved to ensure the proper running of system processes such as dockerd and kubelet.</td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Cluster draining policy</td>
        <td><b>To ensure that there are sufficient resources for system processes, pods will be drained when necessary</b>.</td>
		<td>2017-11-30</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30654">Draining or Cordoning a Node</a></td>
	</tr>
	<tr>
		<td>Dockerd log rollback</td>
        <td><b>Logs are recycled automatically to ensure that there is sufficient disk space</b>: when log files occupy a certain amount of memory, the log rollback feature will be triggered to automatically recycle logs to ensure that there is sufficient disk space.</td>
		<td>2017-11-30</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Ingress forwarding rules support wildcards</td>
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
		<td>Launches beta for TKE application management feature</td>
        <td>With the rise of micro-service and Devops, users need to deploy and manage multiple services in multiple environments. <b>TKE supports the group management of services via applications</b>, which significantly simplifies service management.</td>
		<td>2017-10-31</td>
		<td>-</td>
	</tr>
	<tr>
		<td>The multi-region deployment of Image Registry supports the new Hong Kong (China) region</td>
        <td>Image Registry is used to store Docker images, which are used to deploy TKE. Each image has a unique ID (the image's repository address + the image name + the image Tag). <b>Image Registry can be deployed in multiple regions, including the Hong Kong (China) region that is now also supported</b>.</td>
		<td>2017-10-31</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1051/38866">Image Registry Overview</a></td>
	</tr>
	<tr>
		<td>The Tencent Cloud international console supports TKE</td>
		<td>The TKE international console is launched, which helps users solve environmental issues in development, testing, and OPS, reduce costs, and improve efficiency.</td>
		<td>2017-10-31</td>
		<td><a href="https://console.cloud.tencent.com/tke2?language=en">TKE International Console</a></td>
	</tr>
</table>

## September 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE Image Registry integrates access permission management</td>
        <td>The address format of a TKE image is as follows: <code>ccr.ccs.tencentyun.com/${namespace}/${name}:${tag}</code>. <b>The following fields are required for configuring the permissions of Image Registry</b>:<li>${namespace}: the namespace of the image repository.</li><li>${name}: the name of the image repository.</li></td>
		<td>2017-09-26</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/11527">TKE Image Registry Resource-level Permission Settings</a></td>
	</tr>
	<tr>
		<td>TKE supports setting labels for services</td>
        <td>TKE supports setting labels for service pods. <b>When searching services, you can filter them by label</b>.</td>
		<td>2017-09-26</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Configuration items can be imported to environment variables</td>
		<td>When deploying a container in a pod, users can import the configuration items ConfigMap and Secret to environment variables.</td>
		<td>2017-09-26</td>
        <td>-</td>
	</tr>
	<tr>
		<td>Clusters support the Project attribute</td>
        <td><li>Clusters are not project-specific, but CVMs, CLBs, and other resources in a cluster are project-specific.</li><li>Project: new resources added to the cluster will be allocated to the project.</li></td>
		<td>2017-09-26</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE supports the Singapore region</td>
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
		<td>TKE integrates the alarm platform</td>
        <td>TKE allows users to set multi-dimensional alarms for clusters to <b>discover cluster exceptions quickly and reduce business risks</b>.</td>
		<td>2017-08-23</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Setting Alarms</a></td>
	</tr>
	<tr>
		<td>TKE clusters support Kubernetes 1.7</td>
        <td>TKE <b>allows users to create clusters with Kubernetes 1.7</b>. </td>
		<td>2017-08-23</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Continuous integration and deployment based on TencentHub</td>
		<td>TencentHub is a management platform created by Tencent Cloud for storing R&D process files and creating DevOps workflows. TencentHub allows users to quickly and conveniently perform operations such as storage, query, and calls for files generated during the full project cycle.</td>
		<td>2017-08-23</td>
        <td>-</td>
	</tr>
	<tr>
		<td>Image Registry adds the trigger feature</td>
        <td>The Image Registry trigger feature allows users to trigger actions such as service update, webhook, and message push after creating an image. <b>The trigger feature can be combined with continuous integration for continuous deployment</b>.</td>
		<td>2017-08-23</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Image Registry supports operation logs</td>
		<td>Operation logs allow users to view image uploads and download records, which helps troubleshoot problems.</td>
		<td>2017-08-23</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Kubectl is used to operate clusters on public networks</td>
        <td>Kubectl is a CLI tool for Kubernetes cluster operations. <b>You can use Kubectl to connect a local client to a TKE cluster</b>.</td>
		<td>2017-08-04</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30639">Connecting to a Cluster</a></td>
	</tr>
	<tr>
		<td>TKE clusters integrate access permission management</td>
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
		<td>TKE supports configuration file management</td>
        <td><li>The configuration file management feature can help you manage the configurations of different businesses under different environments. It supports multiple versions and the YAML format.</li><li>The configuration file supports multiple versions, allowing you to update and roll back applications. </li><li>It also allows you to quickly import configurations, in the form of files, into containers.</li></td>
		<td>2017-07-19</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE supports CI source code building</td>
        <td>Continuous container integration <b>enables the automatic and manual building of container images on the Tencent TKE Platform.</b></td>
		<td>2017-07-18</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Image Registry adds TencentHub images</td>
		<td>Image Registry allows users to view and use TencentHub images.</td>
		<td>2017-07-18</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Image Registry adds "Favorite Public Images"</td>
		<td>"Favorite Public Images" will display the images bookmarked by users, allowing users to query and use specific images.</td>
		<td>2017-07-18</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1051/38866">Image Registry Overview</a></td>
	</tr>
	<tr>
		<td>Image Registry supports multiple namespaces</td>
        <td><b>Image Registry supports the creation of multiple namespaces. The names of namespaces are globally unique. </b>If the namespace name you want to use is already being used by another user, try using another appropriate name.</td>
		<td>2017-07-18</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1051/38866">Creating a Namespace</a></td>
	</tr>
</table>

## June 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE supports NFS volumes</td>
		<td>NFS volumes are used for the persistent storage of data that is read and written many times. They can also be used in scenarios such as big data analysis, media processing, and content management. </td>
		<td>2017-06-24</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30678">Volume Management</a></td>
	</tr>
	<tr>
		<td>TKE supports privileged containers and working directory configurations</td>
        <td><li>A privileged container has a certain priority. </li><li>WorkingDir: specifies the current working directory. If it does not exist, one will be automatically created. If no directory is specified, the default directory when the container runs is used. If workingDir is not specified in the image or through the console, the default workingDir is `/`.</li></td>
		<td>2017-06-24</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE supports cluster capacity</td>
		<td>A cluster is a collection of cloud resources required for running a container, including several CVMs and CLBs. You can run your applications in your cluster.</td>
		<td>2017-06-07</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30635">Cluster Overview</a></td>
	</tr>
	<tr>
		<td>TKE supports auto-formatting data disks and specifying container directories while creating/adding CVMs in container clusters</td>
		<td>If the system disk capacity is small or a server with a data disk needs to format the data disk, you can set the storage directory of the containers and images.</td>
		<td>2017-06-07</td>
        <td><li><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30652">Adding a Node</a></li></td>
	</tr>
	<tr>
		<td>TKE supports service re-deployment</td>
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
		<td>TKE supports adding existing CVMs to container clusters</td>
		<td>TKE allows users to add existing CVMs to container clusters, which helps users reuse existing resources and effectively reduce costs.</td>
        <td>2017-04-27</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30652#.E6.B7.BB.E5.8A.A0.E5.B7.B2.E6.9C.89.E8.8A.82.E7.82.B9">Adding an Existing Node</a></td>
	</tr>
	<tr>
		<td>TKE supports the query of monitoring metrics for instances, services, and clusters</td>
		<td>A good monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud TKE. You can collect monitoring data in different dimensions for different resources to quickly understand the resource usage situation and easily locate errors.</td>
        <td>2017-04-27</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
	</tr>
	<tr>
		<td>TKE supports viewing container logs</td>
		<td>By creating log collection rules, TKE can provide users with log information from within a cluster, making it easier for them to maintain and troubleshoot containers.</td>
        <td>2017-04-27</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32419">Log Collection</a></td>
	</tr>
	<tr>
		<td>The TKE remote terminal supports uploading and downloading files remotely</td>
		<td><ul class="params"><li>When uploading files, you need to specify the file directory.</li><li>When downloading files, you need to specify the file path.</li></ul></td>
        <td>2017-04-19</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/9120">Basic Remote Terminal Operations</a></td>
	</tr>
	<tr>
		<td>TKE supports custom security groups when creating a cluster</td>
        <td>If the current default security group cannot meet your business requirements, you can customize cluster security groups by referring to "Managing Security Group Rules".</td>
        <td>2017-04-19</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a></td>
	</tr>
</table>


## March 2017
<table>
	<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
	<tr>
		<td>TKE allows remote web terminals to log in to containers</td>
        <td>Remote terminals help you debug containers quickly and connect to the containers for troubleshooting. <b>It supports file copy, paste, upload, and download operations, and helps solve the problems of long container login paths and difficult debugging</b>.</td>
        <td>2017-03-15</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/9120">Basic Remote Terminal Operations</a></td>
	</tr>
	<tr>
		<td>TKE supports third-party image creation services</td>
        <td>The third-party image creation service <b>helps users deploy applications flexibly based on their actual business needs</b>.</td>
        <td>2017-03-15</td>
		<td>-</td>
	</tr>
	<tr>
		<td>TKE now supports 7-layer load balancing</td>
        <td>An Ingress is a collection of rules that allow access to services within a cluster. You can configure different forwarding rules to <b>allow different URLs to access different services within the cluster</b>.</td>
        <td>2017-03-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/37013">Ingress Management</a></td>
	</tr>
	<tr>
		<td>Users can query monitoring information about clusters, services, and pods</td>
        <td>A good monitoring environment ensures the high reliability, high availability, and high performance of Tencent Cloud TKE. <b>You can collect monitoring data in different dimensions for different resources </b>to quickly understand the resource usage situation and easily locate errors.</td>
        <td>2017-03-06</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
	</tr>
	<tr>
		<td>TKE supports native Kubernetes APIs, requesting Kubernetes certificates via Tencent Cloud APIs, and all Kubernetes features</td>
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
		<td>Cluster management</td>
		<td>Cluster management supports cluster addition, deletion, modification, and query, VPC-based container clusters, cross-AZ clusters, and open-source native Kubernetes APIs.</td>
        <td>2016-12-26</td>
        <td>-</td>
	</tr>
	<tr>
		<td>Service management</td>
		<td>Service management supports service addition, deletion, modification, and query, the creation of services via private images and official Docker images, and cross-AZ scheduling of services.</td>
        <td>2016-12-26</td>
		<td>-</td>
	</tr>
	<tr>
		<td>Image management</td>
		<td>Image management supports official Docker images, My Images, uploading and downloading private images, and official Docker image acceleration.</td>
        <td>2016-12-26</td>
        <td>-</td>
	</tr>
	<tr>
		<td>Cluster monitoring and container monitoring</td>
		<td>TKE provides the basic monitoring feature for all clusters by default.</td>
        <td>2016-12-26</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/457/30689">Viewing Monitoring Data</a></td>
	</tr>
	<tr>
		<td>Service creation, event updates, and rolling updates for services</td>
		<td>Rolling updates indicate that pods are updated one by one, which allows you to update the service without interrupting your business.</td>
        <td>2016-12-26</td>
		<td>-</td>
	</tr>
</table> 

<style>
	.params{ margin-bottom:0px!important; } 
</style>
