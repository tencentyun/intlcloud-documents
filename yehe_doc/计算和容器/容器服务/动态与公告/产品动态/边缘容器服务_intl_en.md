## September 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
  <td>边缘集群添加腾讯云带 GPU 的边缘节点</td><td>边缘集群添加腾讯云带 GPU 的边缘节点，添加 GPU 版本和操作系统版本的说明。</td><td>2021-09-06</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35386">节点管理 </a></td>
</tr>  
</table>

## July 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
  <td>TKE Edge 增强边缘集群安全特性</td><td>优化边缘节点权限，添加节点脚本支持配置 ttl 过期时间。</td><td>2021-06-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35386">节点管理 </a></td>
</tr>  
</table>

## April 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
  <td>支持 statefulsetGrid 应用和灰度升级功能</td><td>后端升级支持 YAML 命令行方式管理 statefulsetGrid 和灰度升级。</td><td>2021-04-27</td><td><a href="https://cloud.tencent.com/document/product/457/50417">通过 yaml 使用 ServiceGroup 功能 </a></td>
</tr>  
</table>


## March 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
  <td>TKE Edge 支持自定义参数创建集群</td><td>TKE Edge 支持自定义参数创建集群，支持指定自定义 K8S 集群相关参数，支持指定单节点 Pod 数量上限。</td><td>2021-03-26</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35385">创建集群 </a></td>
</tr>  
</table>

## January 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Added support for the OPS management of edge cluster.</td><td>The OPS management of edge cluster is supported. User can configure, overview, and search the log, audit, and event information.</td><td>2021-01-30</td><td><a href="https://cloud.tencent.com/document/product/457/32090">OPS Center</a></td>
</tr>
<tr>
    <td>Added support for using TCR image repository.</td><td>User can select TCR image repository when creating edge applications and workloads.</td><td>2021-01-19</td><td><a href="https://intl.cloud.tencent.com/document/product/457/36838">Using a Container Image in a TCR Enterprise Instance to Create a Workload</a></td>
</tr>
<tr>
    <td>Added support for configuring alarms in Cloud Monitor.</td><td>TKE Edge alarming is supported by Cloud Monitor. User can configure alarm policies for TKE Edge in Cloud Monitor.</td><td>2021-01-18</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30688">Overview of Monitoring and Alarms</a></td>
</tr>
<tr>
<td>Added support for the creation of CVM node.</td><td>CVM node can be purchased for edge cluster.</td><td>2021-01-13</td><td>-</a></td>
</tr>
</table>


## December 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
  <td>TKE Edge opens source for SuperEdge.</td><td>SuperEdge is an edge container management system based on the native Kubernetes. Tencent Cloud has provided the edge-related source code in the TKE Edge for the SuperEdge open source project.</td><td>2020-12-19</td><td><a href="https://github.com/superedge/superedge">SuperEdge GitHub </a></td>
</tr>  
</table>


## November 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>ServiceGroup 功能产品化</td><td>用户可通过控制台使用 ServiceGroup 功能，功能入口与集群“节点管理”入口平级。</td><td>2020-11-27</td><td><li><a href="https://intl.cloud.tencent.com/document/product/457/37772">ServiceGroup 功能概述</a></li><li><a href="https://cloud.tencent.com/document/product/457/50417">通过 yaml 使用 ServiceGroup 功能</a></li><li><a href="https://cloud.tencent.com/document/product/457/50418">通过控制台使用 ServiceGroup 功能</a></li></td>
</tr>
<tr>
    <td>The node installation script supports “check” and “clear” parameters.</td><td><li>The “check” parameter is convenient for users to use scripts to manually check where the installation requirements are not met in the node environment.</li><li>The “clear” parameter is convenient for one-click cleaning of dirty data in the node, turning off the firewall, etc.</li></td><td>2020-11-13</td><td>-</td>
</tr>
<tr>
    <td>Edge DNS solution was launched.</td><td>The edge DNS solution will no longer occupy 53 port of the nodes.</td><td>2020-11-4</td><td>-</a></td>
</tr>
</table>

