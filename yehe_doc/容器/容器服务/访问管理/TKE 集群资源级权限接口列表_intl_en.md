With resource-level permissions, you can specify the resources that a user can operate on. TKE (formerly CCS) supports some resource-level permissions, where for certain TKE operations, you can control the operations that the user is allow to perform (based on the conditions that must be met) or the resources that the user can use.
The following table describes the types of resources that can be authorized in TKE.

| Resource Type | Resource Description Method in the Authorization Policy |
|----|-----|
| Cluster resources | `qcs::ccs:$region::cluster/*` |

The following table describes the TKE (Tencent Kubernetes Engines) API operations that currently support resource-level permissions. You can use the wildcard (*) when specifying a resource path.
>**Notes:**
>Only the TKE API operations listed here support resource-level permissions. You can still authorize a user to perform a TKE API operation that does not support resource-level permissions, but you must specify the resource element in the policy statement with the asterisk (*).

| API Operation | Resource Path |
|-----|-----|
| DescribeClusterService | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| DescribeClusterServiceInfo | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| CreateClusterService | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CLB resource<br>`qcs::clb:$region:$account:clb/*`<br>CBS resource<br>`qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` |
| ModifyClusterService | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CLB resource<br>`qcs::clb:$region:$account:clb/*`<br>CBS resource<br>`qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` |
| DeleteClusterService | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| ModifyServiceDescription | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| DescribeServiceEvent | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| ResumeClusterService | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| PauseClusterService | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| RollBackClusterService | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| ModifyClusterServiceImage | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| RedeployClusterService | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| DescribeServiceInstance | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| ModifyServiceReplicas | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| DeleteInstances | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| DescribeClusterNameSpaces | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| CreateClusterNamespace | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| DeleteClusterNamespace | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| DescribeCluster | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| CreateCluster | CVM resource<br>`qcs::cvm:$region:$account:instance/*` |
| DeleteCluster | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| DescribeClusterInstances | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId` |
| AddClusterInstances | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CVM resource<br>`qcs::cvm:$region:$account:instance/*` |
| DeleteClusterInstances | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CVM resource<br>`qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` |
| AddClusterInstancesFromExistedCvm | Cluster resource<br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CVM resource<br>`qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` |


