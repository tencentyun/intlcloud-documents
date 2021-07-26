
TencentDB for PostgreSQL allows you to create one or more read-only replicas, which is suitable for read/write separation and one-primary-multiple-secondary application scenarios and capable of greatly enhancing the read load capacity of your databases.

Unified read/write separation addresses (i.e., read and write requests are separated automatically) are not supported currently. You can access read-only replicas with separate IPs and ports, or add them to a read-only replica group (RO group) to balance their loads.

>?For more information on read-only replica fees, please see [Pricing](https://intl.cloud.tencent.com/document/product/409/4993). Currently, read-only replicas do not support monthly subscription.

#### Concepts
- Read-only replica group (RO group): it consists of one or more load balancing-enabled read-only replicas. If there are multiple read-only replicas in one RO group, read requests can be evenly distributed among the replicas. RO groups provide IPs and ports for access to databases.
- Read-only replica: it is a single-node (without a secondary node) instance that supports read requests. A read-only replica cannot exist independently; instead, it must belong to a primary instance.

#### Architecture
Read-only replicas adopt PostgreSQL streaming replication, which can sync the changes in the primary instance to all read-only replicas. Given the single-node architecture (without a secondary node) of read-only replicas, repeated attempts to restore a failing read-only replica will be made. Therefore, we recommend that you use an RO group to manage read-only replicas for higher availability.
![](https://main.qcloudimg.com/raw/bf2ef3ecfc232f6e69a99ead319a5cb2.png)

## Feature Limits
- The minimum disk capacity for a read-only replica must be greater than or equal to the storage capacity used by the primary instance.
- Up to six read-only replicas can be created for a primary instance.
- Backup and rollback features are not supported.
- Data cannot be migrated to read-only replicas.
- Databases can be neither created in nor deleted from read-only replicas.
- Operations including account creation/deletion/authorization and account name/password modification are not supported.

## Notes
- There is no need to maintain accounts or databases for read-only replicas, which are synchronized with those of the primary instance.
- Data inconsistency between multiple read-only replicas may occur due to the delay in data sync between the read-only replicas and the primary instance. You can check the delay in the console.
- The specification of a read-only replica can be different from that of the primary instance, which makes it easier for you to upgrade the read-only replica according to the load. We recommend you keep the same specifications of read-only replicas in one RO group.

## Directions
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click the instance ID or **Manage** in the **Operation** column to access the instance management page.
2. Click **Add Read-only Replica** in the **Instance Architecture Diagram** section on the **Instance Details** tab or click **Create** on the **Read-only Replica** tab.
![](https://main.qcloudimg.com/raw/a5bb132bfaa35bb3529fa040dc021d9f.png)
3. On the displayed purchase page, specify the following read-only replica configurations, confirm that everything is correct, and click **Buy Now**.
 - **Specify RO Group**: create an RO group, specify an existing RO group, or do not specify any RO group for the time being.
    - **Create RO Group**: if multiple read-only replicas are purchased at a time, all of them will be assigned to the newly created RO group. The RO group automatically allocates read weights to each read-only replica, and automatically distributes read requests among the read-only replicas based on their read weights. For more information, please see [Creating RO Groups](https://intl.cloud.tencent.com/document/product/409/39546).
    - **Existing RO Group**: specify an existing RO group. If multiple read-only replicas are purchased at a time, all of them will be assigned to the RO group.
 - **Remove Read-only Replicas Exceeding the Delay Threshold**: remove a read-only replica from the RO group if the data sync log size difference between the primary instance and the read-only replica is greater than the specified threshold (MB).
4. After the purchase is completed, you will be redirected to the instance list. After the status of the read-only replica is displayed as **Running**, it can be used normally.
