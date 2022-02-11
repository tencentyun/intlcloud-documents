## July 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Supports creation of container instance</td><td>Container instance is a service model launched by Elastic Kubernetes Service that allows users to deploy container applications without the need to purchase servers or deploy K8s clusters.</td><td>2021-07-14</td><td>Container instance</td>
</tr>
</table>


## May 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr> 
    <td>Supports automatic allocation of EIP for Pods when they are created.</td><td>The EIP can be automatically allocated for Pod when it is created. Pod no longer strongly relies on NAT gateway for public network communication.</td><td>2021-05-28</td><td>-</td>
</tr>
<tr> 
    <td>Supports modifying the custom DNS of the virtual node.</td><td>Users can modify the custom DNS of the virtual node. After modification, the Pods scheduled to this virtual node will adopts this DNS configuration by default.</td><td>2021-05-26</td><td><a href="https://intl.cloud.tencent.com/document/product/457/39759">Virtual Node Overview</a></td>
</tr>
<tr> 
    <td>Elastic cluster supports log collection via CRD configuration.</td><td>Users can use the Custom Resource Definitions (CRD) to configure log collection for the Elastic cluster. CRD is non-intrusive to Pod and supports a variety of log parsing methods. It sends standard output and file logs in the container to Tencent Cloud CLS, which provides search and analysis, visual application, log download and consumption, and other services. It is recommended to use CRD to configure log collection.</td><td>2021-05-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/40585">Using a CRD to Configure Log Collection</a></td>
</tr>
</table>


## March 2021
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>EKS has connected to Tencent Cloud Tags.</td><td>Users can add Tencent Cloud tag to EKS cluster, and manage bills through tags.</td><td>2021-03-20</td><td>-</td>
</tr>
</table>

## December 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Supports spot instance.</td><td>The spot instance costs are 20% of the original cost, which is expected to reduce business costs by 65%.</td><td>2020-12-25</td><td>-</td>
</tr>
<tr>
    <td>Event dashboard was launched.</td><td>This feature supports the multi-dimensional statistics of top events, exception events, etc. and supports aggregation search and trend observation.</td><td>2020-12-08</td><td>Event Dashboard</a></td>
</tr>
</table>

## November 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The event storage feature was added.</td><td>Users can observe resource change and locate the problem in time.</td><td>2020-11-26</td><td><a href="https://intl.cloud.tencent.com/document/product/457/30686">Event Storage</a></td>
</tr>
</table>

## August 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Pod Event completion</td><td>The Pod Event is aligned with the native K8S, making the K8S cluster running events more abundant and locating problems in Pod operation more convenient.</td><td>2020-08-15</td><td>-</td>
</tr>
</table>


## July 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Supports binding Pods with CAM roles.</td><td>Users can bind Pods with CAM roles to obtain the permission policies owned by the roles.</td><td>2020-07-22</td><td><a href="https://intl.cloud.tencent.com/document/product/457/11542">Permission Management</a></td>
</tr>
<tr>
    <td>Supports static IP addresses of Pods.</td><td>The IP addresses of Pods can remain unchanged when the StatefulSet/Bare Pod updates its workload.</td><td>2020-07-15</td><td>-</td>
</tr>
<tr>
    <td>Supports Pod login.</td><td>Users can use the console or run kubectl exec -it to remotely log in to a Pod.</td><td>2020-07-01</td><td>-</td>
</tr>
<tr>
    <td>Supports third-party image repositories.</td><td>When creating a workload, users can select images from third-party image repositories and set the image repository access credential.</td><td>2020-07-01</td><td>-</td>
</tr>
</table>

## June 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The EKS console provides a command line window for interaction with containers.</td><td>This feature improves the user experience and helps you quickly identify issues.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>Supports updates of StatefulSets and Pods without changing their IP addresses.</td><td>This feature enhances service stability and simplifies service network management.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>LoadBalancer supports IPv6.</td><td>The service IP address supports the IPv6 network.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>EKS supports the purchase of Tencent’s self-developed Star Lake servers.</td><td>Tencent’s self-developed Star Lake servers provide reliable, secure, and stable high performance at low costs.</td><td>2020-06-18</td><td><a href="https://intl.cloud.tencent.com/document/product/457/34057">Resource Specifications</a></td>
</tr>
<tr>
    <td>EKS was fully launched.</td><td>EKS is a service mode launched by Tencent Cloud TKE that allows users to deploy workloads without having to purchase nodes.</td><td>2020-06-01</td><td><a href="https://intl.cloud.tencent.com/document/product/457/34040">Elastic Kubernetes Service</a></td>
</tr>
</table>

## December 2019

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
<td>Elastic Kubernetes Service (EKS) beta is launched. </td><td>EKS <b>allows users to deploy workloads without having to purchase nodes</b>. <b>It is fully compatible with native Kubernetes</b> and supports resource purchase and management in the native mode. Resources are billed based on the amount of resources used by the containers.</td> <td>2019-12-27</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/34040">Elastic Kubernetes Service</a></td>
</tr>
</table>
