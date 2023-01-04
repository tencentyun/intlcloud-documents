TDSQL-C for MySQL allows you to modify the maximum connections of each account to the database in the console. By doing so, you can prevent a single account from using up all connections.

This document describes how to modify the account connections in the console.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region, find the target cluster in the cluster list, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. Click **Account Management**, find the target account in the list, select **More** > **Modify Maximum Connections** in the **operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/kdPL311_9.png)
4. In the pop-up window to modify connections, enter a value in **New Maximum Connections**, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/zsBZ495_10.png)
>?Valid range of connections: 1-10240. If you don't enter a value, the maximum number of connections will be 10240.
