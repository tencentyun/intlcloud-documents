This document describes how to enable or disable the connection pool feature.

## Prerequisites
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/236/42052).

## Enabling the connection pool feature
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select **Database Proxy** > **Access Policy**, find the target access policy, and click **Settings**.
>? You can also find the target access address in **Database Proxy** > **Overview** > **Connection Address**. Then, click **Adjust Configurations** in the **Operation** column.
>
3. In the pop-up window, toggle on **Connection Pool Status** and click **OK**. Then, the session-level connection pool will be enabled by default.
![](https://qcloudimg.tencent-cloud.cn/raw/ae2436546dfc7c8f0f8b6c6d6f154482.png)

## Disabling the connection pool feature
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select **Database Proxy** > **Access Policy**, find the target access policy, and click **Settings**.
>? You can also find the target access address in **Database Proxy** > **Overview** > **Connection Address**. Then, click **Adjust Configurations** in the **Operation** column.
>
3. In the pop-up window, toggle off **Connection Pool Status** and click **OK**.
