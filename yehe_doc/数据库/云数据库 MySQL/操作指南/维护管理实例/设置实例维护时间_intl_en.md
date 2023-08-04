## Overview
Maintenance time is a very important concept for TencentDB for MySQL. To ensure the stability of your TencentDB for MySQL instance, the backend system performs maintenance operations on the instance during the maintenance period from time to time. To minimize the potential impact on your business, we recommend that you set an acceptable maintenance period for your business instance, usually during off-peak hours.

In addition, we also recommend you perform operations involving data migration during the maintenance time, such as instance specification adjustment, instance version upgrade, and instance kernel upgrade. Currently, the maintenance time can be customized for source, read-only, and disaster recovery instances.

Take the database instance specification upgrade as an example. As this operation involves data migration, after the upgrade is completed, a momentary disconnection from the database may occur. When the upgrade is initiated, you can select **During maintenance time** for **Switch Time**, so that the instance specification will be switched during the next **maintenance time** after the instance upgrade is completed. Note that when you select **During maintenance time** for **Switch Time**, the switch will not occur immediately after the database specification upgrade is completed; instead, the sync will continue till the instance goes into the next **maintenance time** when the switch will be performed. As a result, the overall time it takes to upgrade the instance may be extended.

>?
>- Before maintenance is carried out for TencentDB for MySQL, notifications will be sent to the contacts configured in your Tencent Cloud account by SMS and email.
>- TencentDB for MySQL will perform a data consistency check within the maintenance time configured for the database instance to ensure the source-replica data consistency and reduce the risk of data exceptions after the instance switch. The database performance will drop slightly during the check; therefore, we recommend that you select a maintenance time during off-peak hours. If the current load of the database is high, the check will be initiated during the maintenance time.
>- Instance switch will cause a momentary disconnection from the database. Make sure that your business has a reconnection mechanism.

## Directions
### Setting the maintenance time
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Maintenance Info** section on the instance details page, click **Modify**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ycyA534_5.png)
3. In the pop-up window, select **Maintenance Window** and **Maintenance Time** and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/gTPh665_6.png)

### [Performing the switch](id:lijiqiehuan)
If a task is configured to be switched during the maintenance time, but you need to switch it urgently under special circumstances, you can click **Switch Now** in the **Operation** column.

>?
>- Immediate switch is applicable to operations involving data migration such as instance specification adjustment, instance version upgrade, and instance kernel upgrade.
>- For version upgrade, if it is associated with multiple instances, the switch will be performed in the order from disaster recovery instance to read-only instance to source instance.
