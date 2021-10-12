## Overview
For applications with high requirements of service continuity, data reliability, and compliance, TencentDB for MySQL provides cross-region disaster recovery instances to help enhance your capability to deliver continued services at low costs and improve data reliability.
>?A disaster recovery instance costs the same as the source instance associated with it. For more information, see [Product Pricing](https://buy.cloud.tencent.com/price/cdb).

#### Features
- With a separate database connection address, a disaster recovery instance can offer read access capability for various scenarios such as local access and data analysis with lower costs of device redundancy.
- Its highly available source/replica architecture helps avoid single points of failure in databases.
- Its data sync achieved through private network features lower sync latency and higher stability, with the sync linkage being much better than the public network.
- The traffic of data sync through private network is currently free of charge during the promotion period. If fees will be charged for it, we will inform you in advance.

#### How it works
- If a TencentDB instance is used as a disaster recovery database, this instance will be the backup of the source instance.
- When any change takes place in the source instance, the log information recording the change will be copied to the disaster recovery instance and then data sync will be implemented through log replay.
- If any failure occurs in the source instance, the disaster recovery instance can be activated in seconds to restore full read/write capability.

## Feature Limits
- Disaster recovery instances can be purchased only for high available GTID-enabled source instances on MySQL 5.6 or above with the InnoDB engine at a specification of 1 GB memory and 50 GB disk capacity or above. If your source instance is below this specification, please upgrade it first.
>?If GTID is not enabled, you can enable it on the instance details page in the [console](https://console.cloud.tencent.com/cdb/). This operation takes a long time, and the instance will be disconnected for several seconds. You are recommended to do so during off-peak hours and add a reconnection mechanism in the programs that access the database.
- The minimum specification of a disaster recovery instance is 1 GB memory and 50 GB disk capacity and must be at least 1.1 times the storage capacity used by the source instance.
- One source instance can have one disaster recovery instance at most. Even if the existing disaster recovery instance is in isolation, you cannot create new ones.
- Disaster recovery instance does not support the following features: transferring project, rollback, SQL operation, parameter settings, changing character set, account management, changing port, data import, rollback log, and read-only instance.

## Directions
### Creating a disaster recovery instance
#### Step 1. Create a disaster recovery instance
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. Make sure that the GTID feature is enabled by viewing the basic information of the instance on the **Instance Details** page. Click **Add Disaster Recovery Instance** in the instance architecture diagram to enter the disaster recovery instance purchase page.
![](https://main.qcloudimg.com/raw/d41ae3d97935763b180f2e8a26cb2364.png)
3. On the purchase page, set basic information of the disaster recovery instance such as **Billing Mode**, **Region**, and **Sync Policy**.
 - If the sync policy is **Sync Now**, data will be synced immediately when the disaster recovery instance is created.
 - If the sync policy is **Sync After Creation**, you need to configure a disaster recovery sync link after the instance is created successfully. For detailed directions, please see [Create a sync link](#cjtblj) below.
>?
>- The time it takes to complete the creation is subject to the data volume, during which no operations can be performed on the source instance in the console. Please do so at an appropriate time.
>- Only the entire instance data can be synced. Please ensure that the disk space is sufficient.
>- You need to ensure that the source instance is in the running state and none of configuration adjustment tasks, restart tasks, and other modification tasks are executed. Otherwise, the sync task may fail.  
4. After confirming that everything is correct, click **Buy Now** and wait for disaster recovery instance delivery.
5. Return to the instance list. After the status of the instance changes to "Running", it can be used normally.

#### [Step 2. Create a sync link (optional)](id:cjtblj)
>?If the **Sync Policy** you select during instance purchase is **Sync After Creation**, you need to configure a disaster recovery sync link after the instance is created successfully. By doing so, you can implement remote disaster recovery.

1. On the **Instance Details** page of the source instance, you can view the sync status of the disaster recovery instance. Click **Create Sync Task** to create a private network sync linkage with the source instance for the disaster recovery instance.
![](https://main.qcloudimg.com/raw/f2f941ccf588d54cb2687cc0a9d0a961.png)
2. Enter the task name, confirm the source and target database information, and click **Save and Next**.
![](https://main.qcloudimg.com/raw/5a2b3ef40de69af903cc60396d8f1a84.png)
3. Select the object to be synced. Sync of the entire instance or certain tables is supported. The sync type cannot be customized currently.
![](https://main.qcloudimg.com/raw/ac3f2db7c68f708ac07bb597a420ae83.png)
4. Click **Save and Check** to check the task. After the check succeeds, click **Start Task**. Then, you can view the task details on the **Disaster Recovery Sync** page in the console.
![](https://main.qcloudimg.com/raw/4cc319646447bb20a5a76982a0783a49.png)

### Managing disaster recovery instances
- **View a disaster recovery instances**
A disaster recovery instance can be viewed from the regions where it resides. You can use the instance list to filter out all instances in a specific region.
![](https://main.qcloudimg.com/raw/1ade1aa59f7c5cd74b2cf30299d31cac.png)
- **View the relationship between the source instance and the disaster recovery instance**
Click the icon on the right of a disaster recovery instance or source instance to view their relationship.
![](https://main.qcloudimg.com/raw/4b98a6b2831c027af52a37050aa16f2d.png)
![](https://main.qcloudimg.com/raw/f08c6d3dd53a40ea544bdadc9e111ee8.png)
- **View sync delay**
View the sync delay between the source instance and the disaster recovery instance at the top of the **Instance Details** page of the disaster recovery instance.
![](https://main.qcloudimg.com/raw/d06a9c821f5ebd04173ee6e453ef5ef2.png)
- **Disaster recovery instance features**
A disaster recovery instance has various features, such as instance details viewing, instance monitoring, backup management, and slow query logging.
 
### Promoting a disaster recovery instance to source instance
You can promote a disaster recovery instance to source instance in the console as needed.
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the ID of the disaster recovery instance to be promoted in the instance list, and access the instance management page.
2. Click **Promote to Source Instance** in the top-right corner to promote the disaster recovery instance to source instance. After the promotion, the sync link with the source instance will be disconnected, so that the promoted instance can get data write capability and full MySQL functionality.
>!The disconnected sync link cannot be reconnected. Please proceed with caution.
> 
![](https://main.qcloudimg.com/raw/c4e1517d56c630ff845c89060402e657.png)

