## Operation Scenario
For applications with high requirements of service continuity, data reliability, and compliance, TencentDB for MySQL provides disaster recovery instances to help enhance your capability to deliver continued services at low costs and improve data reliability.

### Features
- With a separate database connection address, a disaster recovery instance can offer read access capability for various scenarios such as local access and data analysis with lower costs of device redundancy.
- Its highly available master/slave architecture helps avoid single points of failure in databases.
- It is billed in a pay-as-you-go manner and supports tiered pricing, so the longer it is used, the cheaper it is.
- Its data sync achieved through private network Direct Connect line features lower sync latency and higher stability, with the sync linkage being much better than the public network.
- Direct Connect is currently free of charge during the promotion period. If fees will be charged for it, we will inform you in advance.

### How It Works
- If a TencentDB instance is used as a disaster recovery database, the disaster recovery instance will be the backup of the master instance.
- When any change takes place in the master instance, the log information recording the change will be copied to the disaster recovery instance and then data sync will be implemented through log replay.
* If any failure occurs in the master instance, the disaster recovery instance can be activated in seconds to restore full read/write capability.

### Functional Limitations
* Currently, disaster recovery instance does not support the following features: project transfer, rollback, SQL operation, parameter settings, character set change, account management, port change, data import, rollback logging, and read-only instance.

## Prerequisites
Before creating a disaster recovery instance, make sure that the master instance is on MySQL v5.6 or higher and the GTID feature has been enabled.

## Directions
### Purchasing a Disaster Recovery Instance
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/).
2. In the instance list, select the instance for which to configure disaster recovery and click the instance name or **Manage** in the "Action" column to enter the instance management page.
3. Make sure that the GTID feature is enabled by viewing the basic information of the instance on the **instance details** page. Click **Add a Disaster Recovery Instance** in the instance architecture to enter the disaster recovery instance purchase page.
<!--![](https://main.qcloudimg.com/raw/d41ae3d97935763b180f2e8a26cb2364.png)-->
4. On the purchase page, set basic information of the disaster recovery instance such as **Billing Mode**, **Region**, and **Sync Policy**. After confirming that everything is correct, click **Buy Now** and wait for delivery.

### Creating a Sync Link
If you select **Sync Now** as the **sync policy** during purchase, the disaster recovery instance will sync data immediately after delivery. In this case, there is no need to create a sync link and you can skip this step.
If **Sync After Creation** is selected, you need to configure the disaster recovery sync link after the instance is delivered successfully. By doing so, you can implement remote disaster recovery.

1. On the **instance details** page of the master instance, you can view the sync status of the disaster recovery instance. Click **Create Sync Task** to create a private network sync linkage with the master instance for the disaster recovery instance.
<!--![](https://main.qcloudimg.com/raw/f2f941ccf588d54cb2687cc0a9d0a961.png)-->
2. Enter the task name, confirm the source and target database information, and click **Save and Next**.
<!--![](https://main.qcloudimg.com/raw/5a2b3ef40de69af903cc60396d8f1a84.png)-->
3. Select the object to be synced. Sync of the entire instance or certain tables is supported. The sync type cannot be customized currently.
<!--![](https://main.qcloudimg.com/raw/ac3f2db7c68f708ac07bb597a420ae83.png)-->
4. Click **Save and Check** to **check the task**. After the check succeeds, click **Start Task**. Then, you can view the task details on the **disaster recovery sync** page in the console.
<!--![](https://main.qcloudimg.com/raw/6b356c5e2673036e1b142d51a5de8336.png)-->
<!--![](https://main.qcloudimg.com/raw/4cc319646447bb20a5a76982a0783a49.png)-->

### Managing a Disaster Recovery Instance
- **View a disaster recovery instances**
  A disaster recovery instance can be viewed from the regions where it resides. You can use the instance list to filter out all instances in a specific region.
	<!--![](https://main.qcloudimg.com/raw/1ade1aa59f7c5cd74b2cf30299d31cac.png)-->
- **View slave-master relationship**
  Click the icon on the right of a disaster recovery instance or master instance to view the slave-master relationship.
  <!--![](https://main.qcloudimg.com/raw/4b98a6b2831c027af52a37050aa16f2d.png)-->
	<!--![](https://main.qcloudimg.com/raw/f08c6d3dd53a40ea544bdadc9e111ee8.png)-->
- **View sync delay**
  View the sync delay between the master instance and the disaster recovery instance at the top of the **instance details** page of the disaster recovery instance.
<!--![](https://main.qcloudimg.com/raw/d06a9c821f5ebd04173ee6e453ef5ef2.png)-->
- **Disaster recovery instance functions**
  A disaster recovery instance has various features, such as instance details viewing, instance monitoring, backup management, and slow query logging.
 
### Promoting a Disaster Recovery Instance to a Master Instance
1. In the instance list, select the disaster recovery instance to be promoted to a master instance and click **Manage**.
2. Enter the management page. Click **Switch to Master Instance** in the top-right corner to promote the disaster recovery instance to a master instance. After the promotion, the sync link with the master instance will be disconnected, so that the promoted instance can obtain data write capability and full MySQL functionality.
>The disconnected sync link cannot be reconnected. Please proceed with caution.
> 
<!--![](https://main.qcloudimg.com/raw/c4e1517d56c630ff845c89060402e657.png)-->

### Switching a Disaster Recovery Instance Back to a Master Instance
After the service is resumed in the region where the master instance resides, with the help of TencentDB for MySQL technical support team, you can perform reverse data sync and check and then switch the disaster recovery instance back to the master instance.

## Notes
- If the cold backup before rollback or disaster recovery does not contain the table, the rollback or disaster recovery will fail.
- If the rollback or disaster recovery involves composite operations on other database tables during the trace of binlogs, the SQL statement may fail.
- If the rollback or disaster recovery involves foreign keys and other constraints of the table during the trace of binlogs, the SQL statements may fail.
