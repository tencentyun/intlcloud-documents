### Overview 
TencentDB for MongoDB allows users to create one or more read-only instances to support read/write separation application scenarios, thus releasing the request stress on the master instance and improving the read load capacity of users' business.
>! 
- The feature of creating read-only instances is implemented based on the whitelist. If you need to use this feature, submit a ticket.
- Synchronization latency between the read-only instances and the master instance can be viewed on the console.
- Due to delay in data synchronization, the real-timeness of data synchronization for read-only instances may not be guaranteed. If the business requires read/write separation and high real-timeness, it is recommended that the business read the slave nodes of the master instance. For more information, see [Connection Example](https://cloud.tencent.com/document/product/240/3563).


### Basic architecture 
Changes on the master instance are synced to read-only instances using oplog. Each read-only instance uses a "1 master, 2 slaves" architecture at least. The architecture is shown as below:
![](https://main.qcloudimg.com/raw/dd4316c0d814aabfb1f05bf337976c1c.svg)

### Use limits  
- Backup and rollback: Backup and rollback are not supported.
- Data migration: Migrating data to read-only instances is not supported.
- Database management: Creation and deletion of databases are not supported.
- Account management: Account creation/deletion, password reset and account authorization are not supported.
- A maximum of 3 read-only instances can be created for one master instance.
- Read-only instances can be created only for monthly subscription master instances.
- The engine of a read-only instance is consistent with that of the master instance.

### Billing description  
Read-only instances only support monthly subscription billing.
### Creation steps
The steps for creating a read-only instance are as below:
- Step 1. On the instance list, click **More** -> **Management**.
	![](https://main.qcloudimg.com/raw/708eae19f300afe99a69281e9e02a6b6.png)
- Step 2. Click the **Read-only Instance** tab.
	![](https://main.qcloudimg.com/raw/beb2aa1493bbcc1f25ce8a21846f7fbc.png)
- Step 3. Click the **New** button. After the purchase is completed, the read-only instance is created successfully.
	![](https://main.qcloudimg.com/raw/ebf55c6f6de21886f570c820c6baa8e5.png)

