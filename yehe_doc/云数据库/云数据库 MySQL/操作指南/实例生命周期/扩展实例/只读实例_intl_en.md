## Operation Scenarios
TencentDB for MySQL now allows you to create one or more read-only instances, which are suitable for read/write separation and one-master-multiple-slave application scenarios and capable of greatly enhancing the read load capacity of your database.
Unified read/write separation addresses (i.e., read and write requests are separated automatically) are not supported currently. Read-only instances need to be accessed with separate IPs and ports.

**Basic concepts**
- RO group: it consists of one or more load balancing-enabled read-only instances. If there are multiple read-only instances in one RO group, read request volume can be evenly distributed among the instances. RO groups provide IPs and ports for access to databases.
- Read-only instance: a single-node (with no slave) instance that supports read requests. A read-only instance cannot exist independently; instead, it must be in an RO group.

**Basic architecture**
The MySQL master/slave binlog sync feature is adopted for read-only instances, which can sync the changes in the master instance (source database) to all read-only instances. Given the single-node architecture (without a slave) of read-only instances, repeated attempts to restore a failing read-only instance will be made. Therefore, you are recommended to choose an RO group over a read-only for higher availability.
![](https://main.qcloudimg.com/raw/bf2ef3ecfc232f6e69a99ead319a5cb2.png)


## Feature Limits
Read-only instances can be purchased only for source instances of high-availability edition on MySQL 5.6 or above with the InnoDB engine at a specification of 1 GB memory and 50 GB disk capacity or above. If your source instance is below this specification, please upgrade it first.
- The minimum specification of a read-only instance is 1 GB memory and 50 GB disk capacity and must be at least 1.1 times the storage capacity used by the master instance.
- A master instance can create up to 5 read-only instances.
- Backup and rollback features are not supported.
- Data cannot be migrated to a read-only instance.
- Database creation and dropping are not supported and neither is phpMyAdmin (PMA).
- Operations including account creation, deletion, authorization and account name/password modification are not supported.

## Notes
- There is no need to maintain account and database for read-only instances, which will be synced with those of the master instance.
- If the MySQL version is 5.6 but GTID is not enabled, you need to enable GTID in the console first before creating a read-only instance.
The operation takes a long time, and the instance will be disconnected for several seconds. You are recommended to do so during off-hours and add a reconnection mechanism in the programs that access the database.
- Read-only instances only support the InnoDB engine.
- Data inconsistency between multiple read-only instances may occur due to the delays in data sync. You can check the sync between master instance and read-only instance in the console.
- The specification of a read-only instance can be different from that of the master instance, which makes it easier for you to upgrade the instance according to the load. You are recommended to keep the same specifications of read-only instances in the same RO group.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/).
2. In the instance list, select the instance for which to create a read-only instance and click **Manage** in the "Operation" column.
3. On the **Instance Details** tab, click **Add Read-Only Instance** in the instance architecture to enter the read-only instance management page.
![](https://main.qcloudimg.com/raw/09902e5af5ef3530bd2ade5a5dc0e616.png)
4. On the **Read-Only instance** tab, click **Create**.
5. Select the desired read-only instance configuration on the purchase page. After confirming that everything is correct, click **Buy Now**.
>
![](https://main.qcloudimg.com/raw/5c002d37fdeb72a5396a394133672338.png)
5. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.
