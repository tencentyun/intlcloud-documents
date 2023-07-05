This document describes how to deploy super nodes in a cluster in the TKE console. 

## Prerequisites

- You have [created a cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- Kubernetes is on v1.16 or later.

## Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** on the left sidebar.
2. On the cluster list page, click the target cluster ID to enter the cluster details page.
3. Select **Node Management** > **Super Node** on the left sidebar.
![](https://qcloudimg.tencent-cloud.cn/raw/b40c5cdbadd2a98355958bfd0c3bacef.png)
4. Click **Create** and specify the parameters as prompted.
	![](https://qcloudimg.tencent-cloud.cn/raw/f276821238f853a4e5b011011a14175e.png)
	- **Node Pool**: **Auto-create a node pool** and **Add to an existing node pool** are available. For the former, a super node pool will be created when a super node is created; for the latter, a new super node can be added to an existing node pool for unified management. Super nodes in different billing modes and AZs and with different specifications can be added to a node pool.
	- **Node Pool Name**: If a node pool is automatically created, its name can be managed.
	- **Super node configuration**:
	  - **Availability zone**: Select the availability zone where the super node is located.
	  - **Billing mode**: The pay-as-you-go billing mode is supported in all regions.
	  - **Container network**: Assign IPs within the container IP range to containers in the cluster. Pods on super nodes will occupy VPC subnet IPs. The number of Pods that can be scheduled to super nodes is limited by the number of remaining IPs. Select subnets with sufficient available IPs and not in conflict with those of other services. Pods on super nodes will run in the specified VPC. Each Pod is bound to an ENI in the specified VPC. You can check the ENI associated with the Pod in the [ENI list](https://console.cloud.tencent.com/vpc/eni).
	  Multiple subnets can be selected in the pay-as-you-go billing mode, and a pay-as-you-go super node is created for a subnet. The super nodes are billed based on the Pod specifications and running duration after the workloads are created and the Pods are scheduled to the super nodes.
	  <dx-alert infotype="notice" title="">
	- We recommend that you configure multiple availability zones for the container network so that your workloads can be automatically distributed to multiple availability zones, which improves usability.
	- Ensure that the subnet assigned to the container network has sufficient available IPs, so as to prevent pod creation failure caused by insufficient IPs when creating a large-scale workload.
	</dx-alert>
    - **Security group configuration**: For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
	<dx-alert infotype="notice" title="">
- The security group configured for a super node is directly associated with its Pods. Configure the network rules as required by the Pods. For example, you need to open port 80 if the Pods provide services via port 80.
- The security group is the default group to which Pods scheduled to the super node are bound. You can specify another security group to overwrite the default one during scheduling.
</dx-alert>
5. (Optional) Click **More Settings** to view or configure more information.
![](https://qcloudimg.tencent-cloud.cn/raw/b0de2c18ae445dcae739038b3c4be537.png)
	- **Cordon initial nodes**: If **Cordon this node** is selected, new Pods cannot be scheduled to this node. You can uncordon the node manually, or execute the [uncordon command](https://intl.cloud.tencent.com/document/product/457/30654) in custom data as needed.
	- **Labels**: Click **New Label** and customize the label settings. The specified label here will be automatically added to super nodes created in the node pool to help filter and manage super nodes by label.
	- **Taints**: It is a node attribute usually used with tolerations. You can specify this parameter for all the super nodes in the node pool, so as to prevent Pods that don't meet the requirements from being scheduled to these nodes and drain such Pods from the nodes.
<dx-alert infotype="explain" title="">
The value of **Taints** usually consists of `key`, `value`, and `effect`. Valid values of `effect`:
- **PreferNoSchedule**: Optional. Try not to schedule a Pod to a node with a taint that cannot be tolerated by the Pod.
- **NoSchedule**: When a node contains a taint, a Pod without the corresponding toleration must not be scheduled.
- **NoExecute**: When a node contains a taint, a Pod without the corresponding toleration won't be scheduled to the node and any such Pods on the node will be drained.<br>

Assume that Taints is set to `key1=value1:PreferNoSchedule`. The following figure shows the configurations in the TKE console:
![](https://qcloudimg.tencent-cloud.cn/raw/b8a9b16cc95bd506f275e14b3957263b.png)
</dx-alert>

6. Click **Create Super Node**. If you select **Auto-create a node pool**, the super node pool of the super node will be created synchronously.

