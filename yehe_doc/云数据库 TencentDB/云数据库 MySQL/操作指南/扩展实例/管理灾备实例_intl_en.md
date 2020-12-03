## Operation Scenarios
For applications with high requirements for service continuity, data reliability, and compliance, TencentDB for MySQL provides cross-region disaster recovery instances to help enhance your capability to deliver continued services at low costs and improve data reliability.

#### Features
- With a separate database connection address, a disaster recovery instance can offer read access capability for various scenarios such as nearby access and data analysis with lower costs of device redundancy.
- Its high-availability master/slave architecture helps avoid single points of failure in databases.
- Its data sync achieved through private network Direct Connect features lower sync latency and higher stability, with the sync linkage being much better than the public network.
- Direct Connect is currently free of charge during the promotion period. If fees will be charged for it, we will inform you in advance.

#### How it works
- If a TencentDB instance is used as a disaster recovery database, the disaster recovery instance will be the backup of the master instance.
- When any change takes place in the master instance, the log information recording the change will be copied to the disaster recovery instance and then data sync will be implemented through log replay.
- If any failure occurs in the master instance, the disaster recovery instance can be activated in seconds to restore full read/write capability.

## Feature Limits
- Disaster recovery instances can be purchased only for high IO GTID-enabled master instances on MySQL 5.6 or above with the InnoDB engine at a specification of 1 GB memory and 50 GB disk capacity or above. If your master instance is below this specification, please upgrade it first.
>If GTID is not enabled, you can enable on the instance details page in the [console](https://console.cloud.tencent.com/cdb/). The operation takes a long time, and the instance will be disconnected for several seconds. You are recommended to do so during off-hours and add a reconnection mechanism in the programs that access the database.
- The minimum specification of a disaster recovery instance is 1 GB memory and 50 GB disk capacity and must be at least 1.1 times the storage capacity used by the master instance.
- One master instance can have one disaster recovery instance at most. Even if the existing disaster recovery instance is in isolation, you cannot create new ones.
- Currently, disaster recovery instance does not support the following features: project transfer, rollback, SQL operation, parameter settings, character set change, account management, port change, data import, rollback logging, and read-only instance.

## Directions
### Creating disaster recovery instance
#### Step 1. Create a disaster recovery instance
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the details page.
2. Make sure that the GTID feature is enabled by viewing the basic information of the instance on the instance details page. Click **Add DR Instance** in the instance architecture diagram to enter the disaster recovery instance purchase page.

4. On the purchase page, set basic information of the disaster recovery instance such as **Billing Mode**, **Region**, and **Sync Policy**.
 - If the sync policy is "Sync Now", data will be synced immediately after the disaster recovery instance is created.
 - If the sync policy is "Sync After Creation", you need to configure a disaster recovery sync link after the instance is created successfully. For detailed directions, please see [Create a sync link](#cjtblj) below.
>
>- The time it takes to complete the creation is subject to the data volume, during which no operations can be performed on the master instance in the console. Please do so at an appropriate time.
>- Currently, data sync is supported only for the entire instance. Please make sure that the disk capacity is sufficient.
>- Make sure that the master instance is in the running status and not running any tasks; otherwise, the sync task may fail.  
5. After confirming that everything is correct, click **Buy Now** and wait for disaster recovery instance delivery.

<span id="cjtblj"></span>
#### Step 2. Create a sync link (optional)
>If the "sync policy" you selected during instance purchase is "Sync After Creation", you need to configure a disaster recovery sync link after the instance is created successfully. By doing so, you can implement remote disaster recovery.

1. On the instance details page of the master instance, you can view the sync status of the disaster recovery instance. Click **Create Sync Task** to create a private network sync linkage with the master instance for the disaster recovery instance.

2. Enter the task name, confirm the source and target database information, and click **Save and Next**.

3. Select the object to be synced. Sync of the entire instance or certain tables is supported. The sync type cannot be customized currently.

4. Click **Save and Check** to **check the task**. After the check succeeds, click **Start Task**. Then, you can view the task details on the "disaster recovery sync" page in the TencentDB for MySQL Console.


### Managing disaster recovery instance
- **View a disaster recovery instance**
  A disaster recovery instance can be viewed from the regions where it resides. You can use the instance list to filter out all instances in a specific region.
	
- **View slave-master relationship**
  Click the icon on the right of a disaster recovery instance or master instance to view the slave-master relationship.	
- **View sync delay**
  View the sync delay between the master instance and the disaster recovery instance at the top of the instance details page of the disaster recovery instance.

- **Disaster recovery instance features**
  A disaster recovery instance has various features, such as instance details viewing, instance monitoring, backup management, and slow query logging.
 
### Promoting disaster recovery instance to master instance
1. In the instance list, select the disaster recovery instance to be promoted to a master instance and click **Manage**.
2. Enter the management page. Click **Promote to master instance** in the top-right corner to promote the disaster recovery instance to a master instance. After the promotion, the sync link with the master instance will be disconnected, so that the promoted instance can get data write capability and full MySQL functionality.
>The disconnected sync link cannot be reconnected. Please proceed with caution.
> 


