## Overview
TencentDB for MySQL allows you to create one or more read-only instances, which are suitable for read/write separation and one-source-multiple-replica application scenarios and capable of greatly enhancing the read load capacity of your database.
Unified read/write separation addresses (i.e., read and write requests are separated automatically) are not supported currently. Read-Only instances need to be accessed with separate IPs and ports.
>?
>- For read-only instance pricing, see [Product Pricing](https://buy.Intl.cloud.tencent.com/price/cdb).
- You can now configure a custom and exclusive private network address (IP and port) for a read-only instance on the instance details page.

#### Concepts
- Read-Only group: it consists of one or more load balancing-enabled read-only instances. If there are multiple read-only instances in one read-only group, read request volume can be evenly distributed among the instances. read-only groups provide IPs and ports for access to databases.
- Read-Only instance: a single-node (with no replica) instance that supports read requests. It cannot exist independently; instead, it must be in a read-only group.

#### Architecture
The MySQL source-replica binlog sync feature is adopted for read-only instances, which can sync the changes in the source instance (source database) to all read-only instances. Given the single-node architecture (without a replica) of read-only instances, repeated attempts to restore a failing read-only instance will be made. Therefore, we recommend you choose an RO group over a read-only instance for higher availability.
![](https://main.qcloudimg.com/raw/bf2ef3ecfc232f6e69a99ead319a5cb2.png)

## Feature Limits
- Read-only instances can be purchased only for **two-node or three-node source instances on MySQL 5.6 or above with the InnoDB engine at a specification of 1 GB memory and 50 GB disk capacity or above**. If your source instance is below this specification, upgrade it first.
- The minimum specification of a read-only instance is 1 GB memory and 50 GB disk capacity and must be greater than or equal to the purchased storage size of the source instance.
- A source instance can create up to 5 read-only instances.
- Backup and rollback features are not supported.
- Data cannot be migrated to read-only instances.
- Database creation/deletion is not supported and neither is phpMyAdmin (PMA).
- Operations including account creation/deletion/authorization and account name/password modification are not supported.

## Notes
- There is no need to maintain accounts or databases for read-only replicas, which are synchronized with those of the primary instance.
- If the MySQL version is 5.6 but GTID is not enabled, you need to enable GTID in the console first before creating a read-only instance.
The operation takes a long time, and the instance will be disconnected for several seconds. You are recommended to do so during off-peak hours and add a reconnection mechanism in the programs that access the database.
- Read-only instances only support the InnoDB engine.
- Data inconsistency between multiple read-only replicas may occur due to the delay in data sync between the read-only replicas and the primary instance. You can check the delay in the console.
- The specification of a read-only replica can be different from that of the primary instance, which makes it easier for you to upgrade the read-only replica according to the load. We recommend you keep the same specifications of read-only replicas in one RO group.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance details page.
2. Click **Add Read-Only Instance** in the **Instance Architecture Diagram** section on the **Instance Details** tab or click **Create** on the **Read-only Replica** tab.
3. On the displayed purchase page, specify the following read-only replica configurations, confirm that everything is correct, and click **Buy Now**.
 - **Specify RO Group**: you can use the RO group automatically assigned by the system allocation, create one, or select an existing one.
    - **Assigned by system**: if multiple instances are purchased at a time, each of them will be assigned to an independent RO group, and their weights will be automatically assigned by the system by default.
    - **Create RO group**: create an RO group. If multiple instances are purchased at a time, all of them will be assigned to this new RO group, and their weights will be allocated by the system automatically by default.
    - **Existing RO group**: specify an existing RO group. If multiple read-only replicas are purchased at a time, all of them will be assigned to the RO group.
    Their weights will be allocated as configured in the RO group. If assignment by the system is set for the RO group, the instances will be added to the group automatically according to the purchased specifications. If custom allocation is set, their weights will be zero by default.
		As the same private IP is shared within an RO group, if a VPC is used, the same security group settings will be shared. If an RO group is specified, it is not possible to customize any security group when instances are purchased.
 - Remove Delayed RO Instances: this option indicates whether to enable the removal policy. If a read-only instance is removed when its delay exceeds the threshold, it will become inactive, its weight will be set to 0 automatically, and warning notifications will be sent out (for more information on how to configure the read-only instance removal alarm and recipients, see [Alarming Feature](https://intl.cloud.tencent.com/document/product/236/8457). The instance will be put back into the RO group when its delay falls below the threshold. No matter whether this option is enabled, a read-only instance that is removed due to instance failure will rejoin the RO group when it is repaired.
![](https://main.qcloudimg.com/raw/5c002d37fdeb72a5396a394133672338.png)
4. After the purchase is completed, you will be redirected to the instance list. After the status of the read-only replica is displayed as **Running**, it can be used normally.

## FAQs
#### What are the rules for removing read-only instances?
After **Remove Delayed RO Instances** is enabled, the RO group will determine the removal rule based on the delay threshold and "Least RO Instances" value. If the delay of a read-only instance reaches the threshold, it will be removed and made inactive, with its weight set to 0 and an alarm sent to user. When its delay falls below the threshold, it will be returned to the RO group.
- Delay Threshold: this sets a delay threshold for the read-only instance. When the threshold is exceeded, the instance will be removed from the read-only group.
- Least RO Instances: this is the minimum number of instances that should be retained in the read-only group. When there are fewer instances in the read-only group, even if an instance exceeds the delay threshold, it will not be removed.

#### If read-only instances are terminated or returned, how will the source instance be affected?
The termination and return of read-only instances has no impact on the source instance.