## October 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Added support for multi-architecture hybrid management.</td><td>Users can manage the nodes in both ARM and X86 CPU architectures within a cluster at the same time.</td><td>2020-10-28</td><td>-</td>
</tr>
<tr>
    <td>Added support for edge Pod HPA.</td><td>The feature of Edge Pod HPA was launched, while the native Kubernetes HPA feature is also available on the edge.</td><td>2020-10-23</td><td><a href="https://intl.cloud.tencent.com/document/product/457/38858">Utilizing HPA to Implement Auto Scaling of Business on TKE</a></td>
</tr>
<tr>
    <td>Upgraded feature of using script to add node.</td><td>Users can use the same script to add self-owned nodes to the cluster multiple times (the script validity is 1 hour), making it convenient to add self-owned nodes in batches.</td><td>2020-10-22</td><td>-</a></td>
</tr>
</table>


## September 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Users can enable edge health feature on the console.</td><td>The "Enable Edge Health" switch is added to the basic information page of the edge cluster. Users can enable or disable this feature based on actual needs.</td><td>2020-09-28</td><td>-</a></td>
</tr>
<tr>
    <td>Added support for ECM security groups.</td><td>When purchasing ECM resources on the TKE Edge console, users can select the node security group for security management.</td><td>2020-09-24</td><td>-</td>
</tr>
<tr>
    <td>The permission convergence of edge node is launched.</td><td>This feature is automatically enabled, and can effectively prevent malicious users from disrupting the normal operation of the system through edge nodes.</td><td>2020-09-15</td><td>-</td>
</tr>
</table>

## August 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Edge cluster is available in Beijing region.</td><td>Users can create edge clusters in Beijing region.</td><td>2020-08-28</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35385">Creating a Cluster</a></td>
</tr><tr>
    <td>The node installation script is optimized.</td><td>The node installation script can automatically obtain the default ENI.</td><td>2020-08-12</td><td>-</td>
</tr>
<tr>
    <td>The Pod access mode is added.</td><td>Pods can access Apiserver in incluster mode.</td><td>2020-08-05</td><td>-</td>
</tr>
</table>

## July 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The application market, Helm Chart, and assembly line now support TKE Edge.</td><td>Users can create apps directly or with application market, and use assembly line with TKE Edge.</td><td>2020-07-06</td><td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/37706">Application Market</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30682">Application Overview</a></li></ul></td>
</tr>
<tr>
    <td>Users can customize the node initialization script.</td><td><ul class="params"><li>Node initialization operations include mounting a data disk, creating directories, and so on.</li><li>The script is run only once during node initialization.</li></ul></td><td>2020-07-01</td><td>-</td>
</tr>
<tr>
    <td>Users can obtain the metrics of all pods in the cluster via the apiserver.</td><td><ul class="params"><li>Users can obtain the metrics of all cluster pods in the cluster(if any) by requesting the api-server.</li><li>In such cases, a monitoring component should be deployed in the cluster.</li></ul></td><td>2020-07-01</td><td>-</td>
</tr>
</table>

## June 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TKE Edge supports GPU.</td><td>Currently, TKE Edge supports the NVIDIA Tesla (T4, P40, M40, P4, and V100) GPU models.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>The TKE Edge image acceleration feature is launched for beta testing.</td><td>The launch time of big-image pods is shortened by 30%, and the public traffic consumption for pulling images is reduced to 1/n (n: the number of nodes in the same LAN) of the original traffic consumption.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>TKE Edge supports custom parameters.</td><td><ul class="params"><li>Supports custom node initialization scripts.</li><li>Supports custom container directories.</li><li>Supports custom node max-pod.</li></ul></td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>TKE Edge supports Kubernetes v1.18.2.</td><td>Supports the creation of Kubernetes v1.18.2 clusters.</td><td>2020-06-01</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35385">Creating Edge Clusters</a></td>
</tr>
</table>

## March 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TKE Edge is launched.</td><td>TKE Edge is a container system that manages edge cloud resources from the central cloud. You can use it to manage distributed nodes in the same cluster across multiple regions. TKE Edge is fully compatible with native Kubernetes, supports one-click app delivery, and provides edge autonomy and distributed health checks.</td><td>2020-03-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35390">Tencent Kubernetes Engine for Edge</a></td>
</tr>
</table>


<style>
	.params{margin:0px !important}
</style>
