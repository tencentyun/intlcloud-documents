
While using TKE service, you need to consider the service quota applied to TKE, CVM and managed clusters.

### TKE quota

The default TKE quota for each user is as follows. If you want to increase the quota, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
>!From October 21, 2019, the maximum node quota for a singer cluster has been adjusted to at least 5,000.
>

<table>
	<tr>
	<th>Item</th>
	<th>Default Value</th>
	<th>Where to Check</th>
	<th>Allow Increasing</th>
	</tr>
	<tr>
	<td>Clusters in a single region</td>
	<td>5</td>
	<td rowspan=5><a href="https://console.cloud.tencent.com/tke2/overview">Bottom-right section of the TKE overview page</a></td>
	<td rowspan=5>Yes</td>
	</tr>
	<tr>
	<td>Nodes in a single cluster</td>
	<td>5,000</td>
	</tr>
	<tr>
	<td>Image namespaces in a single region</td>
	<td>10</td>
	</tr>
	<tr>
	<td>Image repositories in a single region</td>
	<td>500</td>
	</tr>
	<tr>
	<td>Image tags for a single image</td>
	<td>100</td>
	</tr>
</table>

### CVM quota

CVMs used for TKE are counted into the quota of CVMs. The default quota of CVMs for each user is as follows. You can also refer to [Purchase Limits on CVMs](https://intl.cloud.tencent.com/document/product/213/2664). If you want to increase the quota, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).

<table>
	<tr>
	<th>Item</th>
	<th>Default Value</th>
	<th>Where to Check</th>
	<th>Allow Increasing</th>
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

| Item | IP Address Range | Affected | Where to Check | Allow Modification |
| ----- | ----- | ---- | --------- | ---------- |
| VPC network - Subnet | Custom | Number of nodes in a subnet |[VPC subnet list page for the cluster - Available IP addresses](https://console.cloud.tencent.com/vpc/subnet) | <ul class="params"><li>No</li><li>You can create new subnets</li></ul> |
| Container CIDR block | Custom | <ul class="params"><li>Maximum nodes per cluster</li><li>Maximum services per cluster</li><li>Maximum Pods per node</li></ul> | Basic information page for the cluster - Container IP range | No |

<style>
	.params{margin-bottom:0px !important;}
</style>

### Managed cluster resource quota
>? The following quotas are automatically applied from April 30, 2022 (UTC +8) and cannot be adjusted. **You can increase the resource quota by upgrading the cluster model**.
> [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) if you have special requirements.
>
Run the following command to check the quota:
```
kubectl get resourcequota tke-default-quota -o yaml
```
To check the `tke-default-quota` object of a specified namespace, add `--namespace` to specify the namespace.

>? 
> - **Other Resources** refers to the number of resources in the manged cluster excluding the Pods, nodes and ConfigMap. For example, for a L100 cluster, the number of the resources, such as ClusterRole, Services and Endpoints, **cannot** exceed 10,000 respectively.
- **CRD** refers to **the sum of all CRDs** in the cluster. If the number of some CRDs increases, the number of other CRDs will decrease.

| Cluster Model | Pods | ConfigMap | CRDs/Other Resources | 
| ---------------- | ------------------- | ------------------------- | ------------------- |
| L5             | 600                 | 256                       | 1,250                 |
| L20             | 1,500                | 512                     | 2,500               |
|  L50            | 3,000                | 1,024                    | 5,000              |
|  L100           | 6,000                | 2,048                    |10,000                |
|  L200              | 15,000               | 4,096                   | 20000               |
|  L500        | 30,000               | 6,144                     | 50,000               |
|  L1000            | 90,000               | 8,192                  | 100,000            |
|  L3000             | 150,000              | 10,240                     | 150000              |
|  L5000             | 200,000              | 20,480                    | 200000              |

#### Allocating quota among namespaces
By default, the remaining quota is evenly allocated among all namespaces. You can also create a configmap `tke-quota-config` under `kube-system` to specify the percentage of quota allocated for each namespace respectively.

In the example below, 50% of the remaining quota is allocated to `default`, 40% is allocated to `kube-system`, and 10% is allocated to the rest namespaces. **If the sum of all percentages exceeds 100%, the allocation is considered invalid, and the default even allocation policy is adopted.**
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
