## Overview
TencentDB for SQL Server allows you to create one or more read-only instances to form a read-only group, which is suitable for read/write separation and one-primary-multiple-replica application scenarios and capable of greatly enhancing the read load capacity of your database.

## Prerequisites
A primary instance must be created first before a read-only instance can be created. For more information, please see [Creating TencentDB for SQL Server Instance](https://intl.cloud.tencent.com/document/product/238/31571).

## Directions
### Creating Read-Only group
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the details page.
2. Click **Add Read-Only Instance** in the **Instance Architecture Diagram** on the instance details page to enter the purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/6acf3d61af70824bae20cbc668e96463.png)
3. On the purchase page, select the desired read-only instance configuration, confirm that everything is correct, and click **Buy Now**.
>?If the **Specify RO Group** option is configured as **Create RO group**, the following basic information of the new read-only group should be entered on the purchase page.
>- RO Group Name: the group name doesn't have to be unique and can contain up to 60 letters, digits, hyphens, underscores, and dots.
>- Remove Delayed RO Instances: this option indicates whether to enable the removal policy. If a read-only instance's delay exceeds the threshold, it will be removed and become inactive, and its weight will be set to 0. It will be put back into the read-only group when its delay falls below the threshold. No matter whether delayed read-only instance removal is enabled, a read-only instance that is removed due to instance failure will rejoin the read-only group when it is repaired.
>- Delay Threshold: this sets a delay threshold for the read-only instance. When the threshold is exceeded, the instance will be removed from the read-only group.
>- Least RO Instances: this is the minimum number of instances that should be retained in the read-only group. When there are fewer instances in the read-only group, even if an instance exceeds the delay threshold, it will not be removed.
>![](https://qcloudimg.tencent-cloud.cn/raw/c95128691098cb6eec01c4d55ac2eae7.png)
>
<table><tr><th width="25%">Specify Read-Only Group</th><th width="75%">Description</th></tr>
<tr>
<td>Assigned by system (not specified)</td>
<td>If multiple instances are purchased at a time, each of them will be assigned to an independent read-only group, and their weights will be automatically assigned by the system by default.</td></tr>
<tr>
<td>Create read-only group</td>
<td>Create a read-only group. If multiple instances are purchased at a time, all of them will be assigned to this new read-only group, and their weights will be allocated by the system automatically by default.</td></tr>
<tr>
<td>Existing read-only group</td>
<td>Specify an existing read-only group. If multiple instances are purchased at a time, all of them will be assigned to this read-only group. Their weights will be allocated as configured in the read-only group. If assignment by the system is set for the read-only group, the instances will be added to the group automatically according to the purchased specifications. If custom allocation is set, their weights will be zero by default. <b>As the same private IP is shared within a read-only group, if a VPC is used, the same security group settings will be shared. If a read-only group is specified, it is not possible to customize any security group when instances are purchased.</b></td></tr>
</table>
4. Return to the instance list. The status of the created read-only instance is **Delivering**. If the status changes to **Running**, the instance has been successfully created.

### Configuring read-only group
On the read-only group configuration page, you can configure the basic information of the group such as name, removal policy, delay threshold, least read-only instances, and read weight.
>?
>- Read-Only instances in a read-only group can use different specifications, and their read traffic weights can be set.
>- Read-Only instances in the same read-only group can have different expiration dates and billing modes.
>
1. In the [instance list](https://console.cloud.tencent.com/sqlserver), select a primary instance for which to set a read-only group, and click the **instance ID** or **Manage** in the **Operation** column on the right to enter the instance management page.
2. On the instance management page, click the **Read-Only Instance** tab and click **Configure** to enter the read-only group configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/2e8489adca2b2bdb29ed9cf7e0b13882.png)
3. In the pop-up window, configure the read-only group options.
![](https://qcloudimg.tencent-cloud.cn/raw/5b08812f65c695e216c01a9f8dce9647.png)
   - RO Group Name: the group name doesn't have to be unique and can contain up to 60 letters, digits, hyphens, underscores, and dots.
   - Remove Delayed RO Instances: this option indicates whether to enable the removal policy. If a read-only instance is removed, its weight will be automatically set to 0.
   - Delay Threshold: this sets a delay threshold for the read-only instance. When the threshold is exceeded, the instance will be removed from the read-only group.
   - Least RO Instances: this is the minimum number of instances that should be retained in the read-only group. When there are fewer instances in the read-only group, even if an instance exceeds the delay threshold, it will not be removed.
   - Assign Read Weight: the read-only group allows for two types of weight assignment: system-assigned weights and custom weights. A number between 0 and 100 must be used as the weight value. The system automatically sets read weights for a SQL Server instance, as seen below.
<table>
<tr><th>Instance Specification</th><th>Weight</th></tr>
<tr>
<td>2,000 MB memory</td><td>1</td></tr>
<tr>
<td>4,000 MB memory</td><td>2</td></tr>
<tr>
<td>8,000 MB memory</td><td>2</td></tr>
<tr>
<td>12,000 MB memory</td><td>4</td></tr>
<tr>
<td>16,000 MB memory</td><td>4</td></tr>
<tr>
<td>24,000 MB memory</td><td>8</td></tr>
<tr>
<td>32,000 MB memory</td><td>8</td></tr>
<tr>
<td>48,000 MB memory</td><td>10</td></tr>
<tr>
<td>64,000 MB memory</td><td>12</td></tr>
<tr>
<td>96,000 MB memory</td><td>14</td></tr>
<tr>
<td>128,000 MB memory</td><td>16</td></tr>
<tr>
<td>244,000 MB memory</td><td>26</td></tr>
<tr>
<td>488,000 MB memory</td><td>50</td></tr>
</table> 
 - Rebalance:
 Modifying weight will only affect new loads if rebalancing is disabled. The operation has no impact on read-only instances accessed by existing persistent connections and does not cause momentary database disconnection.
    If rebalancing is enabled, all connections to the database will be temporarily disconnected, and the loads of newly added connections will be balanced according to the set weights.

### Terminating and deleting read-only group
- Read-Only groups cannot be deleted manually.
- A read-only group will be automatically deleted when the last read-only instance in it is eliminated.
- Empty read-only groups cannot be retained.
