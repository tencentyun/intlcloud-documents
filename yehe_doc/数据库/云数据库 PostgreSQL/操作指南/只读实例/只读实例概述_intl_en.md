TencentDB for PostgreSQL allows you to create one or more read-only instances. They are suitable for read/write separation and one-primary-multiple-standby application scenarios and capable of greatly enhancing the read load capacity of your database.

Unified read/write separation addresses (i.e., read and write requests are separated automatically) are not supported currently. You can access read-only instances with separate IPs and ports, or add them to a read-only instance group (RO group) to balance their loads.

>?For read-only instance pricing, see [Pricing](https://intl.cloud.tencent.com/document/product/409/4993).

#### Concepts
- RO group: It consists of one or more load balancing-enabled read-only instances. If there are multiple read-only instances in one RO group, read requests can be evenly distributed among the instances. RO groups provide IPs and ports for access to databases.
- Read-only instance: It is a single-node (with no standby) instance that supports read requests. It cannot exist independently; instead, it must belong to a primary instance.

#### Architecture
Changes in the primary instance (source database) are synced to all read-only instances through PostgreSQL's streaming replication mechanism. Given the single-node architecture (with no standby) of read-only instances, repeated attempts to restore a failed read-only instance will be made. Therefore, we recommend you choose an RO group rather than a read-only instance for higher availability.
![](https://main.qcloudimg.com/raw/bf2ef3ecfc232f6e69a99ead319a5cb2.png)

## Feature Limits
- The minimum disk capacity of a read-only instance must be greater than or equal to the storage capacity used by the primary instance.
- Up to six read-only instances can be created for a primary instance.
- Backup and rollback features are not supported.
- Data cannot be migrated to read-only instances.
- Databases cannot be created in or deleted from read-only instances.
- Operations including account creation/deletion/authorization and account name/password modification are not supported.

## Notes
- There is no need to maintain accounts or databases for read-only instances, which are synced with those of the primary instance.
- Data inconsistency between multiple read-only instances may occur due to the delay in data sync between the read-only instances and the primary instance. You can check the delay in the console and configure CM alarms.
- The specification of a read-only instance can be different from that of the primary instance, which makes it easier for you to upgrade the read-only instance based on your business load. We recommend you keep the same specifications of read-only instances in one RO group.
- If the primary instance is written so frequently that the automatic log cleanup threshold is exceeded, logs will be automatically deleted. If the standby instance hasn't obtained the deleted logs yet, the primary-standby replication will be disconnected, and the read-only instance will be automatically rebuilt and become inaccessible.
- Read-only instances don't have high availability. We recommend you use an RO group and configure at least two read-only instances to avoid business access failures caused by single points of failures.

## Directions
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. Click **Add Read-Only Instance** in the **Instance Architecture Diagram** section on the **Instance Details** tab or click **Create** on the **Read-Only Instance** tab.
![](https://main.qcloudimg.com/raw/a5bb132bfaa35bb3529fa040dc021d9f.png)
3. On the purchase page, select the desired read-only instance configuration, confirm that everything is correct, and click **Buy Now**.
 - **Specify RO Group**: Select **Do not specify for now**, **Create RO group**, or **Existing RO group**.
    - **Create RO group**: If multiple read-only instances are purchased at a time, all of them will be assigned to the newly created RO group. The RO group automatically allocates read weights to each read-only instance and automatically distributes read requests among them based on their read weights. For more information, see [Managing RO Groups](https://intl.cloud.tencent.com/document/product/409/39546).
    - **Existing RO group**: Specify an existing RO group. If multiple read-only instances are purchased at a time, all of them will be assigned to the RO group.
 - **Remove Delayed RO Instances**: Remove a read-only instance from the RO group if the data sync log size difference between the primary instance and the read-only instance is greater than the specified threshold (in MB).
 - **AZ**: You can select any AZ in the same region as the primary instance.
4. After the purchase is completed, you will be redirected to the instance list. After the status of the instance changes to **Running**, the instance can be used normally.
