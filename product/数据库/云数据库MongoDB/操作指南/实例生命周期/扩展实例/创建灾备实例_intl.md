### Overview 
TencentDB for MongoDB allows users to create one or more disaster recovery instances for applications with a strong demand for continued services and reliable data or regulatory requirements, helping users enhance their capability to deliver continued services at a low cost and improve data reliability.
>!
- The feature of creating disaster recovery instances is implemented based on the whitelist. If you need to use this feature, submit a ticket.
- Due to delay in data synchronization, the real-timeness of data synchronization for disaster recovery instances may not be guaranteed. Synchronization latency between the disaster recovery instances and the master instance can be viewed on the console.

### How does it work 
Changes on the master instance are synced to disaster recovery instances using oplog. Each disaster recovery instance uses a "1 master, 2 slaves" architecture at least. If any failure occurs with the master instance, the disaster recovery instances can be activated in seconds to recover business reading and writing.
### Use limits 
- Backup and rollback: Backup and rollback are not supported.
- Data migration: Migrating data to read-only instances is not supported.
- Database management: Creation and deletion of databases are not supported.
- Account management: Account creation/deletion, password reset and account authorization are not supported.
- A maximum of 3 disaster recovery instances can be created for one master instance.
- Disaster recovery instances can be created only for monthly subscription master instances.
- The engine of a disaster recovery instance is consistent with that of the master instance.
- Due to network isolation, you cannot create disaster recovery instances in finance zones for master instances in common regions, and vice visa.

### Billing description 
Read-only instances only support monthly subscription billing.

### Creation steps 
The steps for creating a read-only instance are as below:
- Step 1. On the instance list, click **More** -> **Management**.
	![](https://main.qcloudimg.com/raw/708eae19f300afe99a69281e9e02a6b6.png)
- Step 2. Click the **Disaster Recovery Instance** tab.
	![](https://main.qcloudimg.com/raw/d189ed8906f9b4130892ad1104444809.png)
- Step 3. Click the **New** button. After the purchase is completed, the read-only instance is created successfully.
	![](https://main.qcloudimg.com/raw/f3a793223473a283c7f96e1dbf026f4c.png)

