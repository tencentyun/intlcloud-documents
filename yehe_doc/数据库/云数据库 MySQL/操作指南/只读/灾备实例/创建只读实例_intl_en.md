## Overview
TencentDB for MySQL allows you to create one or more read-only instances, which are suitable for read/write separation and one-source-multiple-replica application scenarios and capable of greatly enhancing the read load capacity of your database.

Database proxy is supported. After creating a read-only instance, you can purchase the database proxy service to enable the read/write separation feature. Then, you can configure the database proxy address in your application so as to automatically forward write requests to the source instance and read requests to the read-only instance.

>?
>- For read-only instance pricing, see [Product Pricing](https://buy.cloud.tencent.com/price/cdb).
>- You can now configure a custom and exclusive private network address (IP and port) for a read-only instance on the instance details page.
>![](https://qcloudimg.tencent-cloud.cn/raw/667761ccccc029b2723eea47c2034186.png)

#### Concepts
- Read-only group: It consists of one or more load balancing-enabled read-only instances. If there are multiple read-only instances in one read-only group, read request volume can be evenly distributed among the instances. Read-only groups provide IPs and ports for access to databases.
- Read-only instance: A single-node (with no replica) instance that supports read requests. It cannot exist independently; instead, it must be in a read-only group.

#### Architecture
The MySQL source-replica binlog sync feature is adopted for read-only instances, which can sync the changes in the source instance (source database) to all read-only instances. Given the single-node architecture (without a replica) of read-only instances, repeated attempts to restore a failing read-only instance will be made. Therefore, we recommend that you choose an RO group over a read-only instance for higher availability.
>!If there is only one read-only instance in the read-only group, there will be risks with single points of failure, and this group will not be included in the overall availability calculation of the TencentDB for MySQL service. A single read-only instance does not provide SLA guarantee. We recommend you purchase at least two read-only instances to ensure the availability of the read-only group.
>
![](https://qcloudimg.tencent-cloud.cn/raw/d6259ca885bb51740f68934481ff28d4.png)

## Feature Limits
- Read-only instances cannot be created for single-node instances of the cloud disk edition.
- Read-only instances can be purchased only for **two-node or three-node source instances on MySQL 5.6 or later with the InnoDB engine at a specification of 1 GB memory and 50 GB disk capacity or above**. If your source instance is below this specification, upgrade it first.
- The minimum specification of a read-only instance is 1 GB memory and 50 GB disk capacity, which must be equal to or greater than the storage capacity purchased for the source instance.
- A source instance can create up to 5 read-only instances.
- Backup and rollback features are not supported.
- Data cannot be migrated to read-only instances.
- Database creation/deletion is not supported and neither is phpMyAdmin (PMA).
- Operations including account creation/deletion/authorization and account name/password modification are not supported.

## Note
- There is no need to maintain accounts or databases for read-only instances, which are synchronized with those of the primary instance.
- If the MySQL version is 5.6 but GTID is not enabled, you need to enable GTID in the console first before creating a read-only instance.
The operation takes a long time, and the instance will be disconnected for several seconds. You are recommended to do so during off-peak hours and add a reconnection mechanism in the programs that access the database.
- Read-only instances only support the InnoDB engine.
- Data inconsistency between multiple read-only instances may occur due to the delay in data sync between the read-only instances and the source instance. You can check the delay in the console.
- The specification of a read-only instance can be different from that of the source instance, which makes it easier for you to upgrade the read-only instance based on the load. We recommend that you keep the same specifications of read-only instances in one RO group.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance details page.
2. Click **Add Read-Only Instance** in the **Instance Architecture Diagram** section on the **Instance Details** tab or click **Create** on the **Read-Only Instance** tab.
3. On the displayed purchase page, specify the following read-only instance configurations, confirm that everything is correct, and click **Buy Now**.
>?If you need to unify the expiration time of the source and read-only instances, you can set the collective expiration date in the [renewal management console](https://console.cloud.tencent.com/account/renewal) as instructed in [Renewal Management](https://intl.cloud.tencent.com/document/product/555/7454).
>
![](https://main.qcloudimg.com/raw/5c002d37fdeb72a5396a394133672338.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Specify RO Group</td><td>You can use the RO group automatically assigned by the system, create one, or select an existing one. <ul><li>Assigned by system: If multiple instances are purchased at a time, each of them will be assigned to an independent RO group, and their weights will be automatically assigned by the system by default. </li><li>Create RO group: Create an RO group. If multiple instances are purchased at a time, all of them will be assigned to this new RO group, and their weights will be allocated by the system automatically by default. </li><li>Existing RO group: Specify an existing RO group. If multiple read-only instances are purchased at a time, all of them will be assigned to the RO group. <br>Their weights will be allocated as configured in the RO group. If assignment by the system is set for the RO group, the instances will be added to the group automatically according to the purchased specifications. If custom allocation is set, their weights will be zero by default. <br>As the same private IP is shared within an RO group, if a VPC is used, the same security group settings will be shared. If an RO group is specified, it is not possible to customize any security group when instances are purchased. </li></ul></td></tr>
<tr>
<td>RO Group Name</td><td>Y can set the name of the new RO group when creating it. The name can contain up to 60 letters, digits, hyphens, underscores, and dots.</td></tr>
<tr>
<td>Remove Delayed RO Instances</td><td>Select whether to enable the removal policy. If this option is enabled, you need to set **Delay Threshold** and **Least RO Instances**, and the weight of the removed instances is automatically set to 0. <dx-alert infotype="explain" title="">
If a read-only instance is removed when its delay exceeds the threshold, it will become inactive, its weight will be automatically set to 0, and alarms will be sent to corresponding recipients. The instance will be put back into the RO group when its delay falls below the threshold. For more information on how to configure the read-only instance removal alarm and recipients, see <a href="https://intl.cloud.tencent.com/document/product/236/8457" target="_blank">Alarm Policies (TCOP)</a>. No matter whether delayed read-only instance removal is enabled, a read-only instance that is removed due to instance failure will rejoin the RO group when it is repaired.
</dx-alert></td></tr>
<tr>
<td>Billing Mode</td><td>Monthly subscription and pay-as-you-go billing are supported. </td></tr>
<tr>
<td>AZ</td><td>When creating a new RO group, you can select the same AZ as the source instance or a different AZ. There are no substantial differences between different AZs. If you choose a different AZ, the RO group will reside across AZs and can improve data disaster recovery, but there will be a few milliseconds of network latency. </td></tr>
</tbody></table>
4. After the purchase is completed, you will be redirected to the instance list. When the status of the instance changes to **Running**, it can be used normally.

## FAQs
#### What are the rules for removing read-only instances?
After **Remove Delayed RO Instances** is enabled, the RO group will determine the removal rule based on the delay threshold and "Least RO Instances" value. If the delay of a read-only instance reaches the threshold, it will be removed and made inactive, with its weight set to 0 and an alarm sent to corresponding recipients. When its delay falls below the threshold, it will be returned to the RO group.
- Delay Threshold: Set a delay threshold for a read-only instance. When the threshold is exceeded, the instance will be removed from the RO group.
- Least RO Instances: This is the minimum number of instances that should be retained in the read-only group. When there are fewer instances in the read-only group, even if an instance exceeds the delay threshold, it will not be removed.

#### If read-only instances are terminated or returned, how will the source instance be affected?
The termination and return of read-only instances has no impact on the source instance.

#### Why can't I select a specific AZ when creating a read-only instance?
If you can't select an AZ, it means that there are no resources in this AZ. You can choose another AZ as displayed on the actual purchase page, which will not affect your use of the read-only instance.

#### Can I select an AZ different from that of the source instance when creating a read-only instance?
Yes. When creating a read-only instance, you can choose to create a new RO group for it and select an AZ different from that of the source instance. However, if you select an existing RO group, the AZ of the new read-only instance can only be the same as that of the selected existing RO group, which may not necessarily be the same as that of the source instance.
