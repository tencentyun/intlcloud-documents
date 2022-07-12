## Overview
Maintenance time is a very important concept for TencentDB for PostgreSQL. To ensure the stability of your TencentDB for PostgreSQL instance, the backend system performs maintenance operations on the instance during the maintenance time. We highly recommend you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.

In addition, we also recommend you perform operations involving data migration during the maintenance time, such as instance specification adjustment. Currently, the maintenance time is supported by primary and read-only instances.

Take the database instance specification upgrade as an example. As this operation involves data migration, after the upgrade is completed, a momentary disconnection from the database may occur. When the upgrade is initiated, the **Switch Time** can be set to **During maintenance time**, so that the instance specification will be switched during the next **maintenance time** after the instance upgrade is completed. Note that when you select **During maintenance time** for **Switch Time**, the switch will not occur immediately after the database specification upgrade is completed; instead, the sync will continue till the instance goes into the next **maintenance time** when the switch will be performed. As a result, the overall time it takes to upgrade the instance may be extended.

>?
>- Before maintenance is carried out for TencentDB for PostgreSQL, notifications will be sent to the contacts configured in your Tencent Cloud account through SMS and email.
>- Instance switch is accompanied by a disconnection from the database lasting for just seconds. Make sure that your business has a reconnection mechanism.

## Directions
### Setting maintenance time
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Maintenance Info** section on the instance details page, click **Modify**.
![](https://qcloudimg.tencent-cloud.cn/raw/dfa08513df80eea146d27c75c62691ad.png)
3. In the pop-up window, select **Maintenance Window** and **Maintenance Time** as needed and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/e0ecb7ff2390e4644b87a0e606e4540d.png)

### [Switching now](id:lijiqiehuan)
If a task is configured to be switched during the maintenance time, but you need to switch it urgently under special circumstances, you can click **Switch Now** in the **Operation** column.

>?Switching now is applicable to operations involving data migration such as instance specification upgrade.
