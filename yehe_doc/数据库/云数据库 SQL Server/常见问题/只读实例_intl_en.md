
### How do I view a read-only instance in TencentDB for SQL Server?
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, instances with an **R** tag are read-only instances. Click the ID of a read-only instance or **Manage** in the **Operation** column to enter its details page.
2. In the **Instance Architecture Diagram** on the read-only instance details page, you can view the information of the bound primary instance and click its ID to enter the primary instance details page. You can also enter the read-only instance details page from the **Instance Architecture Diagram** of the primary instance.
In addition, some features on the read-only instance details page cannot be modified and are synced from the primary instance. If you need to change them, do so on the primary instance details page. For more information, see [Managing Read-Only Instance](https://www.tencentcloud.com/document/product/238/43143).

### Does TencentDB for SQL Server support read/write separation?
Currently, TencentDB for SQL Server doesn't support unified read/write separation addresses (i.e., separating read and write requests automatically), and read-only instances can be accessed only at separate IPs and ports. After creating read-only instances, to send write requests to the primary instance and read requests to read-only instances respectively, you should configure the connection addresses of the primary instance and each read-only instance in your application. For more information, see [Read-Only Instance Overview](https://www.tencentcloud.com/document/product/238/43142).

### How do I create a read-only instance in TencentDB for SQL Server?
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click the ID of an instance or **Manage** in the **Operation** column to enter its details page.
2. Click **Add Read-Only Instance** in **Instance Architecture Diagram** on the **Instance Details** tab, or click **Create** on the **Read-Only Instance** tab to enter the purchase page. For more information, see [Managing Read-Only Instance](https://www.tencentcloud.com/document/product/238/43143).

### How do I create an RO group in TencentDB for SQL Server?
TencentDB for SQL Server allows you to create one or multiple read-only instances to form an RO group, which is suitable for read/write separation and one-primary-multiple-replica scenarios and capable of greatly enhancing the read load capacity of your database. For more information, see [Read-Only Group](https://www.tencentcloud.com/document/product/238/43144).

[](id:TBYCDS)
### How long is the sync delay between the TencentDB for SQL Server primary and read-only instances?
SQL Server versions earlier than 2017 use replication sync, which has a delay of 3–5 seconds. If you use the Always On read-only replica feature of SQL Server 2017 and 2019, the sync delay is 1–2 seconds.

### Are there any differences between read-only instances on different versions? Which version should I choose?
Read-only instances vary by version. If your business requires read-only instances, we recommend that you choose instances on v2017 or later for the following reasons:
- On versions earlier than 2017, the publish/subscribe mode is used to create read-only instances, and data can be synced at the object level with a delay of 3–5 seconds. To use read-only instances, we recommend that you upgrade the primary instance to v2017 or later first in order to guarantee an efficient and stable data sync.
- In 2017 Enterprise and later two-node architecture (formerly High Availability/Cluster Edition), the Always On mode is used to create read-only instances, and data sync is more efficient and stable with a delay of 1–2 seconds.

### Can I use accounts created in the primary instance in read-only instances?
Accounts created in the primary instance will be synced to read-only instances but cannot be managed there. They support only read but not write operations in read-only instances.

### How many read-only instances can I create for a TencentDB for SQL Server primary instance at most?
You can create up to three read-only instances for a primary instance. To create more, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Does TencentDB for SQL Server support data migration to read-only instances?
No.

### Do TencentDB for SQL Server read-only instances support database creation/deletion?
No. If needed, do so in the primary instance.

### Do TencentDB for SQL Server read-only instances support account creation/deletion?
Read-only instances don't support account creation/deletion/authorization or account name/password change. If needed, do so in the primary instance.

[](id:BFHHD)
### Do TencentDB for SQL Server read-only instances support backup and rollback?
No. If needed, do so in the primary instance.

### Do I need to enable load rebalancing after customizing weights in TencentDB for SQL Server?
If load rebalancing is disabled, modifying weights will only take effect for new loads but will not affect the read-only instances accessed by original persistent connections or cause momentary disconnections from the database. If load rebalancing is enabled, all connections to the database will be momentarily disconnected, and the loads of new connections will be balanced according to the configured weights. You can choose whether to enable this feature as needed.

