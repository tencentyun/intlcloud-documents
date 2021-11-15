## Overview
Maintenance time is a very important concept for TencentDB for SQL Server. To ensure the stability of your TencentDB for SQL Server instance, the backend system performs maintenance operations on the instance during the maintenance window from time to time. We highly recommend you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.

In addition, we also recommend you perform operations involving data migration during the maintenance time, such as instance specification adjustment, instance version upgrade, and instance kernel upgrade. Currently, the maintenance period concept is supported by primary and read-only instances.

Take the database instance specification upgrade as an example. As this operation involves data migration, after the upgrade is completed, a momentary disconnection from the database may occur. When the upgrade is initiated, the **switch time** can be selected as **during maintenance window**, so that the instance specification switch will be enabled during the next **maintenance window** after the instance upgrade is completed. Please note that when you do so, the switch will not occur immediately after the database specification upgrade is completed; instead, the sync will continue till the instance goes into the next **maintenance window** when the switch will be performed. In this way, the overall time it takes to upgrade the instance may be extended.

>?
>- Before maintenance is carried out for TencentDB for SQL Server, notifications will be sent to the contacts configured in your Tencent Cloud account through SMS and email.
>- Instance switch is accompanied by a disconnection from the database lasting for just seconds. Please make sure that your business has a reconnection mechanism.

## Directions
### Setting maintenance time
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Maintenance Info** section on the instance details page, click **Modify**.
![](https://main.qcloudimg.com/raw/141ecd7d3a0ce63ac514aa6c8b4a530f.png)
3. In the pop-up window, select the **Maintenance Period** and **Maintenance Time** as needed and click **OK**.
![](https://main.qcloudimg.com/raw/d3cdb9e92661e4cdf11bec5861bfb53d.png)

### Immediate switch
If a task is configured to be switched during the maintenance window, but you need to switch it urgently under special circumstances, you can click **Switch Now** in the **Operation** column in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
>?Immediate switch is applicable to operations involving data migration such as instance specification adjustment, instance version upgrade, and instance kernel upgrade.
