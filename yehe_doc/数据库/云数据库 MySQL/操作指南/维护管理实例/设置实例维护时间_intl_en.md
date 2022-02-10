## Overview
Maintenance window is a very important concept for TencentDB for MySQL. To ensure the stability of your TencentDB for MySQL instance, the backend system performs maintenance operations on the instance during the maintenance window from time to time. It is highly recommended that you set an acceptable maintenance window for your instance, usually during off-peak hours, so as to minimize the potential impact on your business.

In addition, it is recommended that operations involving data migration be performed during the maintenance window too, such as instance specification adjustment, instance version upgrade, and instance kernel upgrade. Currently, the maintenance window is supported by source instances, read-only replicas, and disaster recovery instances.

Taking the database instance specification upgrade as an example, as this operation involves data migration, after the upgrade is completed, a momentary disconnection from the database may occur. When the upgrade is initiated, the **Switch Time** can be selected as **During maintenance window**, so that the instance specification switch will be enabled within the next **maintenance window** after the instance upgrade is completed. Please note that when you do so, the switch will not occur immediately after the database specification upgrade is completed; instead, the sync will continue till the instance goes into the next **maintenance window** when the switch will be performed. In this way, the overall time it takes to upgrade the instance may be extended.

>?
>- Before maintenance is carried out for TencentDB for MySQL, notifications will be sent to the contacts configured in your Tencent Cloud account via SMS and email.
>- Instance switch is accompanied by a disconnection from the database lasting for just seconds. Please make sure that your business has a reconnection mechanism.

## Directions
### Setting maintenance window
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Maintenance Info** section, click **Modify**.
![](https://main.qcloudimg.com/raw/388e3aa6ca18c6cb947eb4d053ad1eb5.png)
3. In the pop-up dialog box, select **Maintenance Schedule** and **Maintenance Time**, and click **OK**.
![](https://main.qcloudimg.com/raw/001fee80a9e1e7f5f55c2de15802a613.png)

<span id="lijiqiehuan"></span>
### Performing immediate switch
If a task is configured to be switched during the maintenance window, but you need to switch it urgently under special circumstances, you can click **Switch Now** in the **Operation** column.
![](https://main.qcloudimg.com/raw/fd9780d4f9e1d8094bcb82f215deb366.png)

>?
>- Immediate switch is applicable to operations involving data migration such as instance specification adjustment, instance version upgrade, and instance kernel upgrade.
>- For version upgrade, if it is associated with multiple instances, the switch will be performed in the order from read-only replica to source instance.
