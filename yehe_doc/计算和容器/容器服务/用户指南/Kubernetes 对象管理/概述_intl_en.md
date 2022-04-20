## Object Management Instructions

You can operate native Kubernetes objects such as Deployment and DaemonSet in the console.
The Kubernetes objects are persistent entities in clusters and are used to host services running within the clusters. Different Kubernetes objects can represent diffrent entites:
- Running applications
- Resources available to applications
- Policies associated with applications

You can use Kubernetes objects directly in the TKE console or through the Kubernetes APIs such as kubectl.

## Types of Objects

Common Kubernetes objects can be divided into the following types:
<table>
	<tr>
	<th colspan=2>Object Types</th>
	<th>Object Descriptions</th>
	<th>Object Management Operations</th>
	</tr>
	<tr>
	<th rowspan=5>Workload</th>
	<td>Deployment</td>
	<td>Use to manage the Pod of which the scheduling rules are specified.</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30662">Deployment Management</a></td>
	</tr>	
	<tr>
	<td>StatefulSet</td>
	<td>Manage the application workload API object, and the application is stateful.</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30663">StatefulSet Management</a></td>
	</tr>	
		<tr>
	<td>DaemonSet</td>
	<td>Ensure the Pods are running on all or some of the nodes, such as log collection program.</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30664">DaemonSet Management</a></td>
	</tr>
		<tr>
	<td>Job</td>
	<td>One or more Pods are created for one Job, until the end of running.</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30665">Job Management</a></td>
	</tr>
		<tr>
	<td>CronJob</td>
	<td> Job tasks that runs on a regular basis.</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30666">CronJob Management</a></td>
	</tr>
	<tr>
	<th rowspan=2>Sevice</th>
	<td>Service</td>
	<td>A Kubernetes object that provides access to Pod. You can define different types based on your needs.</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/36832">Service Management</a></td>
	</tr>	
	<tr>
	<td>Ingress</td>
	<td>A Kubernetes object that manages external access to services in a cluster.</td>
	<td><a href="https://cloud.tencent.com/document/product/457/56844">Ingress Management</a></td>
	</tr>
		<tr>
	<th rowspan=2>Configuration</th>
	<td>ConfigMap</td>
	<td>Use to store configuration information.</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30675">ConfigMap Management</a></td>
	</tr>	
	<tr>
	<td>Secret </td>
	<td>Use to store sensitive information, such as password and token.</td>
	<td><a href="https://intl.cloud.tencent.com/document/product/457/30676">Secret Management</a></td>
	</tr>	
		<tr>
	<th rowspan=4>Storage</th>
	<td>Volume</td>
	<td>Use to store data related to container access.</td>
	<td rowspan=4><a href="https://intl.cloud.tencent.com/document/product/457/37769">Storage Management</a></td>
	</tr>	
	<tr>
	<td>Persistent Volumes（PV）</td>
	<td>A piece of storage configured in a Kubernetes cluster.</td>
	</tr>	
	<tr>
	<td>Persistent Volumes Claim（PVC）</td>
	<td>A statement of storage request. If you consider a PV as a Pod, then PVC is equivalent to workload.</td>
	</tr>	
	<tr>
	<td>StorageClass</td>
	<td>Use to describe the type of storage. When a PVC is created, storage of the specified type, i.e., storage template, is created using StorageClass.</td>
	</tr>	
</table>

There are dozens of other Kubernetes objects such as Namespace, HPA, and ResourceQuotas. You can use different objects based on your business needs. Available objects vary depending on Kubernetes version. For more information, visit [Kubernetes website](https://kubernetes.io/docs/concepts/).


## Resource Quota

TKE applies the following resource limits to all **managed clusters** by using ResourceQuota/tke-default-quota. If you need more quota, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to apply.
<table>
	<tr>
	<th rowspan=2>Cluster Size</th>
	<th colspan=2>Quota</th>
	</tr>
	<tr>
	<th>Pod</th>
	<th>ConfigMap</th>	
	<tr>
	<td>Number of nodes ≤ 5</td>
	<td>4000</td>
	<td>3000</td>
	</tr>	
	<tr>
	<td>5 < Number of nodes ≤ 20 </td>
	<td>8000</td>
	<td>6000</td>
	</tr>	
	<tr>
	<td>Number of nodes > 20</td>
	<td>None</td>
	<td>None</td>
	</tr>
</table>


