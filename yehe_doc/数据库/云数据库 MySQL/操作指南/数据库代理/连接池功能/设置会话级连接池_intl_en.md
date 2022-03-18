This document describes how to configure the session-level connection pool.

## Prerequisites
- [The database proxy version is at least 1.1.2.](https://intl.cloud.tencent.com/document/product/236/45627)
- The database version of the source instance is MySQL 5.7, and the database kernel minor version is at least 20211031. If this requirement is not satisfied, you need to [upgrade the database kernel minor version](https://intl.cloud.tencent.com/document/product/236/36816) first.

## Database Proxy Disabled
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target instance to enter the instance management page.
3. On the **Database Proxy** tab on the instance management page, click **Enable Now**.
4. In the pop-up dialog box, enable the connection pool feature.
![](https://qcloudimg.tencent-cloud.cn/raw/ae2436546dfc7c8f0f8b6c6d6f154482.png)

## Database Proxy Enabled
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target instance to enter the instance management page.
3. On the **Database Proxy** tab on the instance management page, click **Enable** after **Connection Pool** at the bottom of the overview.
![](https://qcloudimg.tencent-cloud.cn/raw/9524cadfc5fe0d67a8a050f44ea5fada.png)
4. In the pop-up window, set the relevant configuration items and click **OK**.
   - **Connection Pool Status**: Enable connection pool.
   - **Connection Pool Type**: Session-level connection pool is supported.
   - **Connection Persistence Timeout**: The time threshold for idle connections to be retained in the connection pool of the proxy, which can be 1–300 seconds.
>!A flash disconnection will occur upon adjustment completion. Make sure that your business has a reconnection mechanism.
>
![](https://qcloudimg.tencent-cloud.cn/raw/f354aa701758d2823c67468392e37617.png)
5. After the connection pool is successfully enabled, you can view the details and edit the configuration in **Overview** > **Basic Info** on the **Database Proxy** tab.

## Disabling Connection Pool
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target instance to enter the instance management page.
3. On the **Database Proxy** tab on the instance management page, click **View/Edit** after **Connection Pool** under the overview.
4. In the pop-up window, set the relevant configuration items and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/6367f83dd1aaacc0dae91e9ec1085955.png)

