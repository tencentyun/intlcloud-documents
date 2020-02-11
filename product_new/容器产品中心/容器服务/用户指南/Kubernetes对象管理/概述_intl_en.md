## Object Management Instructions

You can operate native Kubernetes objects such as Deployment and DaemonSet in the console.
The Kubernetes objects are persistent entities in clusters and are used to host services running within the clusters. Different Kubernetes objects can represent diffrent entites:
- Running applications
- Resources available to applications
- Policies associated with applications

You can use Kubernetes objects directly in the TKE console or through the Kubernetes APIs such as kubectl.

## Types of Objects

Common Kubernetes objects can be divided into the following types:
- Workloads
    + Deployment: used to manage Pods for which scheduling rules have been specified.
    + StatefulSet: the workload API object used to manage stateful applications.
    + DaemonSet: ensures that all or some nodes run a copy of a Pod, such as a logs collection daemon.
    + Job: creates one or more Pods until the end of run.
    + CronJob: scheduled Job.
- Services
    + Service: a Kubernetes object that provides access to Pod. You can define different types based on your needs.
    + Ingress: a Kubernetes object that manages external access to services in a cluster.
- Configuration
    + ConfigMap: used to store configuration information.
    + Secret: used to store sensitive information such as passwords and tokens.
- Storage
    + Volume: used to store data related to container access.
    + Persistent Volumes (PV): a piece of storage configured in the Kubernetes cluster.
    + PersistentVolumesClaim (PVC): claim for a storage request. If PVs were Pods, then PVCs would be workloads.
    + StorageClass: used to describe the type of storage. When a PVC is created, storage of the specified type, i.e., storage template, is created using StorageClass.

There are dozens of other Kubernetes objects such as Namespace, HPA, and ResourceQuotas. You can use different objects based on your business needs. Available objects vary depending on Kubernetes version. For more information, visit [Kubernetes website](https://kubernetes.io/docs/concepts/).


## Resource Quota

TKE uses ResourceQuota/tke-default-quota to set resource limit for all **managed clusters**. If you need a higher quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1).
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


## Object Management Operations

- Workloads
    + [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662)
    + [StatefulSet Management](https://intl.cloud.tencent.com/document/product/457/30663)
    + [DaemonSet Management](https://intl.cloud.tencent.com/document/product/457/30664)
    + [Job Management](https://intl.cloud.tencent.com/document/product/457/30665)
    + [CronJob Management](https://intl.cloud.tencent.com/document/product/457/30666)
- Services
    + [Service Management](https://intl.cloud.tencent.com/document/product/457/30672)
    + [Ingress Management](https://intl.cloud.tencent.com/document/product/457/30673)
- Configuration
    + [ConfigMap Management](https://intl.cloud.tencent.com/document/product/457/30675)
    + [Secret Management](https://intl.cloud.tencent.com/document/product/457/30676)
- Storage
    + [Volume Management](https://intl.cloud.tencent.com/document/product/457/30678)
    + [PersistentVolume Management](https://intl.cloud.tencent.com/document/product/457/30679)
    + [PersistentVolumesClaim Management](https://intl.cloud.tencent.com/document/product/457/30679)
    + [StorageClass Management](https://intl.cloud.tencent.com/document/product/457/30680)
