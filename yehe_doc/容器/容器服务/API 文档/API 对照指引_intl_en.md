**[Tencent Kubernetes Engine (TKE) API 2.0](https://intl.cloud.tencent.com/document/product/457/9458) is being deprecated at the end of March 2020. Please use [TKE API 3.0](https://intl.cloud.tencent.com/document/product/457/32029) instead. 3.0 further standardizes interface definition and reduces access latency. The following is a reference table that shows the relationships between modules in the 2.0 and 3.0 APIs.

> Part of the TKE API 3.0 and Kubernetes API documentation will be released soon. Keep an eye on our documentation pages for changes.

<table>
	<tr><th colspan=2>Module</th><th>API 2.0</th><th>API 3.0</th></tr>
	<tr>
		<td rowspan=20 colspan=2>Cluster</td>
		<td>Creates a cluster (CreateCluster)</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32027">Creates a cluster (CreateCluster)</a></td>
	</tr>
	<tr>
		<td>Deletes a cluster (DeleteCluster)</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33870">Deletes a cluster (DeleteCluster)</a></td>
	</tr>
	<tr>
		<td>Queries a list of clusters (DescribeCluster)</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32025">Queries a list of clusters (DescribeCluster)</a></td>
	</tr>
	<tr>
		<td>Adds nodes to a cluster (AddClusterInstances)</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33862">Adds nodes to a cluster (AddClusterInstances)</a></td>
	</tr>
	<tr>
		<td>Adds existing CVM instances to a cluster (AddClusterInstancesFromExistedCvm)</td>
		<td>Adds existing instances to a cluster (AddExistedInstances)</td>
	</tr>
	<tr>
		<td>Deletes nodes from a cluster (DeleteClusterInstances)</td>
		<td>Deletes nodes from a cluster (DeleteClusterInstances)</td>
	</tr>
	<tr>
		<td>Queries a list of nodes in a cluster (DescribeClusterInstances)</td>
		<td>Queries a list of nodes in a cluster and their details (DescribeClusterInstances)</td>
	</tr>
	<tr>
		<td>Queries information on access to a cluster from a public network (DescribeClusterSecurityInfo)</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33865">Queries information on access to a cluster and related security settings (DescribeClusterSecurity)</a></td>
	</tr>
	<tr>
		<td>Verifies the CIDR block (CheckClusterCIDR)</td>
		<td>Checks to see if the CIDR block conflicts with the CIDR blocks of existing clusters (CheckClusterCIDR)</td>
	</tr>
	<tr>
		<td>Queries a list of instances in a cluster (DescribeExistedCvmForAddClusterInstances)</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33861">Queries a list of existing nodes (DescribeExistedInstances)</a></td>
	</tr>
	<tr>
		<td>Queries cluster Request and Limit information (DescribeClusterRequestLimitInfo)</td>
		<td rowspan=2>Kubernetes APIs</td>
	</tr>
	<tr>
			<td>Modifies node label (ModifyClusterNodeLabel)</td>
	</tr>
	<tr>
		<td>Modifies cluster attributes (ModifyClusterAttributes)</td>
		<td rowspan=2>Modifies cluster attributes (ModifyClusterAttribute)</td>
	</tr>
	<tr>
		<td>Modifies the project to which the cluster belongs (ModifyProjectId)</td>
	</tr>
	<tr>
		<td>Modifies cluster namespace description (ModifyNamespaceDescription)</td>
		<td>Kubernetes API</td>
	</tr>
	<tr>
		<td><ul class="params"><li>Creates or removes cluster VIP (OperateClusterVip)</li><li>Queries async task result (DescribeClusterTaskResult)</li></td>
		<td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/33871">Creates managed cluster public network access port (CreateClusterEndpointVip)</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/33868">Deletes managed cluster public network access port (DeleteClusterEndpointVip)</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/33866">Queries the status of the managed cluster public network access port (DescribeClusterEndpointVipStatus)</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/33864">Modifies the security group to which the managed cluster public network access port belongs (ModifyClusterEndpointSP)</a></li></ul></td>
	</tr>
	<tr>
		<td>Drains cluster nodes (DrainClusterNode)</td>
		<td>Drains nodes (DrainClusterNode)</td>
	</tr>
	<tr>
		<td>Modifies the schedulable setting of a cluster node (ModifyClusterNodeSchedulable)</td>
		<td>Kubernetes API</a></td>
	</tr>
	<tr>
		<td>Adds private third-party image hub (AddHubInfo)</td>
		<td rowspan=2>Deprecated</td>
	</tr>
	<tr>
		<td>Queries cluster third-party image hub (DescribeHubInfo)</td>
	</tr>
	<tr>
		<td rowspan=9  colspan=2>Cluster Auto Scaling</td>
		<td>Creates a cluster auto scaling group (CreateClusterAsg)</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33852">Creates an auto scaling group for the cluster (CreateClusterAsGroup)</a></td>
	</tr>
	<tr>
		<td>Enables a cluster auto scaling group (EnableClusterAsg)</td>
		<td>Modifies the attributes of a cluster auto scaling group (ModifyClusterAsGroupAttribute)</td>
	</tr>
	<tr>
		<td>Queries a list of cluster auto scaling groups (DescribeClusterAsg)</td>
	 <td>Queries a list of auto scaling groups associated with the cluster (DescribeClusterAsGroups)</td>
	</tr>
	<tr>
		<td>Modifies the scale down setting of a cluster auto scaling group (ModifyClusterAsgScaleDown)</td>
	 <td>Modifies the scaling attribute of a cluster auto scaling group (ModifyClusterAsGroupOptionAttribute)</td>
	</tr>
	<tr>
		<td>Modifies the label of a cluster auto scaling group (ModifyClusterAsgLabel)</td>
	 <td rowspan=3>Deprecated</td>
	</tr>
	<tr>
		<td>Resets the label of a cluster auto scaling group (ResetClusterAsgLabel)</td>
	<tr>
		<td>Deletes the label of a cluster auto scaling group (DeleteClusterAsgLabel)</td>
	</tr>
	</tr>
	<tr>
		<td>Disables a cluster auto scaling group (DisableClusterAsg)</td>
		<td>Modifies the attributes of a cluster auto scaling group (ModifyClusterAsGroupAttribute)</td>
	</tr>
	<tr>
		<td>Deletes a cluster auto scaling group (DeleteClusterAsg)</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33851">Deletes a cluster auto scaling group (DeleteClusterAsGroups)</a></td>
	</tr>
	<tr>
		<td rowspan=14  colspan=2>Service</td>
		<td>Creates a cluster service (CreateClusterService)</td>
		<td rowspan=25>Kubernetes API</td>
	</tr>
	<tr>
		<td>Queries a list of cluster services (DescribeClusterService)</td>
	</tr>
	<tr>
		<td>Queries the detail information of a cluster service (DescribeClusterServiceInfo)</td>
	</tr>
	<tr>
		<td>Queries a list of service events (DescribeServiceEvent)</td>
	</tr>
	<tr>
		<td>Queries the YAML file of a cluster service (DescribeClusterServiceText)</td>
	</tr>
	<tr>
		<td>Modifies a cluster service (ModifyClusterService)</td>
	</tr>
	<tr>
		<td>Modifies the description of a service (ModifyServiceDescription)</td>
	</tr>
	<tr>
		<td>Modifies the image of a cluster service (ModifyClusterServiceImage)</td>
	</tr>
	<tr>
		<td>Modifies the label of a service (ModifyServiceLabels)</td>
	</tr>
	<tr>
		<td>Cluster rollback service (RollBackClusterService)</td>
	</tr>
	<tr>
		<td>Redeploys a cluster service (RedeployClusterService)</td>
	</tr>
	<tr>
		<td>Pauses a cluster service (PauseClusterService)</td>
	</tr>
	<tr>
		<td>Resumes a cluster service (ResumeClusterService)</td>
	</tr>
	<tr>
		<td>Deletes a cluster service (DeleteClusterService)</td>
	</tr>
	<tr>
        <td rowspan=4  colspan=2>Service Instance</td>
        <td>Queries a list of service instances (DescribeServiceInstance)</td>
	</tr>
	<tr>
		<td>Modifies the number of service replicas (ModifyServiceReplicas)</td>
	</tr>
	<tr>
		<td>Queries service instance logs (DescribeInstanceLog)</td>
	</tr>
	<tr>
		<td>Deletes a service instance (DeleteInstances)</td>
	</tr>
	<tr>
        <td rowspan=3  colspan=2>Namespace</td>
        <td>Queries cluster namespaces (DescribeClusterNameSpaces)</td>
	</tr>
	<tr>
		<td>Creates a cluster namespace (CreateClusterNamespace)</td>
	</tr>
	<tr>
		<td>Deletes a cluster namespace (DeleteClusterNamespace)</td>
	</tr>
	<tr>
        <td rowspan=4  colspan=2>Ingress</td>
        <td>Creates an ingress (CreateIngress)</td>
	</tr>
	<tr>
		<td>Queries a list of ingresses (DescribeIngress)</td>
	</tr>
	<tr>
		<td>Modifies an ingress (MosifyIngress)</td>
	</tr>
	<tr>
		<td>Deletes an ingress (DeleteIngress)</td>
	</tr>
	<tr>
        <td rowspan=8  colspan=2>Log</td>
        <td>Enables logging (GetLogDaemonStatus)</td>
        <td rowspan=8>Deprecated</td>
	</tr>
	<tr>
		<td>Creates cluster log collection policies (CreateLogCollector)</td>
	</tr>
	<tr>
		<td>Lists log collection policies (ListLogCollector)</td>
	</tr>
	<tr>
		<td>Updates log collection policies (UpdateLogCollector)</td>
	</tr>
	<tr>
		<td>Gets log collector information (GetLogCollector)</td>
	</tr>
	<tr>
		<td>Gets the status of log collectors (GetLogDaemonStatus)</td>
	</tr>
	<tr>
		<td>Checks the names of log collectors (CheckIfLogCollectorName)</td>
	</tr>
	<tr>
		<td>Deletes log collection policies (DeleteLogCollector)</td>
	</tr>
	<tr>
        <td  colspan=2 >Monitor</td>
        <td>Gets container service monitor data (GetMonitorData)</td>
        <td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/248/11016">Container service - pod metrics monitoring (GetMonitorData)</a></li><li><a href="https://intl.cloud.tencent.com/document/product/248/11017">Container service - container metrics monitoring (GetMonitorData)</a></li><li><a href="https://intl.cloud.tencent.com/document/product/248/11018">Container service - service metrics monitoring (GetMonitorData)</a></li></ul></td>
	</tr>
    <tr>       
        <td rowspan=28 >Image Hub</td>
        <td rowspan=3>User and Password Management</td>
        <td>Registers a user (without specifying a namespace) (RegisterRepositoryAccountNew)</td>
        <td >Creates an individual user (CreateUserPersonal)</td>
    </tr>
    <tr>
        <td>Queries user quota (GetLimit)</td>
        <td >Queries individual user quota (DescribeUserQuotaPersonal)</td>
    </tr>
    <tr>
        <td>Modifies password (ChangePassword)</td>
        <td>Modifies individual user login password (ModifyUserPasswordPersonal)</td>
    </tr>
    <tr>
    	<td rowspan=4>Namespace</td>
        <td>Creates namespace (CreateCCRNamespace)</td>
        <td>Creates namespace (CreateNamespacePersonal)</td>
    </tr>
    <tr>
        <td>Queries namespace (GetNamespaceInfo)</td>
        <td>Queries namespace (DescribeNamespacePersonal)</td>
    </tr>
    <tr>
        <td>Queries the namespace existence (NamespaceIsExists)</td>
        <td>Queries the namespace existence (ValidateNamespaceExistPersonal)</td>
    </tr>
    <tr>
        <td>Deletes namespace (DeleteUserNamespace)</td>
        <td>Deletes namespace (DeleteNamespacePersonal)</td>
    </tr>
    <tr>
    	<td rowspan=9>Image Repository</td>
        <td>Creates image repository (CreateRepository)</td>
        <td>Creates image repository (CreateRepositoryPersonal)</td>
    </tr>
    <tr>
        <td>Queries image repository information (GetRepositoryInfo)</td>
        <td>Queries image repository (DescribeRepositoryPersonal)</td>
    </tr>
    <tr>
        <td>-</td>
        <td>Deletes image repository (DeleteRepositoryPersonal)</td>
    </tr>
    <tr>
        <td>Deletes repositories in batches (BatchDeleteRepository)</td>
        <td>Deletes repositories in batches (BatchDeleteRepositoryPersonal)</td>
    </tr>
    <tr>
        <td>Checks if the image repository exists (RepositoryisExists)</td>
        <td>Checks if the image repository exists (ValidateRepositoryExistPersonal)</td>
    </tr>
    <tr>
        <td>Gets a list of user repositories (GetUserRepositoryList)</td>
        <td>Queries a list of user-created repositories (DescribeRepositoryOwnerPersonal)</td>
    </tr>
    <tr>
        <td>Queries user repositories (SearchUserRepository)</td>
        <td>Queries user repositories that fits certain criteria (DescribeRepositoryFilterPersonal</td>
    </tr>
    <tr>
        <td>Updates image repository access attributes (UpdateRepositoryPublic)</td>
        <td>Modifies image repository public attributes (ModifyRepositoryAccessPersonal)</td>
    </tr>
    <tr>
        <td>Modifies image repository description (UpdateRepositoryDesc)</td>
        <td>Modifies image repository description (ModifyRepositoryInfoPersonal)</td>
    </tr>
    <tr>
    	<td rowspan=8>Image Repository</td>
        <td>Gets a list of tags (GetTagList)</td>
        <td>Queries image version (DescribeImagePersonal)</td>
    </tr>
    <tr>
        <td>-</td>
        <td >Queries image version using certain criteria (DescribeImageFilterPersonal)</td>
    </tr>
    <tr>
        <td>-</td>
        <td>Deletes image version (DeleteImagePersonal)</td>
    </tr>
    <tr>
        <td>Deletes tags in batches (BatchDeleteTag)</td>
        <td>Deletes image version in batches (BatchDeleteImagePersonal)</td>
    </tr>
    <tr>
        <td>Duplicates image version (DuplicateImage)</td>
        <td>Duplicates image version (DuplicateImagePersonal)</td>
    </tr>
    <tr>
        <td>Sets repository tag auto delete strategy (SetAutoDelStrategy)</td>
        <td>Creates image version lifecycle configuration (CreateImageLifecyclePersonal)</td>
    </tr>
    <tr>
        <td>Gets repository tag auto delete strategy (GetAutoDelStrategy)</td>
        <td>Queries image version lifecycle configuration (DescribeImageLifecyclePersonal)</td>
    </tr>
    <tr>
        <td>Disables repository tag auto delete strategy (CloseAutoDelStrategy)</td>
        <td>Deletes image version lifecycle configuration (DeleteImageLifecyclePersonal)</td>
    </tr>
    <tr>
    	<td rowspan=4>Trigger</td>
        <td>Adds a trigger (AddUpdateWorkloadTrigger)</td>
        <td>Creates an application update trigger (CreateApplicationTriggerPersonal)</td>
    </tr>
    <tr>
        <td>Modifies service update trigger (ModifyUpdateServiceTrigger)</td>
        <td>Modifies service update trigger (ModifyApplicationTriggerPersonal)</td>
    </tr>
    <tr>
        <td>Queries triggers (ListTrigger)</td>
        <td>Queries application triggers (DescribeApplicationTriggerPersonal)</td>
    </tr>
    <tr>
        <td>Queries trigger logs (ListTriggerLog)</td>
        <td>Queries application update trigger logs (DescribeApplicationTriggerLogPersonal)</td>
    </tr>
</table>


<style>
	.params{margin-bottom:0px !important;}
</style>






