## May 2022
<table >
<th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> 
<tr>
  <td style="word-wrap:break-word;word-break:break-all;">
   Edge cluster supports ServiceGroup
  </td>
  <td style="word-wrap:break-word;word-break:break-all;">
  ServiceGroup makes it easy to deploy a set of services in different data centers or regions in the same cluster. It also allows requests between services to be completed within the same data center or region, avoiding cross-region access to services.
  </td><td>2022-05-18</td><td style="word-wrap:break-word;word-break:break-all;">-</a></td>
</tr>
</table>

## April 2022
<table >
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
  <td style="word-wrap:break-word;word-break:break-all;">Cluster resource quota adjustment</td><td style="word-wrap:break-word;word-break:break-all;">Edge cluster automatically applies a set of resource quotas to namespaces in clusters with no more than five nodes (0 < nodeNum ≤5) and clusters with more than five and fewer than 20 nodes (5 < nodeNum < 20). You cannot adjust the quotas as they will protect the cluster control plane from instability caused by potential bugs in an application after it is deployed in the cluster.</td><td>2022-04-29</td><td style="word-wrap:break-word;word-break:break-all;">-</a></td>
</tr>
<tr>
  <td style="word-wrap:break-word;word-break:break-all;">Cross-region service access</td><td style="word-wrap:break-word;word-break:break-all;">Edge cluster allows Pods in different edge regions to access services in different regions.</td><td>2022-04-29</td><td style="word-wrap:break-word;word-break:break-all;">-</a></td>
</tr>
</table>

## March 2022
<table >
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
<td style="word-wrap:break-word;word-break:break-all;">Edge cluster supports edge node pool management and group management of node pools</td><td style="word-wrap:break-word;word-break:break-all;">Edge cluster supports edge node pool management and group management of node pools. This update reconstructs the UI interaction between the earlier versions of NodeGroup and NodeUnit. Clusters created after March 29, 2022 will use the new interaction logic, and clusters on earlier versions will not be affected.</td><td>2022-03-29</td><td style="word-wrap:break-word;word-break:break-all;">-</a></td>
</tr>
</table>


## February 2022
<table >
<tr>
<th style="width:15%">Update</th>	
<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	
<th style="width:15%">Documentation</th> 
</tr>
<tr>
  <td>Edge cluster supports edge node-ENI binding</td><td style="word-wrap:break-word;word-break:break-all;">Edge cluster supports binding ENI to Pods on CVM edge nodes to implement a high-availability network scheme.</td><td>2021-02-10</td><td>-</a></td>
</tr>  
<tr>
  <td>Edge cluster supports remote login to edge nodes</td><td style="word-wrap:break-word;word-break:break-all;">Edge cluster supports remote login to edge nodes in both the public and private networks.</td><td>2021-02-10</td><td>-</a></td>
</tr>
</table>


## November 2021
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
  <td>Enhances the feature development in edge cluster</td><td>Edge cluster supports edge node-Pod connection, Kubernetes 1.20 features, and StatefulsetGrid/Headless service.</td><td>2021-11-06</td><td><a href="https://intl.cloud.tencent.com/zh/document/product/457/35385">Edge Cluster Guide</a></td>
</tr>  
</table>

## September 2021
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
  <td>Edge cluster adds Tencent Cloud edge nodes with GPU</td><td>Edge cluster adds Tencent Cloud edge nodes with GPU as well as GPU version and OS version description.</td><td>2021-09-06</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35386">Node Management</a></td>
</tr>  
</table>

## June 2021
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
  <td>TKE Edge enhances the security features of edge clusters</td><td>Edge node permissions are optimized and node scripts are added to support the configuration of TTL expiration time.</td><td>2021-06-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35386">Node Management</a></td>
</tr>  
</table>

## April 2021
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
  <td>Adds support for StatefulsetGrid application and grayscale upgrade</td><td>Backend upgrade supports StatefulsetGrid management in YAML command line mode and grayscale upgrade.</td><td>2021-04-27</td><td></a></td>
</tr>  
</table>



## March 2021
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
  <td>TKE Edge supports using custom parameters to create clusters</td><td>TKE Edge supports using custom parameters to create clusters, specifying custom related parameters for K8s clusters, and specifying the maximum number of Pods per node.</td><td>2021-03-26</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35385">Creating a Cluster</a></td>
</tr>  
</table>

## January 2021
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
    <td>Adds support for the Ops management of edge cluster</td><td>The Ops management of edge cluster is supported. Users can configure, overview, and search the log, audit, and event information.</td><td>2021-01-30</td><td><a href="https://intl.cloud.tencent.com/zh/document/product/457/38428">Cluster Ops</a></td>
</tr>
<tr>
    <td>Adds support for using TCR image repository</td><td>You can select TCR image repository when creating edge applications and workloads.</td><td>2021-01-19</td><td><a href="https://intl.cloud.tencent.com/document/product/457/36838">Using a Container Image in a TCR Enterprise Instance to Create a Workload</a></td>
</tr>
<tr>
    <td>Adds support for configuring alarms in Cloud Monitor</td><td>Edge clusters can be connected to Cloud Monitor for alarm policy configuration.</td><td>2021-01-18</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
</tr>
<tr>
<td>Adds support for the creation of CVM node</td><td>CVM node can be purchased for edge cluster.</td><td>2021-01-13</td><td>-</a></td>
</tr>
</table>


