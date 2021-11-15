## Operation Scenarios
TencentDB for MySQL allows you to create one or more read-only instances to form an RO group, which is suitable for read/write separation and one-master-multiple-slave application scenarios and capable of greatly enhancing the read load capacity of your database.

## Prerequisites
- A master instance should be created before a read-only instance can be created. For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/236/5160).
- Before use, a TencentDB for MySQL instance needs to be initialized. For more information, please see [Initializing TencentDB for MySQL Instance](https://intl.cloud.tencent.com/document/product/236/3128).

## Directions

### Creating RO group
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the details page.
2. On the instance details page, click **Add Read-only Instance** in the **Instance Architecture Diagram** to enter the read-only instance management page.
![](https://main.qcloudimg.com/raw/83e817ae1b9205d6cdf061684f7d3c12.png)
3. On the read-only instance page, click **Create** to create a read-only instance.
4. Select the desired configuration of the instance on the purchase page. After confirming that everything is correct, click **Buy Now**.
>If the "Specify RO Group" option is configured as **Create RO group**, the following basic information of the new RO group should be entered on the purchase page.
>- Group Name: the RO group name doesn't have to be unique and can contain up to 60 letters, digits, `-`, `_`, and `.`.
>- Eliminate Instances with Out-of-limit Delay: this option indicates whether to enable the removal policy. If a read-only instance is removed when its delay exceeds the threshold, it will become inactive, its weight will be set to 0 automatically, and warning notifications will be sent out (for more information on how to configure the RO instance elimination alarm and recipients, please see [Alarming Feature](https://intl.cloud.tencent.com/document/product/236/8457)). The instance will be put back into the RO group when its delay falls below the threshold. No matter whether this option is enabled, a read-only instance that is removed due to instance failure will rejoin the RO group when it is repaired.
>- Delay Threshold: set a delay threshold for a read-only instance. When the threshold is exceeded, the instance will be removed from the RO group.
>- Min Retained Instances: this is the minimum number of instances that have to be retained in the RO group. When there are fewer instances in the RO group, even if an instance exceeds the delay threshold, it will not be removed.

>
 - Specify an RO group.
 <table>
  <tr>
    <th width="25%">Specify RO Group</th>
    <th width="75%">Description</th>
  </tr>
  <tr>
    <td>Automatically assigned by the system (not specified)</td>
    <td>If multiple instances are purchased at a time, each instance will be distributed to an independent RO group, and their weights will be allocated by the system automatically by default.</td>
  </tr>
  <tr>
    <td>Create an RO group</td>
    <td>Create an RO group. If multiple instances are purchased at a time, all of them will be assigned to this new RO group, and their weights will be allocated by the system automatically by default.</td>
  </tr>
  <tr>
    <td>Existing RO group</td>
    <td>Specify an existing RO group. If multiple instances are purchased at a time, all of them will be assigned to this RO group. Their weights will be allocated as configured in the RO group. If automatic allocation by the system is set for the RO group, the instances will be added to the group automatically according to the purchased specifications. If custom allocation is set, their weight will be zero by default. <b>As the same private ID is shared within an RO group, if a VPC is used, the same security group settings will be shared. If an RO group is specified, it is not possible to customize any security group when purchasing instances.</b></td>
  </tr>
</table>
 - Billing mode: read-only instances are pay-as-you-go.
 - Select an instance specification and required disk capacity.
5. Return to the instance list. The status of the created instance is "Delivering". If the status changes to "Running", the read-only instance has been successfully created.


### Configuring RO group
On the RO group configuration page, you can configure the basic information of the group such as name, removal policy, delay threshold, minimum number of retained instances, and read weight.
>
>- Read-only instances in an RO group can use different specifications and their read traffic weights can be set.
>- Read-only instances in the same RO group can have different expiration dates and billing methods.
>
1. On the instance list page, select the master instance for which to set an RO group and click **Manage** in the **Action** column.
2. On the RO group management tab on the **Read-only Instance** page, click **Configure** to enter the read-only instance RO group configuration page.
![](https://main.qcloudimg.com/raw/f03a6fc7e5460181e1e933157b4922cb.png)
3. Configure the RO group options.
![](https://main.qcloudimg.com/raw/94a42aa7ed813d8ba68560c40749998f.png)
   - RO Group Name: the group name doesn't have to be unique and can contain up to 60 letters, digits, `-`, `_`, and `.`.
   - Eliminate Instances with Out-of-limit Delay: this option indicates whether to enable the removal policy. If a read-only instance is removed when its delay exceeds the threshold, it will become inactive, its weight will be set to 0 automatically, and warning notifications will be sent out (for more information on how to configure the RO instance elimination alarm and recipients, please see [Alarming Feature](https://intl.cloud.tencent.com/document/product/236/8457)).
   - Delay Threshold: set a delay threshold for a read-only instance. When the threshold is exceeded, the instance will be removed from the RO group.
   - Min Retained Instances: this is the minimum number of instances that have to be retained in the RO group. When there are fewer instances in the RO group, even if an instance exceeds the delay threshold, it will not be removed.
   - Assign Read Weight: the RO group supports two weight allocation methods: automatic allocation by the system and custom allocation. The weight value must be an integer between 0 and 100. Below is the list of read weights automatically set for High IO TencentDB for MySQL instances by the system:
<table>
  <tr>
    <th>Instance Specification</th>
    <th>Weight</th>
  </tr>
  <tr>
		<td>1,000 MB memory</td>
		<td>1</td>
  </tr>
  <tr>
		<td>2,000 MB memory</td>
		<td>1</td>
  </tr>
  <tr>
		<td>4,000 MB memory</td>
		<td>2</td>
  </tr>
	  <tr>
		<td>8,000 MB memory</td>
		<td>2</td>
  </tr>
	  <tr>
		<td>12,000 MB memory</td>
		<td>4</td>
  </tr>
	  <tr>
		<td>16,000 MB memory</td>
		<td>4</td>
  </tr>
	  <tr>
		<td>24,000 MB memory</td>
		<td>8</td>
  </tr>
	  <tr>
		<td>32,000 MB memory</td>
		<td>8</td>
  </tr>
	  <tr>
		<td>48,000 MB memory</td>
		<td>10</td>
  </tr>
	  <tr>
		<td>64,000 MB memory</td>
		<td>12</td>
  </tr>
	  <tr>
		<td>96,000 MB memory</td>
		<td>14</td>
  </tr>
	  <tr>
		<td>128,000 MB memory</td>
		<td>16</td>
  </tr>
	  <tr>
		<td>244,000 MB memory</td>
		<td>26</td>
  </tr>  <tr>
		<td>488,000 MB memory</td>
		<td>50</td>
  </tr>
</table> 
 - Load Rebalancing:
 If load rebalancing is disabled, modifying weight will take effect only for new loads but not affect the read-only instances accessed by existing persistent connections or cause short disconnection from the database.
  If load rebalancing is enabled, a short disconnection lasting for just seconds will occur to disconnect all connections from the database, and the loads of newly added connections will be balanced according to the set weights.

### Terminating and deleting RO group
- RO groups cannot be deleted manually.
- An RO group will be automatically deleted when the last read-only instance in it is terminated completely.
- Empty RO groups cannot be retained.
