## Overview
TencentDB for MySQL allows you to create one or more read-only instances, which are suitable for read/write separation and one-source-multiple-replica application scenarios and capable of greatly enhancing the read load capacity of your database.

Database proxy is supported. After creating a read-only instance, you can purchase the database proxy service to enable the read/write separation feature. Then, you can configure the database proxy address in your application so as to automatically forward write requests to the source instance and read requests to the read-only instance.

>?
>- For read-only instance pricing, see [Pricing | TencentDB for MySQL](https://buy.intl.cloud.tencent.com/price/cdb).
>- You can enable an independent private network address and customize the private IP and port for a read-only instance on the **Instance Details** page.
>![](https://qcloudimg.tencent-cloud.cn/raw/667761ccccc029b2723eea47c2034186.png)

#### Concepts
- Read-only group: It consists of one or more load balancing-enabled read-only instances. If there are multiple read-only instances in one read-only group, read request volume can be evenly distributed among the instances. read-only groups provide IPs and ports for access to databases.
- Read-only instance: A single-node (with no replica) instance that supports read requests. It cannot exist independently; it must be in a read-only group.

#### Architecture
The MySQL source-replica binlog sync feature is adopted for read-only instances, which can sync the changes in the source instance (source database) to all read-only instances. Given the single-node architecture (without a replica) of read-only instances, repeated attempts to restore a failing read-only instance will be made. Therefore, we recommend you choose a read-only group over a read-only instance for higher availability.
>!If there is only one read-only instance in the read-only group, there will be risks with single points of failure, and this group will not be included in the overall availability calculation of the TencentDB for MySQL service. A single read-only instance does not provide SLA guarantee. We recommend you purchase at least two read-only instances to ensure the availability of the read-only group.
>
![](https://qcloudimg.tencent-cloud.cn/raw/e8000e0fae60f2f8ff884bf47d6babb0.png)

## Feature Limits
- Read-only instances cannot be created for single-node instances of the cloud disk edition.
- Read-only instances can be purchased only for **two-node or three-node source instances on MySQL 5.6 or later with the InnoDB engine at a specification of 1 GB memory and 50 GB disk capacity or above**. If your source instance is below this specification, upgrade it first.
- The minimum specification of a read-only instance is 1 GB memory and 50 GB disk capacity, which must be equal to or greater than the storage capacity purchased for the source instance.
- Up to five read-only instances can be created for a source instance.
- Backup and rollback features are not supported.
- Data cannot be migrated to read-only instances.
- Database creation/drop are not supported and neither is phpMyAdmin (PMA).
- Operations including account creation/deletion/authorization and account name/password modification are not supported.

## Notes
- There is no need to maintain accounts or databases for read-only instances, which are synced with those of the source instance.
- If the MySQL version is 5.6 but GTID is not enabled, you need to enable GTID in the console first before creating a read-only instance.
The operation takes a long time, and the instance will be disconnected for several seconds. We recommend you do so during off-peak hours and add a reconnection mechanism in the programs that access the database.
- Read-only instances only support the InnoDB engine.
- Data inconsistency between multiple read-only instances may occur due to the delay in data sync between the read-only instances and the source instance. You can check the delay in the console.
- The specification of a read-only instance can be different from that of the source instance, which makes it easier for you to upgrade the read-only instance based on your business load. We recommend you keep the same specifications of read-only instances in one read-only group.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. Click **Add Read-Only Instance** in the **Instance Architecture Diagram** section on the **Instance Details** tab or click **Create** on the **Read-Only Instance** tab.
3. On the purchase page, select the desired read-only instance configuration, confirm that everything is correct, and click **Buy Now**.
>?If you need to unify the expiration time of the source and read-only instances, you can set the collective expiration date in the [Renewal Management console](https://console.cloud.tencent.com/account/renewal) as instructed in [Renewal Management](https://intl.cloud.tencent.com/document/product/555/7454).
>
 - **Specify RO Group**: You can use the read-only group automatically assigned by the system allocation, create one, or select an existing one.
    - **Assigned by system**: If multiple instances are purchased at a time, each of them will be assigned to an independent read-only group, and their weights will be automatically assigned by the system by default.
    - **Create RO group**: Create a read-only group. If multiple instances are purchased at a time, all of them will be assigned to this new read-only group, and their weights will be allocated by the system automatically by default.
    - **Existing RO group**: Specify an existing read-only group. If multiple read-only instances are purchased at a time, all of them will be assigned to the read-only group.
    Their weights will be allocated as configured in the read-only group. If assignment by the system is set for the read-only group, the instances will be added to the group automatically according to the purchased specifications. If custom allocation is set, their weights will be zero by default.
		As the same private IP is shared within a read-only group, if a VPC is used, the same security group settings will be shared. If a read-only group is specified, it is not possible to customize any security group when instances are purchased.
 >- Remove Delayed RO Instances: This option indicates whether to enable the removal policy. If a read-only instance is removed when its delay exceeds the threshold, it will become inactive, its weight will be set to 0 automatically, and warning notifications will be sent out. The instance will be put back into the read-only group when its delay falls below the threshold. No matter whether this option is enabled, a read-only instance that is removed due to instance failure will rejoin the read-only group when it is repaired. For more information on how to configure the read-only instance removal alarm and recipients, see [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
![](https://main.qcloudimg.com/raw/5c002d37fdeb72a5396a394133672338.png)
4. After the purchase is completed, you will be redirected to the instance list. After the status of the instance is displayed as **Running**, it can be used normally.

## FAQs
#### What are the rules for removing read-only instances?
After **Remove Delayed RO Instances** is enabled, the read-only group will determine the removal rule based on the delay threshold and "Least RO Instances" value. If a read-only instance's delay exceeds the threshold, it will be removed and become inactive, its weight will be set to 0, and an alarm will be sent. It will be put back into the read-only group when its delay falls below the threshold.
- Delay Threshold: This sets a delay threshold for the read-only instance. When the threshold is exceeded, the instance will be removed from the read-only group.
- Least RO Instances: This is the minimum number of instances that should be retained in the read-only group. When there are fewer instances in the read-only group, even if an instance exceeds the delay threshold, it will not be removed.

#### If read-only instances are terminated or returned, how will the source instance be affected?
The termination and return of read-only instances have no impact on the source instance.



