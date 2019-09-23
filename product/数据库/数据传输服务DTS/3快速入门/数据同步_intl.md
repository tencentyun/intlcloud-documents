Data synchronization can be used for sync disaster recovery instances. This section introduces data synchronization feature with disaster recovery instance as an example.

## Overview
For application with a strong demand for continued services and reliable data or regulatory requirements, TencentDB provides disaster recovery instances to help users enhance their capability to deliver continued services at a low cost and improve data reliability.


## Characteristics
* With a separate database connection address, disaster recovery instances can offer read access capability for such scenarios as "connection to the nearest node" and data analysis with a lower cost in device redundancy.
* Highly available Master/Slave architecture can avoid the single point of failure (SPOF) risks of database.
* Billing on an hourly basis supports instant-on and instant-off. Adoption of tiered prices allows a lower cost for a longer usage.
* **Disaster recovery instance synchronization achieved through private network Direct Connect has a lower synchronization latency and higher stability, with the synchronization linkage being much more superior than the public network.**
* Direct Connect is free of charge during promotion period, and the date of commencement for commercial charges will be subject to the further notice.



## How Does It Work
* In a scenario where a Tencent Cloud database is used as a disaster recovery database, disaster recovery instance is the backup of the master instance database.	
* When any changes take place in the master instance, the log information recording the modification will be copied to the disaster recovery instance, and data synchronization can be achieved through log replay.
* If any failure occurs with the master instance, the disaster recovery instance can be activated in seconds for restoring the full read and write features.

## Preconditions
Before creating a disaster recovery instance, make sure that the master instance is MySQL 5.6 version or above and the GTID feature has been enabled.

## Use Limits
* Disaster recovery instance does not support the following features: transferring project, rollback, SQL operation, parameter settings, changing character set, account management, changing port change, data import, rollback log, read-only instance.

## Procedure
### Purchase a disaster recovery instance
Step 1: In the instance list, select the instance for which you want to configure a disaster recovery instance, and click **Manage**.
![](https://main.qcloudimg.com/raw/6d75a2937c02896d4844f30dae33f544.png)<br>
Step 2: Make sure the GTID feature has been enabled. Click **Add Disaster Recovery Instance** to enter the disaster recovery instance purchase page.
![](https://main.qcloudimg.com/raw/6fb1aa7c567a6c215da5585b4e93bb40.png)<br>
Step 3: On the purchase page, select the region of the disaster recovery instance. After confirming the instance information, click Activate and wait for the delivery of disaster recovery instance.
![](https://main.qcloudimg.com/raw/6ee7a3a9c078c8086fae351d6585003e.png)

### Create a synchronization link
After the delivery of disaster recovery instance, you need to configure a synchronization link for disaster recovery to achieve the remote disaster recovery.

Step 1: In the list of master instances and the "instance details" page, you can view the synchronization status of the disaster recovery instance. If "Unsynchronized" is displayed, click **Create Synchronization** to create a private network synchronization linkage with the master instance for the disaster recovery instance.
![](https://main.qcloudimg.com/raw/9a5f2c9038a5df4b751a524c8324e478.png)
![](https://main.qcloudimg.com/raw/e68b679740e3096ec174b4f4bd70bf87.png)<br>
Step 2: Enter the task name, check the source database and destination database information, and then click **Next**.
![](https://main.qcloudimg.com/raw/78adf64f234204062d4d77af8a5e4af7.png)<br>
Step 3: Select the object to be synced. Synchronization of the entire instance or only part of the database table is supported. Synchronization type cannot be selected for now.
![](https://main.qcloudimg.com/raw/059df46d855029f728e9d0e7fdf615f9.png)<br>
Step 4: Click **Save and Verify**. After the verification succeeds, you can view the task details on the TencentDB **Data Transfer** page.
![](https://main.qcloudimg.com/raw/4d4a3fb012ce1b455e046a32d32590c8.png)
![](https://main.qcloudimg.com/raw/b65b4458b3d7cc46bb4ac9b836aff1c5.png)<br>


### Manage disaster recovery instances
1. View disaster recovery instances<br>
Disaster recovery instances can be viewed in the region to which they belongs. You can filter out all the disaster recovery instances of a region in the **Instance Type** of the instance list. For each disaster recovery instance, you can view the master instance information using the icon under the instance name.
![](https://main.qcloudimg.com/raw/d96eeadfdb1d0cc0046524476c910800.png)
2. View synchronization latency<br>
You can view the synchronization latency between the master instance and the disaster recovery instance at the top of the instance details page.
![](https://main.qcloudimg.com/raw/430d17d785b202a4b5004af7e6a31e5f.png)
3. Features of disaster recovery instance<br>
Disaster recovery instance provides instance details, instance monitoring, backup management, and slow log features that can be viewed in the console.
![](https://main.qcloudimg.com/raw/73745c6e06fae64e9188d096bee80dfe.png)

### Upgrade a disaster recovery instance to a master instance
You can quickly upgrade a disaster recovery instance to a master instance in the console. After the switching, the synchronization connection between the disaster recovery instance and the master instance is broken, and the instance database data write capability and the full TencentDB features are restored.
Once the synchronization connection is broken, it cannot be reestablished. Please proceed with caution.
![](https://main.qcloudimg.com/raw/e6b9103763d4b77d3b4466b83f592804.png)

### Switch a disaster recovery instance back to a master instance
After the service is resumed in the region where the master instance resides, you can, with the help of TencentDB service personnel, perform reverse data synchronization and data verification, and then switch the disaster recovery instance back to the master instance.

## Notes
1. If the cold backup before rollback or disaster recovery does not contain the table, the rollback or disaster recovery will fail.
2. If the rollback or disaster recovery involves composite operations on other database tables during the trace of binlog, the statement may fail.
3. If the rollback or disaster recovery involves table's foreign key and other constraints during the trace of binlog, SQL statements may fail.

