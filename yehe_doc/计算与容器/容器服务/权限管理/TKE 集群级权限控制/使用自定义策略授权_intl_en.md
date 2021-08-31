This document describes how to configure custom policies in Tencent Kubernetes Engine (TKE) and grant sub-accounts specific permissions. Reference this document to create custom policies that best fit your business requirements.




## Policy Syntax Description
The following figure shows the structure of the policy syntax.
![](https://main.qcloudimg.com/raw/dc57207bdbf095ad1b499f0b5acaef57.png)

- **action**: indicates an API.
- **resource**: indicates a resource.

>? You can define the policy syntax on your own, or create a custom policy by using the policy generator in CAM. You can configure a custom policy based on the following example.
>- [Configuring a Sub-account's Administrative Permissions for a Single TKE Cluster](https://intl.cloud.tencent.com/document/product/457/30702)
>- [Use tags to grant full permissions for a batch of clusters to a sub-account](https://intl.cloud.tencent.com/document/product/457/37483)



## Configuring TKE API Permissions
This section describes multiple features, their sub-features, corresponding Tencent Cloud APIs, APIs for indirect calls, resource levels for permission control, and Action fields of clusters and node modules.

### Cluster modules

The following table describes the mappings between features and APIs.

<table>
	<tr>
	<th>&nbsp;&nbsp;Feature&nbsp;</th><th>Sub-feature</th> <th>Corresponding Tencent Cloud API</th> <th>API for Indirect Calls</th><th>Resource Level for Permission Control</th> <th>Action Field</th>
	</tr>
	<tr>
	<td>Creating an empty cluster</td>
        <td><ul class="params"><li>Selecting a Kubernetes version</li><li>Selecting a runtime component</li><li>Selecting a VPC</li><li>Setting a container network</li><li>Selecting a custom image</li><li>Setting IPVS</li></ul></td>
    <td rowspan=5>tke:CreateCluster</td>
    <td>cam:GetRole
account:DescribeUserData
account:DescribeWhiteList
tag:GetTagKeys
cvm:GetVmConfigQuota
vpc:DescribeVpcEx
cvm:DescribeImages</td>
<td><ul class="params"><li>API-level permissions are required for creating a cluster.</li><li>VPC-level permissions are required for obtaining a VPC list.</li></ul></td>
    <td>"tke:CreateCluster",
"cam:GetRole",
"tag:GetTagKeys",
"cvm:GetVmConfigQuota",
"vpc:DescribeVpcEx",
"cvm:DescribeImages"</td>
	</tr>
	<tr>
	<td>Using an existing CVM to create a managed cluster</td>
    <td><ul class="params"><li>Creating an empty cluster to include features</li><li>Using an existing CVM as a node</li><li>Mounting a security group</li><li>Mounting a data disk</li><li>Enabling automatic adjustment</li></ul></td>
    <td>cvm:DescribeInstances
vpc:DescribeSubnetEx
cvm:DescribeSecurityGroups
vpc:DescribeVpcEx
cvm:DescribeImages
cvm:ResetInstance
cvm:DescribeKeyPairs</td>
<td><ul class="params"><li>API-level permissions are required for creating a cluster.</li><li>CVM-level permissions are required for obtaining a CVM list.</li></ul></td>
    <td>"tke:CreateCluster",
"cvm:DescribeInstances",
"vpc:DescribeSubnetEx",
"cvm:DescribeSecurityGroups",
"vpc:DescribeVpcEx",
"cvm:DescribeImages",
"cvm:ResetInstance",
"cvm:DescribeKeyPairs"</td>
	</tr>
	<tr>
	<td>Using an existing CVM to create a self-deployed cluster</td>
        <td><ul class="params"><li>Creating an empty cluster to include features</li><li>Using an existing CVM as a node</li><li>Using an existing CVM as Control Plane & ETCD</li><li>Mounting a security group</li><li>Mounting a data disk</li><li>Enabling automatic adjustment</li></ul></td>
    <td>cvm:DescribeInstances
vpc:DescribeSubnetEx
cvm:DescribeSecurityGroups
vpc:DescribeVpcEx
cvm:DescribeImages
cvm:ResetInstance
cvm:DescribeKeyPairs</td>
        <td><ul class="params"><li>API-level permissions are required for creating a cluster.</li><li>VPC-level permissions are required for obtaining a VPC list.</li><li>CVM-level permissions are required for obtaining a CVM list.</li></ul></td>
    <td>"tke:CreateCluster",
"cvm:DescribeInstances",
"vpc:DescribeSubnetEx",
"cvm:DescribeSecurityGroups",
"vpc:DescribeVpcEx",
"cvm:DescribeImages",
"cvm:ResetInstance",
"cvm:DescribeKeyPairs"</td>
	</tr>
	<tr>
	<td>Automatically creating a CVM to create a managed cluster</td>
        <td><ul class="params"><li>Creating an empty cluster to include features</li><li>Purchasing a CVM as a node</li><li>Mounting a security group</li><li>Mounting a data disk</li><li>Enabling automatic adjustment</li></ul></td>
    <td>cvm:DescribeSecurityGroups
cvm:DescribeKeyPairs
cvm:RunInstances
vpc:DescribeSubnetEx
vpc:DescribeVpcEx
cvm:DescribeImages</td>
<td><ul class="params"><li>API-level permissions are required for creating a cluster.</li><li>VPC-level permissions are required for obtaining a VPC list.</li></ul></td>
    <td>"cvm:DescribeSecurityGroups",
"cvm:DescribeKeyPairs",
"cvm:RunInstances",
"vpc:DescribeSubnetEx",
"vpc:DescribeVpcEx",
"cvm:DescribeImages",
"tke:CreateCluster"</td>
</tr>
	<tr>
	<td>Automatically creating a CVM to create a self-deployed cluster</td>
        <td><ul class="params"><li>Creating an empty cluster to include features</li><li>Purchasing a CVM as a node</li><li>Purchasing a CVM as Control Plane & ETCD</li><li>Mounting a security group</li><li>Mounting a data disk</li><li>Enabling automatic adjustment</li></ul></td>
    <td>cvm:DescribeSecurityGroups
cvm:DescribeKeyPairs
cvm:RunInstances
vpc:DescribeSubnetEx
vpc:DescribeVpcEx
cvm:DescribeImages</td>
<td><ul class="params"><li>API-level permissions are required for creating a cluster.</li><li>VPC-level permissions are required for obtaining a VPC list.</li></ul></td>
    <td>"cvm:DescribeSecurityGroups",
"cvm:DescribeKeyPairs",
"cvm:RunInstances",
"vpc:DescribeSubnetEx",
"vpc:DescribeVpcEx",
"cvm:DescribeImages",
"tke:CreateCluster"</td>
	</tr>
	<tr>
	<td>Querying a cluster list</td>
	<td>-</td>
    <td>tke:DescribeClusters</td>
    <td>-</td>
    <td>Cluster-level permissions are required for obtaining a cluster list.</td>
    <td>"tke:DescribeClusters"</td>
	</tr>
	<tr>
	<td>Displaying cluster credentials</td>
	<td>-</td>
    <td>tke:DescribeClusterSecurity</td>
    <td>-</td>
    <td>Cluster-level permissions are required for displaying cluster credentials.</td>
    <td>"tke:DescribeClusterSecurity"</td>
	</tr>
	<tr>
	<td>Enabling/Disabling the private network/Internet access URL of a cluster</td>
        <td><ul class="params"><li>Creating an Internet access port for a managed cluster</li><li>Creating a cluster access port</li><li>Modifying security policies for the Internet access port of a managed cluster</li><li>Querying the Internet access port enabling status of a managed cluster</li><li>Deleting the Internet access port of a managed cluster</li><li>Deleting a cluster access port</li></ul></td>
        <td>tke:CreateClusterEndpointVip
            tke:CreateClusterEndpoint
            tke:ModifyClusterEndpointSP
            tke:DescribeClusterEndpointVipStatus
            tke:DescribeClusterEndpointStatus
            tke:DeleteClusterEndpointVip
            tke:DeleteClusterEndpoint
        </td>
    <td>-</td>
    <td>Cluster-level permissions are required for enabling or disabling cluster access.</td>
    <td>-</td>
	</tr>
	<tr>
	<td>Deleting a cluster</td>
	<td>-</td>
    <td>tke:DeleteCluster</td>
    <td>tke:DescribeClusterInstances
        tke:DescribeInstancesVersion
        tke:DescribeClusterStatus</td>
    <td>Cluster-level permissions are required for deleting a cluster.</td>
    <td>"tke:DescribeClusterInstances",
"tke:DescribeInstancesVersion",
"tke:DescribeClusterStatus",
"tke:DeleteCluster"</td>
	</tr>
</table> 



### Node modules

The following table describes the mappings between features and APIs.

<table>
	<tr>
	<th>&nbsp;&nbsp;Feature&nbsp;</th><th>Sub-feature</th> <th>Corresponding Tencent API</th> <th>API for Indirect Calls</th><th>Resource Level for Permission Control</th> <th>Action Field</th>
	</tr>
	<tr>
	<td>Adding an existing node</td>
	<td><ul class="params"><li>Adding an existing node to a cluster</li><li>Resetting a data disk</li><li>Setting a security group</li></ul></td>
    <td>tke:AddExistedInstances</td>
    <td>cvm:DescribeInstances
vpc:DescribeSubnetEx
cvm:DescribeSecurityGroups
vpc:DescribeVpcEx
cvm:DescribeImages
cvm:ResetInstance
cvm:DescribeKeyPairs
cvm:ModifyInstancesAttribute		    
tke:DescribeClusters</td>
<td><ul class="params"><li>Cluster-level permissions are required for adding an existing node.</li><li>CVM-level permissions are required for obtaining a CVM list.</li></ul></td>
    <td>"cvm:DescribeInstances",
"vpc:DescribeSubnetEx",
"cvm:DescribeSecurityGroups",
"vpc:DescribeVpcEx",
"cvm:DescribeImages",
"cvm:ResetInstance",
"cvm:DescribeKeyPairs",
"tke:DescribeClusters",
"tke:AddExistedInstances"</td>
	</tr>
	<tr>
	<td>Creating a node</td>
	<td><ul class="params"><li>Creating a node and adding it to a cluster</li><li>Resetting a data disk</li><li>Setting a security group</li></ul></td>
    <td>tke:CreateClusterInstances</td>
    <td>cvm:DescribeSecurityGroups
cvm:DescribeKeyPairs
cvm:RunInstances
vpc:DescribeSubnetEx
vpc:DescribeVpcEx
cvm:DescribeImages
tke:DescribeClusters</td>
    <td>Cluster-level permissions are required for creating a node.</td>
    <td>"cvm:DescribeSecurityGroups",
"cvm:DescribeKeyPairs",
"cvm:RunInstances",
"vpc:DescribeSubnetEx",
"vpc:DescribeVpcEx",
"cvm:DescribeImages",
"tke:DescribeClusters"</td>
	</tr>
	<tr>
	<td>Node list</td>
	<td>Viewing a cluster node list</td>
    <td>tke:DescribeClusterInstances</td>
    <td>cvm:DescribeInstances
tke:DescribeClusters</td>
<td><ul class="params"><li>Cluster-level permissions are required for viewing a node list.</li><li>CVM-level permissions are required for obtaining a CVM list.</li></ul></td>
    <td>"cvm:DescribeInstances",
"tke:DescribeClusters",
"tke:DescribeClusterInstances"</td>
	</tr>
	<tr>
	<td>Deleting a node</td>
	<td>-</td>
    <td>tke:DeleteClusterInstances</td>
    <td>cvm:TerminateInstances
tke:DescribeClusters</td>
        <td><ul class="params"><li>Cluster-level permissions are required for viewing a node list.</li><li>CVM-level permissions are required for obtaining a CVM list.</li><li>The termination policy of a node is required for terminating the node.</li></ul></td>
    <td>"cvm:TerminateInstances",
"tke:DescribeClusters",
"tke:DeleteClusterInstances"</td>
	</tr>
</table>


<style>
	.params{margin:0px !important}
</style>
