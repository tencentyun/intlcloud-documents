Resource-level permission refers to the ability to specify which resources can be operated by a user. TKE (formerly CCS) supports certain resource-level permissions, which means that for certain TKE operations, you can control when the user is allowed to perform operations (based on conditions that must be met) or use specific resources.
Types of resources that can be authorized in TKE include:

| Resource type | Resource description method in authorization policy |
|----|-----|
| Cluster-related | `qcs::ccs:$region::cluster/*` |

The table below describes the TKE API operations that currently support resource-level permissions. When specifying a resource path, you can use the "*" wildcard in the path.
>**Note:**
>TKE API operations not listed in the table do not support resource-level permissions. Even if a TKE API operation does not support resource-level permissions, you can still grant the permissions for the operation to the user, but you must specify * for the resource element of the policy statement.

| API operation | Resource path |
|-----|-----|
|DescribeClusterService| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|DescribeClusterServiceInfo| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|CreateClusterService| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CLB resource <br>`qcs::clb:$region:$account:clb/*`<br>CBS resource <br>`qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`|
|ModifyClusterService| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CLB resource <br>`qcs::clb:$region:$account:clb/*`<br>CBS resource <br>`qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`|
|DeleteClusterService| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|ModifyServiceDescription| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|DescribeServiceEvent| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|ResumeClusterService| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|PauseClusterService| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|RollBackClusterService| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|ModifyClusterServiceImage| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|RedeployClusterService| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|DescribeServiceInstance| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|ModifyServiceReplicas| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|DeleteInstances| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|DescribeClusterNameSpaces| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|CreateClusterNamespace| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|DeleteClusterNamespace| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|DescribeCluster| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|CreateCluster| CVM resource <br>`qcs::cvm:$region:$account:instance/*`|
|DeleteCluster| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|DescribeClusterInstances| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`|
|AddClusterInstances| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CVM resource <br>`qcs::cvm:$region:$account:instance/*`|
|DeleteClusterInstances| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CVM resource <br>`qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`|
|AddClusterInstancesFromExistedCvm| Cluster resource <br>`qcs::ccs:region:account:cluster/*`<br>`qcs::ccs:region:account:cluster/$clusterId`<br>CVM resource <br>`qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`|


