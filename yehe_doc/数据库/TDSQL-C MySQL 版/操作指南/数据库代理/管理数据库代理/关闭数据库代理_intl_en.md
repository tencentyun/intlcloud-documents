This document describes how to disable the database proxy in the TDSQL-C for MySQL console.
>!
>- After the database proxy is disabled, the database proxy address will be unavailable, but the read-write instance address is still available.
>- If you enable the database proxy again after disabling it, the database proxy access address will change.

## Prerequisite
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/1098/49999).

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql), and click the ID or **Manage** in the **Operation** column of the target cluster to enter the cluster management page.
2. On the cluster management page, select the **Database Proxy** tab and click **Disable Database Proxy** in the top-right corner.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WNgS491_4.png)
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.
