
## Overview
TencentDB for MySQL allows you to create one or more read-only instances to form an RO group, which is suitable for read/write separation and one-source-multiple-replica application scenarios and capable of greatly enhancing the read load capacity of your database.

An RO group is a set of read-only instances sharing the same address. You can set their weights to balance the traffic load, set the policy of removing delayed read-only instances, and perform other configurations. You can deploy an RO group as needed and send the corresponding read requests to read-only instances according to certain rules. In addition, you can implement disaster recovery by configuring multiple read-only instances in the same RO group.

## Prerequisites
- A source instance must be created first before a read-only instance can be created. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/236/5160).
- Before use, a TencentDB for MySQL instance needs to be initialized. For more information, see [Initializing TencentDB for MySQL Instance](/doc/product/236/3128).

## Directions
### Creating RO group
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. Click **Add Read-Only Instance** in the **Instance Architecture Diagram** section on the **Instance Details** tab or click **Create** on the **Read-Only Instance** tab.
![](https://main.qcloudimg.com/raw/83e817ae1b9205d6cdf061684f7d3c12.png)
3. On the displayed purchase page, specify the following read-only instance configurations, confirm that everything is correct, and click **Buy Now**.
 - **Specify RO Group**: select **Create RO group**. If multiple instances are purchased at a time, all of them will be assigned to this new RO group, and their weights will be allocated by the system automatically by default.
 - **RO Group Name**: the RO group name doesn't need to be unique and can contain up to 60 letters, digits, hyphens, underscores, and dots.
 - **Remove Delayed RO Instances**: this option indicates whether to enable the removal policy. If a read-only instance is removed, its weight will be automatically set to 0.
 If a read-only instance is removed when its delay exceeds the threshold, it will become inactive, its weight will be automatically set to 0, and alarms will be sent (for more information on how to configure the read-only instance removal alarm and recipients, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)). The instance will be put back into the RO group when its delay falls below the threshold.
 No matter whether delayed read-only instance removal is enabled, a read-only instance that is removed due to instance failure will rejoin the RO group when it is repaired.
 - **Delay Threshold**: this sets a delay threshold for the read-only instance. When the threshold is exceeded, the instance will be removed from the RO group.
 - **Least RO Instances**: this is the minimum number of instances that should be retained in the RO group. When there are fewer instances in the RO group, even if an instance exceeds the delay threshold, it will not be removed.
 - **Assign Read Weight**: it is assigned by the system.
 - **Billing Mode**: read-only instances are pay-as-you-go.
![](https://main.qcloudimg.com/raw/a8f80ce3f01cbaa1847978bec455aa0d.png)
 - **Region**: it is the same as that of the source instance by default and cannot be changed currently.
 - **Database Version**: it is the same as that of the source instance by default.
 - **Architecture**: it is single-node. Although the single-node architecture is cost-effective, there are risks of single points of failures. We recommend you purchase at least two read-only instances in the RO group of your business that requires high availability.
 - **Data Replication Mode**: it is the same as that of the source instance by default.
 - **AZ**: if there are multiple AZs in the current region, you can select one as needed.
>?The network delay across AZs in the same region, in different regions, and in regions outside the Chinese mainland is around a few milliseconds, tens of milliseconds, and over 100 milliseconds respectively, so you should select an AZ carefully.
5. Return to the instance list. The status of the created instance is **Delivering**. If the status changes to **Running**, the read-only instance has been successfully created.

### Configuring RO group
On the RO group configuration page, you can configure the basic information of the group such as ID, name, delayed replication, replication delay, removal policy, delay threshold, least read-only instances, and read weight.
>?
>- Read-Only instances in an RO group can use different specifications, and their read traffic weights can be set.
>- Read-Only instances in the same RO group can have different expiration dates and billing modes.
>- Once enabled, delayed replication will take effect for all read-only instances in this RO group, but won't change their replication statuses.
>- The replication delay option will appear only after delayed replication is enabled.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click a source instance ID to enter the instance management page.
2. On the instance management page, click the **Read-Only Instance** tab and click **Configure** in the **RO Group** column to enter the RO group configuration page.
![](https://main.qcloudimg.com/raw/f03a6fc7e5460181e1e933157b4922cb.png)
3. On the RO group configuration page, configure the RO group information and click **OK**.
   You can set delayed replication and select to replay by flashbacked position or global transaction identifier (GTID) during the delay to efficiently roll back data and fix failures.
   - **Replication Delay**: you can configure the time of delayed replication between a read-only instance and its source instance. The value range is 1–259200 seconds.
   - **Remove Delayed RO Instances**: this option indicates whether to enable the removal policy. If a read-only instance is removed when its delay exceeds the threshold, its weight will be set to 0 automatically, and alarms will be sent (for more information on how to configure the read-only instance removal alarm and recipients, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)).
   - **Delay Threshold**: this sets a delay threshold for the read-only instance. When the threshold is exceeded, the instance will be removed from the RO group.
   - **Least RO Instances**: this is the minimum number of instances that should be retained in the RO group. When there are fewer instances in the RO group, even if an instance exceeds the delay threshold, it will not be removed.
   - **Assign Read Weight**: the RO group supports two weight assignment methods: automatic assignment by the system and custom assignment. The weight value must be an integer between 0 and 100. Below is the list of read weights automatically set for two-node and three-node MySQL instances by the system:
<table>
<thead><tr>
<th>Memory Specification (MB)</th>
<th>1000</th><th>2000</th><th>4000</th><th>8000</th><th>12000</th><th>16000</th><th>24000</th><th>32000</th><th>48000</th><th>64000</th><th>96000</th><th>128000</th><th>244000</th><th>488000</th>
</tr></thead>
<tbody><tr>
<td>Weight</td>
<td>1</td><td>1</td><td>2</td><td>2</td><td>4</td><td>4</td><td>8</td><td>8</td><td>10</td><td>12</td><td>14</td><td>16</td><td>26</td><td>50</td></tr>
</tbody></table>
 - **Rebalance**:
    - Modifying weight will only affect new loads if rebalancing is disabled. The operation has no impact on read-only instances accessed by existing persistent connections and does not cause momentary database disconnection.
    - If rebalancing is enabled, all connections to the database will be temporarily disconnected, and the loads of newly added connections will be balanced according to the set weights.
<img src="https://main.qcloudimg.com/raw/94a42aa7ed813d8ba68560c40749998f.png"  style="zoom:55%;">


### Terminating and deleting RO group
>?
>
>- RO groups cannot be deleted manually.
- An RO group will be automatically deleted when the last read-only instance in it is eliminated.
- Empty RO groups cannot be retained.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click a source instance ID to enter the instance management page.
2. On the instance management page, click the **Read-Only Instance** tab and click **Terminate/Return** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/ef06e1a956370519e0c0b652b8a07c72.png)
3. In the pop-up window, read and agree to the **Termination Rules** and click **Terminate Now**.

