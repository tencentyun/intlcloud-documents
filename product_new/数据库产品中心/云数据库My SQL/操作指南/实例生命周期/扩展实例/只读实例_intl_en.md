## Operation Scenario
TencentDB for MySQL allows you to create one or more read-only (RO) instances, which can be used to support read-write separation and one-master-multiple-slave application scenarios and boost the read load capacity of your databases.
Unified read-write separation addresses (i.e., read and write requests are separated automatically) are not supported currently. RO instances need to be accessed with separate IPs and ports.

**Terms**
- **RO group**: It consists of one or more load balancing-enabled RO instances. If there are multiple RO instances in one RO group, read request volume can be evenly distributed among the instances. RO groups provide IPs and ports for access to databases.
- **RO instance**: A single-node (with no slave) instance that supports read requests. An RO instance cannot exist independently; instead, it must be in an RO group.

## Basic Architecture
The MySQL master-slave binlog sync feature is adopted for RO instances, which can sync the changes in the master instance (source database) to all RO instances. Given the single-node architecture (without a slave) of RO instances, repeated attempts to restore a failing RO instance will be made. Therefore, you are recommended to choose an RO group over an RO instance for higher availability.
![](https://mc.qcloudimg.com/static/img/3f2a163d690deda5978474f8db4b8738/image.png)

## Functional Limitations
- RO instances are only available to **high-IO master instances on MySQL 5.6 or higher with at least 1 GB of memory and 50 GB of disk capacity**. If a master instance has a lower specification, please upgrade its specification first.
- The minimum specification of an RO instance is 1 GB memory and 50 GB disk capacity and must be at least 1.1 times the storage capacity occupied by the master instance.
- A master instance can create up to 5 RO instances.
- An RO instance can have a different specification from the master instance, so you can upgrade its specification based on the load.
- Backup and rollback features are not supported.
- Data cannot be migrated to an RO instance.
- Database creation/deletion is not supported and neither is phpMyAdmin (PMA).
- Operations including account creation/deletion/authorization and account name/password modification are not supported.

## Precautions
- There is no need to maintain the accounts and databases of RO instances, as they are synced from the master instance.
- If the MySQL version is 5.6 but GTID is not enabled, you need to enable GTID in the console first before creating an RO instance.
It takes a relatively long time to enable GTID, and the instance will suffer an interruption lasting for seconds. It is recommended to perform the operation during off-hours and add a reconnection mechanism in the program accessing the database.
- Only the InnoDB storage engine is supported for RO instances, which can be created only for master instances with InnoDB.
- Data inconsistency between multiple RO instances may occur due to the delays in data sync. You can check the delay in master-RO sync in the console.
- It is recommended to ensure that all RO instances in the same RO group have the same specification.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/).
2. In the instance list, select the TencentDB instance for which you want to create an RO instance and click **Manage** in the "Operation" column.
3. On the **Instance Details** tab, click **Add Read-Only Instance** in the instance architecture to enter the RO instance management page.
![](https://main.qcloudimg.com/raw/91bde52130ced8dd443adb978c9d7c14.png)
4. On the **Read-only instance** tab, click **Create**.
5. Select the desired configuration for the RO instance on the purchase page, confirm that everything is correct, and then click **Buy Now**.
>If you want the master instance and RO instances to have the same expiry date, you can set a collective expiry date in the [Renewal Management Console](https://console.cloud.tencent.com/account/renewal) as instructed in [Unify Expiry Date](https://cloud.tencent.com/document/product/555/7454#.E7.BB.9F.E4.B8.80.E5.88.B0.E6.9C.9F.E6.97.A5).
>
![](https://main.qcloudimg.com/raw/7774b64f4e25e965fd2f119ce4e17acd.png)

