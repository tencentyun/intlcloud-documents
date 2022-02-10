## Overview
TencentDB for MySQL allows you to create one or more read-only instances to form an RO group, which is suitable for read/write separation and one-source-multiple-replica application scenarios and capable of greatly enhancing the read load capacity of your database.

An RO group is a set of read-only instances sharing the same private network address. You can set their weights to balance the traffic load, set the policy of removing delayed read-only instances, and perform other configurations. You can deploy an RO group as needed and send the corresponding read requests to read-only instances according to certain rules. In addition, you can implement disaster recovery by configuring multiple read-only instances in the same RO group.

## Prerequisites
- A source instance must be created first before a read-only instance can be created. For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/236/5160).
- Before use, a TencentDB for MySQL instance needs to be initialized. For more information, please see [Initializing TencentDB for MySQL Instance](/doc/product/236/3128).

## Directions
### Creating RO group
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance details page, click **Add Read-Only Instance** in **Instance Architecture Diagram** or click **Create** on the read-only instance page to enter the purchase page.
![](https://main.qcloudimg.com/raw/83e817ae1b9205d6cdf061684f7d3c12.png)
3. Select the desired read-only instance configuration on the purchase page. After confirming that everything is correct, click **Buy Now**.
 - **Specify RO Group**: select **Create RO group**. If multiple instances are purchased at a time, all of them will be assigned to this new RO group, and their weights will be automatically assigned by the system by default.
 - **RO Group Name**: the RO group name doesn't need to be unique and can contain up to 60 letters, digits, hyphens, underscores, and dots.
 - **Remove Delayed RO Instances**: this option indicates whether to enable the removal policy. If a read-only instance is removed, its weight will be automatically set to 0.
 If a read-only instance is removed when its delay exceeds the threshold, it will become inactive, its weight will be automatically set to 0, and alarms will be sent (for more information on how to configure the read-only instance removal alarm and recipients, please see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)). The instance will be put back into the RO group when its delay falls below the threshold.
 No matter whether delayed read-only instance removal is enabled, a read-only instance that is removed due to instance failure will rejoin the RO group when it is repaired.
 - **Delay Threshold**: set a delay threshold for the read-only instance. When the threshold is exceeded, the instance will be removed from the RO group.
 - **Least RO Instances**: this is the minimum number of instances that should be retained in the RO group. When there are fewer instances in the RO group, even if an instance exceeds the delay threshold, it will not be removed.
 - **Assign Read Weight**: it is assigned by the system.
 - **Billing Mode**: read-only instances are pay-as-you-go.
![](https://main.qcloudimg.com/raw/a8f80ce3f01cbaa1847978bec455aa0d.png)
5. Return to the instance list. The status of the created instance is **Delivering**. If the status changes to **Running**, the read-only instance has been successfully created.

### Configuring RO group
On the RO group configuration page, you can configure the basic information of the group such as name, removal policy, delay threshold, least RO instances, and read weight.
>?
>- Read-Only instances in an RO group can use different specifications, and their read traffic weights can be set.
>- Read-Only instances in the same RO group can have different expiration dates and billing modes.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click a source instance name to enter the instance management page.
2. On the instance management page, click the **Read-Only Instance** tab and click **Configure** in the RO group column to enter the RO group configuration page.
![](https://main.qcloudimg.com/raw/f03a6fc7e5460181e1e933157b4922cb.png)
3. On the RO group configuration page, configure the RO group information and click **OK**.
   - **Remove Delayed RO Instances**: this option indicates whether to enable the removal policy. If a read-only instance is removed, its weight will be automatically set to 0. If a read-only instance is removed when its delay exceeds the threshold, it will become inactive, alarms will be sent (for more information on how to configure the read-only instance removal alarm and recipients, please see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)).
   - **Delay Threshold**: set a delay threshold for the read-only instance. When the threshold is exceeded, the instance will be removed from the RO group.
   - **Least RO Instances**: this is the minimum number of instances that should be retained in the RO group. When there are fewer instances in the RO group, even if an instance exceeds the delay threshold, it will not be removed.
   - **Assign Read Weight**: the RO group supports two weight assignment methods: automatic assignment by the system and custom assignment. The weight value must be an integer between 0 and 100. Below is the list of read weights automatically set for two-node and three-node TencentDB for MySQL instances by the system:
<table>
<tr><th>Instance Specification</th><th>Weight</th></tr>
<tr><td>1,000 MB memory</td><td>1</td></tr>
<tr><td>2,000 MB memory</td><td>1</td></tr>
<tr><td>4,000 MB memory</td><td>2</td></tr>
<tr><td>8,000 MB memory</td><td>2</td></tr>
<tr><td>12,000 MB memory</td><td>4</td></tr>
<tr><td>16,000 MB memory</td><td>4</td></tr>
<tr><td>24,000 MB memory</td><td>8</td></tr>
<tr><td>32,000 MB memory</td><td>8</td></tr>
<tr><td>48,000 MB memory</td><td>10</td></tr>
<tr><td>64,000 MB memory</td><td>12</td></tr>
<tr><td>96,000 MB memory</td><td>14</td></tr>
<tr><td>128,000 MB memory</td><td>16</td></tr>
<tr><td>244,000 MB memory</td><td>26</td></tr>
<tr><td>488,000 MB memory</td><td>50</td></tr>
</table> 
 - **Rebalance**:
    - If rebalance is disabled, modifying weight will take effect only for new loads but will not affect the read-only instances accessed by existing persistent connections or cause a momentary disconnection from the database.
    - If rebalance is enabled, a momentary disconnection will occur to disconnect all connections from the database, and the loads of newly added connections will be balanced according to the set weights.
![](https://main.qcloudimg.com/raw/94a42aa7ed813d8ba68560c40749998f.png)

### Terminating and deleting RO group
- RO groups cannot be deleted manually.
- An RO group will be automatically deleted when the last read-only instance in it is eliminated.
- Empty RO groups cannot be retained.
