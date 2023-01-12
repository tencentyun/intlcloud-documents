The TencentDB for MySQL database proxy provides the transaction split feature. This feature separates read and write operations in one transaction to different instances for execution and forwards read requests to read-only instances, thereby lowering the load of the source instance.

## Background
By default, the TencentDB for MySQL database proxy forwards all requests in a transaction to the source instance to ensure the transaction correctness. In some frameworks, however, all requests are encapsulated to transactions that are not committed automatically, causing an excessive load of the source instance. In this case, you can use the transaction split feature.
The transaction split feature is disabled by default. You can enable it by adjusting the configuration of the database proxy address.

## Prerequisites
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/236/42052).

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select **Database Proxy** > **Access Policy**, find the target access policy, and click **Settings**.
>? You can also find the target access address in **Database Proxy** > **Overview** > **Connection Address**. Then, click **Adjust Configurations** in the **Operation** column.
3. In the pop-up window, toggle on **Transaction Split** and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NvFN030_1.png)
