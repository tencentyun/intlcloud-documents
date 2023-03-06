- **Storage engine**
TencentDB for MariaDB currently supports the following storage engines. We recommend that you use InnoDB as other ones may compromise the performance. You can run the `SHOW ENGINES` command to view the storage engines supported by the current database:

| Storage Engine | Supported by TencentDB | Reason for Default Disablement |
| ------------------ | ------------------ | ---------------------------------- |
| InnoDB | Yes (default) | - |
| MyISAM | Yes (you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to enable it) | It may cause data inconsistency and affect sync efficiency |
| Memory | Yes | - |
| Merge | Yes | - |
| Archive | Yes (you need to submit a ticket to enable it) | It may cause data inconsistency and affect sync efficiency |
| Federated | No | It may cause security risks |
| CSV | Yes (you need to submit a ticket to enable it) | It may cause data inconsistency and affect sync efficiency |
| BLACKHOLE | Yes | - |
| MRG_MyISAM | Yes | - |
| PERFORMANCE_SCHEMA | Yes (you need to submit a ticket to enable it) | It may cause data inconsistency and affect sync efficiency |



- **Precautions on upgrading a TencentDB instance**
During the upgrade of a TencentDB instance, the instance will be disconnected for 1–30 seconds (for switch after upgrade); therefore, you need to get prepared and enable automatic reconnection between your application and database in advance to avoid service unavailability.

- **Definitions of primary and replica in the documentation**
In TencentDB documentation, a replica server refers to the hot backup database server in the high-availability architecture. When the primary server fails, the replica server will be put into use in real time for continuous service.

- **The architecture of "1-primary-2-replicas" is recommended if strong sync is required**
When you perform strong sync replication, the primary database will be hanged if it is disconnected from the replica database or if the replica database fails. If there is only one primary or replica database, the high-availability solution will be unavailable, because if only one single server provides the service, part of the data will be lost completely when a failure occurs.
 
- **Enabling public network access for a long time and using weak passwords may lead to security risks**
A public network IP of the database is likely to be detected and scanned by malicious users if it is enabled for a long period. If you use a weak password (such as 12345678 or 1234abcd) in this case, your database may be at great security risk.

- **Notes on TencentDB for MariaDB rollback**
   - TencentDB for MariaDB supports data rollback, but we recommend that you back up your key production data before performing rollback.
   - Data will be directly rolled back into a new pay-as-you-go instance.
   - Deleting the original instance will not affect the rollback instance.

- **Notes on TencentDB locking policy**
TencentDB has a locking mechanism. If the storage capacity usage of your instance exceeds the threshold (which is usually 103–130%; the read-only threshold for TencentDB for MariaDB is 110% currently), the system will lock your instance which will become read-only. Therefore, we recommend that you periodically check the storage capacity usage and enable SMS reminder for usage in the TencentDB for MariaDB console. If you cannot expand the instance capacity timely due to financial reasons, you can submit a ticket to apply for temporary unlocking for 1–3 business days.

_ **TencentDB for MariaDB failover**
TencentDB for MariaDB adopts high-availability modes such as one primary and one replica or one primary and two replicas. When the primary database fails, TencentDB for MariaDB can switch to the replica database within 1 second (200 ms in average). However, during the switch, there may be a short period of up to 30 seconds when you cannot access the database (this period of time is used for failure detection and data sync). In this case, you need to set automatic reconnection between your application and the instance in advance to avoid service unavailability. The switch is imperceptible to the business (i.e., the IP and port remain unchanged and no human intervention is required). You only need to ensure that automatic reconnection is enabled for your business.

- **Things to do after TencentDB instance purchase:**
After purchasing a TencentDB instance, you don't need to perform basic Ops tasks, such as high-availability maintenance, backup, and security patch, but you should keep in mind the following:
 - Check whether the CPU, IOPS, space, and number of connections of your TencentDB instance are sufficient. If they become insufficient, you need to optimize or upgrade the instance.
 - Check whether your TencentDB instance has performance issues, many slow or poor SQL statements, and excessive or missing indexes.

- **You cannot modify any data in the `mysql`, `information_schema`, `performance_schema`, and `sysdb` databases.**

- **You cannot directly use SQL statements to configure accounts or grant permissions, which can only be done in the console. The following 19 common permissions are supported, while some rarely used permissions are not supported:**
SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER
CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW
CREATE ROUTINE, ALTER ROUTINE, EVENT, TRIGGER, SHOW DATABASES

- **TencentDB for MariaDB does not provide the root account**

- **We recommend that you use a public network address only for routine maintenance, rather than for connecting business servers**

