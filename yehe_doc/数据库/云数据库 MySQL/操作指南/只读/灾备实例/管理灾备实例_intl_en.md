## Overview
For applications with high requirements of service continuity, data reliability, and compliance, TencentDB for MySQL provides cross-region disaster recovery instances to help enhance your capability to deliver continued services at low costs and improve data reliability.
>?A disaster recovery instance costs the same as the source instance associated with it. For more information, see [Product Pricing](https://buy.cloud.tencent.com/price/cdb).

#### Features
- With a separate database connection address, a disaster recovery instance can offer read access capability for various scenarios such as nearby access and data analysis with lower costs of device redundancy.
- Its highly available source/replica architecture helps avoid single points of failure for databases.
- Data is synced over a private network with lower latency and higher stability compared to public network.
- The traffic of data sync over the private network is currently free of charge during the promotion period. Start date of charging for commercial purpose is subject to further notice.

#### How it works
- If a TencentDB instance is used as a disaster recovery database, this instance will be the backup of the source instance.
- When any change takes place in the source instance, the log information recording the change will be copied to the disaster recovery instance and then data sync will be implemented through log replay.
- If any failure occurs in the source instance, the disaster recovery instance can be activated in seconds to provide full read/write capability.

## Feature limits
- Disaster recovery instances cannot be created for single-node instances of the cloud disk edition.
- Disaster recovery instances can be purchased only for high available GTID-enabled source instances on MySQL 5.6 or later with the InnoDB engine at a specification of 1 GB memory and 50 GB disk capacity or above. If your source instance is below this specification, upgrade it first.
>?If GTID is not enabled, you can enable it on the instance details page in the [console](https://console.cloud.tencent.com/cdb/). This operation takes a long time, and the instance will be disconnected for several seconds. We recommend that you do so during off-peak hours and add a reconnection mechanism in the programs that access the database.
- The minimum specification of a disaster recovery instance is 1 GB memory and 50 GB disk capacity and must be at least 1.1 times the storage capacity used by the source instance.
- One source instance can have one disaster recovery instance at most. Even if the existing disaster recovery instance is in isolation, you cannot create new ones.
- Disaster recovery instance does not support the following features: transferring project, rollback, SQL operation, changing character set, account management, changing port, data import, rollback log, and read-only instance.

## Creating a disaster recovery instance
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the details page.
2. Make sure that the GTID feature is enabled by viewing the basic information of the instance on the **Instance Details** page. Click **Add Disaster Recovery Instance** in the instance architecture diagram to enter the disaster recovery instance purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/3535c0274c3dfa18134ccc735edd0f46.png)
3. On the purchase page, set basic information of the disaster recovery instance such as **Billing Mode** and **Region**.
 >?
>- The time required to complete the creation depends on the amount of data, and no operations can be performed on the source instance in the console during the creation. We recommend you do so at an appropriate time.
>- If the sync policy is **Sync Now**, the data will be synced immediately when the disaster recovery instance is created.
>- Only the data of the entire instance can be synced. Make sure that the disk space is sufficient.
>- You need to ensure that the source instance is in the running state and none of configuration adjustment tasks, restart tasks, and other modification tasks are executed. Otherwise, the sync task may fail. 
>
4. After confirming that everything is correct, click **Buy Now** and wait for the delivery of disaster recovery instance.
5. Return to the instance list. After the status of the instance changes to **Running**, it can be used normally.

## Managing a disaster recovery instance
- **View a disaster recovery instance**
A disaster recovery instance can be viewed from the region where it resides. You can use the instance list to filter out all instances in a specific region.
![](https://qcloudimg.tencent-cloud.cn/raw/096486c7562d5385bfd50a187f85b307.png)
- **View the relationship**
Click the icon on the right of a disaster recovery instance or source instance to view their relationship.
![](https://qcloudimg.tencent-cloud.cn/raw/89d342733d4c2264dd5dc00a1c7d4143.png)
- **View sync delay**
View the sync delay between the source instance and the disaster recovery instance at the top of the **Instance Details** page of the disaster recovery instance.
![](https://qcloudimg.tencent-cloud.cn/raw/053c38735dd3dd5b7e46d5c82687dd09.png)
- **Disaster recovery instance features**
A disaster recovery instance has various features, such as instance details, instance monitoring, database management, security group, and backup and restoration.

## Promoting a disaster recovery instance to a source instance
You can promote a disaster recovery instance to source instance in the console as needed.
>!
>- After the disaster recovery instance is promoted to source instance, it will replace the original one as the new source instance to continue your business, and its access address will change. Therefore, you need to update the new address for your business.
>- After the promotion, the sync link to the original source instance will be disconnected and cannot be reconnected. You must exercise caution with this operation.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the ID of the disaster recovery instance to be promoted in the instance list, and access the instance management page.
2. Click **Promote to Source Instance** in the top-right corner to promote the disaster recovery instance to source instance. After the promotion, the sync link with the original source instance will be disconnected, so that the promoted instance can get data write capability and full MySQL functionality.
![](https://qcloudimg.tencent-cloud.cn/raw/5eb3f1f08b46d4c20ab3b4038309ab03.png)

