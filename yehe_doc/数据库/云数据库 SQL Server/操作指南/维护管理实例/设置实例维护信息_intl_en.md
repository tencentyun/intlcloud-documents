## Scenario
Maintenance period is a very important concept for TencentDB for SQL Server. To ensure the stability of your TencentDB for SQL Server instance, the backend system performs maintenance operations on the instance during the maintenance period from time to time. To minimize the potential impact on your business, we recommend that you set an acceptable maintenance period for your business instance, usually during off-peak hours.

In addition, we recommend that you perform operations involving data migration during the maintenance time, such as instance specification adjustment, instance version upgrade, and instance kernel upgrade. Currently, the maintenance period is supported by primary and read-only instances.

Take the database instance specification upgrade as an example. As this operation involves data migration, after the upgrade is completed, a momentary disconnection from the database may occur. When the upgrade is initiated, the **Switch Time** can be set to **During maintenance time**, so that the instance specification will be switched during the next **maintenance time** after the instance upgrade is completed. Note that when you select **During maintenance time** for **Switch Time**, the switch will not occur immediately after the database specification upgrade is completed; instead, the sync will continue till the instance goes into the next **maintenance time** when the switch will be performed. As a result, the overall time it takes to upgrade the instance may be extended.

>?
>- Before maintenance is carried out for TencentDB for SQL Server, notifications will be sent to the contacts configured in your Tencent Cloud account by SMS and email.
>- Instance switch is accompanied by a disconnection from the database lasting for just seconds. Make sure that your business has a reconnection mechanism.

## Directions
### Setting the maintenance window
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance details page.
2. In the **Maintenance Info** section on the instance details page, click **Modify**.
![](https://main.qcloudimg.com/raw/141ecd7d3a0ce63ac514aa6c8b4a530f.png)
3. In the pop-up window, select **Maintenance Window** and **Maintenance Time** as needed and click **OK**.
![](https://main.qcloudimg.com/raw/d3cdb9e92661e4cdf11bec5861bfb53d.png)
>!Select at least one maintenance window; otherwise, the change cannot be submitted.

### Performing immediate switch
If a task is configured to be switched during the maintenance window, but you need to switch it urgently under special circumstances, you can click **Switch Now** in the **Operation** column in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
>?Immediate switch is applicable to operations involving data migration such as instance specification adjustment, instance version upgrade, instance kernel upgrade, and cross-AZ migration.
>
