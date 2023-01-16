
After the database proxy is enabled, you can view **Connections** in the proxy node list or the performance monitoring data of each proxy node to check whether the numbers of connections on the nodes are unbalanced. If there is a large number of persistent connections, increasing the number of the database proxy nodes may also cause load imbalance among them, and if so, you can distribute the connections by clicking **Rebalance**. This document describes how to manually rebalance the node in the console.

## Prerequisites
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/236/42052).

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). Select the region at the top of the page and click the target instance ID to enter the instance management page.
2. On the instance management page, select **Database Proxy** > **Overview**, find the target access address in **Connection Address**, and click **Rebalance** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/FjIc990_21.png)
3. In the pop-up window, click **OK**.
>? Rebalancing will cause the disconnection of the session to the address, during which the service will be unavailable momentarily. We recommend that you restart the service during off-peak hours. Make sure that your business has a reconnection mechanism.
