This document describes how to configure the session-level connection pool.

## Database Proxy Disabled
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target cluster to enter the cluster management page.
3. On the **Database Proxy** tab on the cluster management page, click **Enable Now**.
4. In the pop-up dialog box, enable the connection pool feature.

## Database Proxy Enabled
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target cluster to enter the cluster management page.
3. On the **Database Proxy** tab on the cluster management page, click **Enable** after **Connection Pool** at the bottom of the overview.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Gvci719_14.png)
2. In the pop-up dialog box, set the relevant configuration items and click **OK**.
   - **Connection Pool Status**: Enable connection pool.
   - **Connection Pool Type**: Session-level connection pool is supported.
   - **Connection Persistence Timeout**: The time threshold for idle connections to be retained in the connection pool of the proxy, which can be 1–300 seconds.
>!A flash disconnection will occur upon adjustment completion. Make sure that your business has a reconnection mechanism.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TkJJ658_15.png)
5. After the connection pool is successfully enabled, you can view the details and edit the configuration in **Overview** > **Basic Info** on the **Database Proxy** tab.

## Disabling Connection Pool
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target cluster to enter the cluster management page.
3. On the **Database Proxy** tab on the cluster management page, click **View/Edit** next to **Connection Pool** at the bottom of the overview.
4. In the pop-up dialog box, toggle off the **Connection Pool Status** option and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/b4AV784_16.png)
