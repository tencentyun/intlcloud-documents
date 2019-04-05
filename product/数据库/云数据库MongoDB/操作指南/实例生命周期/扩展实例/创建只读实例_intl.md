### Overview
TencentDB for MongoDB allows users to create one or more read-only instances to separate read/write operations, which can help reduce the request amount sent to the master instance and improve the read loading capacity.
>!
Creating read-only instances is currently whitelisting. Please submit a ticket for the service.
You can find the synchronization latency between the read-only instances and the master instance on the console.
Due to the delay in data synchronization, read-only instances may not synchronize the data in real-time. If your business needs to separate read/write operations and real-time data synchronization, we recommend you read data from the slave nodes of the master instance. For more information, see [Connection Example](https://cloud.tencent.com/document/product/240/3563).


### Basic architecture
Changes on the master instance can be synced to read-only instances using oplog. Each read-only instance have at least 1 master and 2 slaves. The figure below describes the architecture:
![](https://main.qcloudimg.com/raw/dd4316c0d814aabfb1f05bf337976c1c.svg)

### limitation
 - Backup and rollback: Not supported.
 - Data migration: Do not support migrating data to read-only instances.
 - Database management: Do not support Creating and deleting a database.
 - Account management: Do not support creating/deleting accounts,  resetting passwords and authorizing accounts.
 - Up to 3 read-only instances allowed for each master instance.
 - Only prepaid (monthly/yearly subscription) master instances can create read-only instances.
 - The engine of a read-only instance is consistent with that of the master instance.

### Billing  
Read-only instances only support prepaid (monthly/yearly subscription) billing method.
### Create a read-only instance
Steps for creating a read-only instance:
- Step 1. On the instance list, click **More** -> **Management**.
	![](https://main.qcloudimg.com/raw/708eae19f300afe99a69281e9e02a6b6.png)
- Step 2. Click the **Read-only Instance** tab.
	![](https://main.qcloudimg.com/raw/beb2aa1493bbcc1f25ce8a21846f7fbc.png)
- Step 3. Click the **New** button. You successfully create a read-only instance (the purchase is completed). 
	![](https://main.qcloudimg.com/raw/ebf55c6f6de21886f570c820c6baa8e5.png)

