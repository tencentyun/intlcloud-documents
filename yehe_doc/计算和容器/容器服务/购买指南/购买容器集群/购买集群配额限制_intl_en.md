
The quota limits include TKE quota limits, CVM quota limits and managed cluster resource quota limits. The details are as follows:

### TKE quota limits

The default TKE quota for each user is as follows. If you want to increase the quota, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
>!From October 21, 2019, the maximum node quota for user clusters has been adjusted to 5000 if the quota was less than 5000.
>

<table>
	<tr>
	<th>Quota Item</th>
	<th>Default Value</th>
	<th>Where to Check</th>
	<th>Support Quota Increase</th>
	</tr>
	<tr>
	<td>Clusters in a single region</td>
	<td>5</td>
	<td rowspan=5><a href="https://console.cloud.tencent.com/tke2/overview">Bottom-right section of the TKE overview page</a></td>
	<td rowspan=5>Yes</td>
	</tr>
	<tr>
	<td>Nodes in a single cluster</td>
	<td>5000</td>
	</tr>
	<tr>
	<td>Image namespaces in a single region</td>
	<td>10</td>
	</tr>
	<tr>
	<td>Image repository in a single region</td>
	<td>500</td>
	</tr>
	<tr>
	<td>Image tags for a single image</td>
	<td>100</td>
	</tr>
</table>

### CVM quota limits

You should abide by the purchase limits when you purchase CVMs. For details, please see [Purchase Limits on CVMs](https://intl.cloud.tencent.com/document/product/213/2664). The default quota of CVMs for each user is as follows. If you want to increase the quota, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).

<table>
	<tr>
	<th>Quota Item</th>
	<th>Default Value</th>
	<th>Where to Check</th>
	<th>Support Quota Increase</th>
	</tr>
	<tr>
    <td>Pay-as-you-go CVMs in a single availability zone</td>
	<td>30 or 60 CVMs</td>
	<td><a href="https://console.cloud.tencent.com/cvm/overview">CVM Instances page - Resources in each region</a></td>
	<td>Yes</td>
	</tr>
</table>


### Cluster configuration limits
>?Cluster configuration limits the cluster size and cannot be modified currently.
>

| Configuration Item | IP Address Range | Affected Item | Where to Check | Support Modification |
| ----- | ----- | ---- | --------- | ---------- |
| VPC network - Subnet | Custom | Number of nodes that can be added |[VPC subnet list page for the cluster - Available IP addresses](https://console.cloud.tencent.com/vpc/subnet) | <ul class="params"><li>No</li><li>You can create new subnets</li></ul> |
| CIDR block of the container IP range | Custom | <ul class="params"><li>Maximum nodes per cluster</li><li>Maximum services per cluster</li><li>Maximum Pods per node</li></ul> | Basic information page for the cluster - Container IP range | No |

<style>
	.params{margin-bottom:0px !important;}
</style>

### Instructions on K8s resource quota
>? The following quota takes effect from April 30, 2022 (UTC +8) and cannot be removed. **You can increase the resource quota by upgrading the cluster specification**.
> You can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to apply to increase the quota.
>
You can run the following command to check the quota:
```
kubectl get resourcequota tke-default-quota -o yaml
```
If you need to view the `tke-default-quota` object of a specified namespace, please add the `--namespace` option to specify the namespace.

>? 
> - “Other K8s resources limits” refers to that the number of the K8s resources in the cluster excluding the Pods, nodes and ConfigMap **cannot** exceed the limit. For example, if the cluster specification is L100, the number of the K8s resources such as ClusterRole, Service and Endpoint **cannot** exceed 10000.
- “CRD limits” refers to **the sum of all CRDs** in the cluster cannot exceed the limit. If the number of some CRDs increases, the number of other CRDs will decrease.

| Cluster Specification | Pod Limits | ConfigMap Limits | CRD/Other K8s Resources Limits | 
| ---------------- | ------------------- | ------------------------- | ------------------- |
| L5             | 600                 | 256                       | 1250                 |
| L20             | 1500                | 512                     | 2500               |
|  L50            | 3000                | 1024                    | 5000              |
|  L100           | 6000                | 2048                    |10000                |
|  L200              | 15000               | 4096                   | 20000               |
|  L500        | 30000               | 6144                     | 50000               |
|  L1000            | 90000               | 8192                  | 100000            |
|  L3000             | 150000              | 10240                     | 150000              |
|  L5000             | 200000              | 20480                    | 200000              |

#### Allocating quota among namespaces
The **balance** (**Balance = Quota - Used part**) is evenly allocated among all namespaces by default. If you want to customize the allocation, you can create a configmap `tke-quota-config` under `kube-system` to specify the percentage of **balance** allocated among all namespaces.

In the sample below, 50% of the **balance** is allocated to the `default` namespace, 40% of the **balance** is allocated to the `kube-system`namespace, and 10% of the **balance** is allocated among other namespaces. **If the sum of all percentages exceeds 100%, the allocation is invalid and all the quota will be allocated evenly among all namespaces**.
```
apiVersion: v1
data:
  default: "50"
  kube-system: "40"
kind: ConfigMap
metadata:
  name: tke-quota-config
  namespace: kube-system
```
