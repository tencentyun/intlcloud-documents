After creating a read-only instance, you can purchase the database proxy service and configure the connection address policy. Then, you can configure the database proxy address in your application so as to automatically forward write requests to the source instance and read requests to the read-only instance. This document describes how to enable read/write separation in the console.

## Prerequisites
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://intl.cloud.tencent.com/document/product/236/42052).

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select **Database Proxy** > **Overview**, find the target access address in **Connection Address**, and click **Adjust Configurations** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4e4x371_15.png)
3. In the pop-up window, set **Read-Write Attribute**, assign the read weight, and click **OK**.
>?The weight here pertains to the allocation strategy for read requests (non-transactional).
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4e4x371_15.png)
