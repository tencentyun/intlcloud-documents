When you use Tencent Kubernetes Engine (TKE), you need to authorize services to use relevant cloud resources. Each scenario usually contains policies that are defined for different roles in advance. The main roles involved are `TKE_QCSRole` and `IPAMDofTKE_QCSRole`. This document introduces the details of each authorization policy, and the authorization scenarios and authorization steps for each role.


<span id="TKE_QCSRole"></span>
## TKE_QCSRole

After TKE is activated, Tencent Cloud grants your account the permissions of the role `TKE_QCSRole`, which is associated with multiple preset policies by default. To obtain relevant permissions, you need to perform the corresponding preset policy authorization operations in specific authorization scenarios. After these operations are completed, the corresponding policy will appear in the role’s list of authorized policies. The preset policies associated with `TKE_QCSRole` by default include:

- [`QcloudAccessForTKERole`](#QcloudAccessForTKERole): the permission for TKE to access cloud resources
- [`QcloudAccessForTKERoleInOpsManagement`](#QcloudAccessForTKERoleInOpsManagement): the permission for OPS management, including the log service
- [`QcloudAccessForTKERoleInCreatingCFSStorageclass`](#QcloudAccessForTKERoleInCreatingCFSStorageclass): the permission for TKE to operate on Cloud File Storage (CFS), including adding/deleting/querying CFS systems, and querying the mount targets of a file system.
- [`QcloudCVMFinanceAccess`](#QcloudCVMFinanceAccess): CVM finance permission





<span id="QcloudAccessForTKERole"></span>
### Preset policy QcloudAccessForTKERole

#### Authorization scenario
When you log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) for the first time after registering and logging in to a Tencent Cloud account, you need to go to the “Cloud Access Management” page to grant the current account TKE permissions for operating on CVMs, CLBs, CBS, and other cloud resources.

<span id="Step"></span>
#### Authorization steps
1. Log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar. The **Service Authorization** window is displayed.
2. Click **Go to Cloud Access Management** to go to the role management page.
3. Click **Grant Authorization** and complete identity verification to complete authorization.

#### Permission content
- CVM issues
<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>cvm:DescribeInstances</code></td>
<td>Querying the list of server instances</td>
</tr>
<tr>
<td><code>cvm:*Cbs*</code></td>
<td>CBS-related permissions</td>
</tr>
</tbody></table>
- Tag issues
<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>tag:*</code></td>
<td>All features related to tags</td>
</tr>
</tbody></table>
- CLB issues
<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>clb:*</code></td>
<td>All features related to CLB</td>
</tr>
</tbody></table>
- TKE issues
<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>ccs:DescribeCluster</code></td>
<td>Querying the cluster list</td>
</tr>
<tr>
<td><code>ccs:DescribeClusterInstances</code></td>
<td>Querying cluster node information</td>
</tr>
</tbody></table>

<span id="QcloudAccessForTKERoleInOpsManagement"></span>
### Preset policy QcloudAccessForTKERoleInOpsManagement

#### Authorization scenario
This policy is associated with `TKE_QCSRole` by default. After TKE is activated and `TKE_QCSRole` is granted, you have the permissions of various OPS-related features, including log features.



#### Authorization steps

This policy and the [preset policy QcloudAccessForTKERole](#QcloudAccessForTKERole) are authorized at the same time, so no extra operation is needed.

#### Permission content
Log service issues

<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>cls:listTopic</code></td>
<td>Displaying the list of log topics under a specified logset</td>
</tr>
<tr>
<td><code>cls:getTopic</code></td>
<td>Viewing log topic information</td>
</tr>
<tr>
<td><code>cls:createTopic</code></td>
<td>Creating a log topic</td>
</tr>
<tr>
<td><code>cls:modifyTopic</code></td>
<td>Modifying a log topic</td>
</tr>
<tr>
<td><code>cls:deleteTopic</code></td>
<td>Deleting a log topic</td>
</tr>
<tr>
<td><code>cls:listLogset</code></td>
<td>Displaying the logset list</td>
</tr>
<tr>
<td><code>cls:getLogset</code></td>
<td>Viewing logset information</td>
</tr>
<tr>
<td><code>cls:createLogset</code></td>
<td>Creating a logset</td>
</tr>
<tr>
<td><code>cls:modifyLogset</code></td>
<td>Modifying a logset</td>
</tr>
<tr>
<td><code>cls:deleteLogset</code></td>
<td>Deleting a logset</td>
</tr>
<tr>
<td><code>cls:listMachineGroup</code></td>
<td>Displaying the server group list</td>
</tr>
<tr>
<td><code>cls:getMachineGroup</code></td>
<td>Viewing server group information</td>
</tr>
<tr>
<td><code>cls:createMachineGroup</code></td>
<td>Creating a server group</td>
</tr>
<tr>
<td><code>cls:modifyMachineGroup</code></td>
<td>Modifying a server group</td>
</tr>
<tr>
<td><code>cls:deleteMachineGroup</code></td>
<td>Deleting a server group</td>
</tr>
<tr>
<td><code>cls:getMachineStatus</code></td>
<td>Viewing server group status</td>
</tr>
<tr>
<td><code>cls:pushLog</code></td>
<td>Uploading logs</td>
</tr>
<tr>
<td><code>cls:searchLog</code></td>
<td>Querying logs</td>
</tr>
<tr>
<td><code>cls:downloadLog</code></td>
<td>Downloading logs</td>
</tr>
<tr>
<td><code>cls:getCursor</code></td>
<td>Getting the cursor based on time</td>
</tr>
<tr>
<td><code>cls:getIndex</code></td>
<td>Viewing indexes</td>
</tr>
<tr>
<td><code>cls:modifyIndex</code></td>
<td>Modifying indexes</td>
</tr>
<tr>
<td><code>cls:agentHeartBeat</code></td>
<td>Heartbeat</td>
</tr>
<tr>
<td><code>cls:getConfig</code></td>
<td>Getting the pusher configuration information</td>
</tr>
</tbody></table>

<span id="QcloudAccessForTKERoleInCreatingCFSStorageclass"></span>
### Preset policy QcloudAccessForTKERoleInCreatingCFSStorageclass

#### Authorization scenario
The Tencent Cloud CFS add-on can help you use file storage in TKE clusters. When using this add-on for the first time, you need to authorize relevant resources, such as file systems in CFS, via TKE.

#### Authorization steps

1. Log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and select **Add-ons** in the left sidebar to go to the “Add-On” management page.
2. On the top of the “Add-On” page, select the region and the cluster, and click **Create**.
3. On the “Create an Add-On” page, if the add-on selected for the first time is “CFS”, click **Service Authorization** at the bottom of the page.
4. In the displayed "Service Authorization" window, click **Cloud Access Management**.
5. On the "Role Management" page, click **Grant Authorization** and complete identity verification to complete authorization.

#### Permission content
File storage issues
<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody><tr>
<td>cfs:CreateCfsFileSystem</td>
<td>Creating a file system</td>
</tr>
<tr>
<td>cfs:DescribeCfsFileSystems</td>
<td>Querying a file system</td>
</tr>
<tr>
<td>cfs:DescribeMountTargets</td>
<td>Querying mount targets of a file system</td>
</tr>
<tr>
<td>cfs:DeleteCfsFileSystem</td>
<td>Deleting a file system</td>
</tr>
</tbody></table>

<span id="QcloudCVMFinanceAccess"></span>
### Preset policy QcloudCVMFinanceAccess

#### Authorization scenario

When you need to purchase a cloud disk using monthly subscription, you need to add this policy to `TKE_QCSRole` to configure payment permission. Otherwise, creation of a PVC based on a monthly subscription storageclass may fail due to lack of payment permission.

#### Authorization steps
1. Log in to the CAM console, and select **[Roles]**(https://console.cloud.tencent.com/cam/role) in the left sidebar.
2. On the "Role" list page, click **TKE_QCSRole** to enter the role management page.
3. Choose **Associate Policy** on the “TKE_QCSRole” page, and confirm the operation in the displayed “Risk Warning” window.
4. In the displayed “Associate Policy” window, find the policy `QcloudCVMFinanceAccess` and select it.
5. Click **OK** to complete the authorization.


#### Permission content

<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>finance:*</code></td>
<td>CVM finance permission</td>
</tr>
</tbody></table>



## IPAMDofTKE_QCSRole

`IPAMDofTKE_QCSRole` is the TKE IPAMD support service role. After the permissions of this role are granted, you need to associate preset policies in the authorization scenarios described in this document. After these operations are completed, the following policies will appear in the list of authorized policies of the role:

[`QcloudAccessForIPAMDofTKERole`](#QcloudAccessForIPAMDofTKERole): the permission for TKE IPAMD to access cloud resources

<span id="QcloudAccessForIPAMDofTKERole"></span>

### Preset policy QcloudAccessForIPAMDofTKERole

#### Authorization scenario

When using the VPC-CNI network mode for the first time to create a cluster, you need to first grant permission for TKE IPAMD to access cloud resources, so that you can use the VPC-CNI network mode normally.

#### Authorization steps

1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. On the "Cluster Management" page, click **Create** or **Template Creation** above the cluster list.
3. On the "Create a Cluster" page, in the step where you configure "Cluster Information", select **VPC-CNI** in "Container Network Plug-In", and click "Service Authorization".
4. In the displayed "Service Authorization" window, click **Go to Cloud Access Management**.
5. On the "Role Management" page, click **Grant Authorization** and complete identity verification to complete authorization.


#### Permission content

- CVM issues
<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>cvm:DescribeInstances</code></td>
<td>Viewing the list of instances</td>
</tr>
</tbody></table>
- Tag issues
<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>tag:GetResourcesByTags</code></td>
<td>Querying the resource list by tag</td>
</tr>
<tr>
<td><code>tag:ModifyResourceTags</code></td>
<td>Batch modifying tags associated with a resource</td>
</tr>
<tr>
<td><code>tag:GetResourceTagsByResourceIds</code></td>
<td>Querying tags associated with a resource</td>
</tr>
</tbody></table>
- VPC issues
<table>
<thead>
<tr>
<th width="50%">Permission Name</th>
<th width="50%">Permission Description</th>
</tr>
</thead>
<tbody><tr>
<td><code>vpc:DescribeSubnet</code></td>
<td>Querying the list of subnets</td>
</tr>
<tr>
<td><code>vpc:CreateNetworkInterface</code></td>
<td>Creating an ENI</td>
</tr>
<tr>
<td><code>vpc:DescribeNetworkInterfaces</code></td>
<td>Querying the list of ENIs</td>
</tr>
<tr>
<td><code>vpc:AttachNetworkInterfac</code>e</td>
<td>Binding an ENI with a CVM</td>
</tr>
<tr>
<td><code>vpc:DetachNetworkInterface</code></td>
<td>Unbinding an ENI from a CVM</td>
</tr>
<tr>
<td><code>vpc:DeleteNetworkInterface</code></td>
<td>Deleting an ENI</td>
</tr>
<tr>
<td><code>vpc:AssignPrivateIpAddresses</code></td>
<td>Applying for private IP addresses for an ENI</td>
</tr>
<tr>
<td><code>vpc:UnassignPrivateIpAddresses</code></td>
<td>Returning the private IP addresses of an ENI</td>
</tr>
<tr>
<td><code>vpc:MigratePrivateIpAddress</code></td>
<td>Migrating the private IP addresses of an ENI</td>
</tr>
<tr>
<td><code>vpc:DescribeSubnetEx</code></td>
<td>Querying the list of subnets</td>
</tr>
<tr>
<td><code>vpc:DescribeVpcEx</code></td>
<td>Querying peering connection</td>
</tr>
<tr>
<td><code>vpc:DescribeNetworkInterfaceLimit</code></td>
<td>Querying the ENI quota</td>
</tr>
<tr>
<td><code>vpc:DescribeVpcPrivateIpAddresses</code></td>
<td>Querying the private IP address of a VPC</td>
</tr>
</tbody></table>