## December 2020
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
  <td>TKE Edge opens source for SuperEdge</td><td>SuperEdge is an edge container management system based on the native Kubernetes. Tencent Cloud has provided the edge-related source code in the TKE Edge for the SuperEdge open-source project.</td><td>2020-12-19</td><td><a href="https://github.com/superedge/superedge">SuperEdge </a></td>
</tr>  
</table>


## November 2020
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
    <td>Launches the ServiceGroup feature as a product</td><td>You can use the ServiceGroup feature in the console, whose feature entry is at the same level as that of cluster node management.</td><td>2020-11-27</td><td>-</li></td>
</tr>
<tr>
    <td>The node installation script supports "check" and "clear" parameters</td><td><li>The "check" parameter is convenient for you to use scripts to manually check where the installation requirements are not met in the node environment.</li><li>The "clear" parameter is convenient for quick cleaning of dirty data in the node, disabling the firewall, etc.</li></td><td>2020-11-13</td><td>-</td>
</tr>
<tr>
    <td>Launches the edge DNS solution</td><td>The edge DNS solution will no longer occupy port 53 of the node.</td><td>2020-11-4</td><td>-</a></td>
</tr
</table>



## October 2020
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
    <td>Adds support for multi-architecture hybrid management</td><td>You can manage the nodes in both ARM and x86 CPU architectures within a cluster.</td><td>2020-10-28</td><td>-</td>
</tr>
<tr>
    <td>Adds support for edge Pod HPA</td><td>The feature of edge Pod HPA is launched, while the native Kubernetes HPA feature is also available on the edge.</td><td>2020-10-23</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38858">Utilizing HPA to Auto Scale Businesses on TKE</a></td>
</tr>
<tr>
    <td>Upgrades the feature of using script to add a node</td><td>You can use the same script to add self-owned nodes to a cluster multiple times (the script validity is one hour), making it convenient to add self-owned nodes in batches.</td><td>2020-10-22</td><td>-</a></td>
</tr>
</table>


## September 2020
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
    <td>Supports enabling Edge Health in the console</td><td>The **Enable Edge Health** switch is added to the **Basic Information** page of the edge cluster. You can enable or disable it as needed.</td><td>2020-09-28</td><td>-</a></td>
</tr>
<tr>
    <td>Adds support for ECM security groups</td><td>When purchasing ECM resources in the TKE Edge console, you can select the node security group for security management.</td><td>2020-09-24</td><td>-</td>
</tr>
<tr>
    <td>Launches the permission convergence solution of edge nodes</td><td>This feature is automatically enabled and can effectively prevent malicious users from disrupting the normal operation of the system through edge nodes.</td><td>2020-09-15</td><td>-</td>
</tr>
</table>

## August 2020
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
    <td>Edge cluster is available in Beijing region</td><td>You can create edge clusters in Beijing region.</td><td>2020-08-28</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35385">Creating a Cluster</a></td>
</tr><tr>
    <td>Optimizes the node installation script</td><td>The node installation script can automatically obtain the default ENI.</td><td>2020-08-12</td><td>-</td>
</tr>
<tr>
    <td>Adds the Pod access mode</td><td>Pods can access the API server in incluster mode.</td><td>2020-08-05</td><td>-</td>
</tr>
</table>

## July 2020
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
    <td>The marketplace, Helm chart, and pipeline supports TKE Edge</td>	<td>You can create applications directly or through the marketplace, and use the pipeline with TKE Edge.</td><td>2020-07-06</td><td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/37706">Application Market</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30682"> Overview</a></li></ul></td>
</tr>
<tr>
    <td>Supports customizing the node initialization script</td>	<td><ul class="params"><li>Node initialization operations include mounting a data disk and creating a directory.</li><li>The script is run only once during node initialization.</li></ul></td><td>2020-07-01</td><td>-</td>
</tr>
<tr>
    <td>Supports getting the metric data of all Pods in the cluster via the API server</td>	<td><ul class="params"><li>You can get the metrics (if any) of all Pods in the cluster by requesting the API server.</li><li>In such cases, a monitoring add-on should be deployed in the cluster.</li></ul></td><td>2020-07-01</td><td>-</td>
</tr>
</table>

## June 2020
<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
    <td>TKE Edge supports GPU</td><td>Currently, TKE Edge supports the NVIDIA Tesla (T4, P40, M40, P4, and V100) GPU models.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>Launches the TKE Edge image acceleration feature for beta testing</td><td>The launch time of big-image Pods is shortened by 30%, and the public traffic consumption for pulling images is reduced to 1/n (n: the number of nodes in the same LAN) of the original consumption.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>TKE Edge supports custom parameters</td><td><ul class="params"><li>Supports custom node initialization scripts.</li><li>Supports custom container directories.</li><li>Supports custom node max-pod.</li></ul></td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>TKE Edge supports Kubernetes v1.18.2</td>	<td>Supports the creation of Kubernetes v1.18.2 clusters.</td><td>2020-06-01</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35385">Creating a Cluster</a></td>
</tr>
</table>

## March 2020

<table>
<tr><th style="width:20%">Update</th>	<th style="width:50%">Description</th> 
<th style="width:15%">Date</th>	<th style="width:15%">Documentation</th> </tr>
<tr>
    <td>Launches TKE Edge</td><td>TKE Edge is a container system that manages edge cloud resources from the central cloud. It can be used to manage distributed nodes in the same cluster across multiple regions. It is fully compatible with native Kubernetes, supports quick application delivery, and provides edge autonomy and distributed health checks.</td><td>2020-03-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35390">Tencent Kubernetes Engine for Edge</a></td>
</tr>
</table>


<style>
	.params{margin:0px !important}
</style>
