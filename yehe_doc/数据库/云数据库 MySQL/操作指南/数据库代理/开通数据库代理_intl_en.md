
This document describes how to enable database proxy in the TencentDB for MySQL console.

[Database proxy](https://intl.cloud.tencent.com/document/product/236/42048) is a network proxy service between the TencentDB service and the application service. It is used to proxy all requests when the application service accesses the database. It provides advanced features such as automatic read/write separation, connection pool, and connection persistence and boasts high availability, high performance, OPS support, and ease of use.


## Notes
- Database proxy currently is supported in the following regions:
  - Beijing (except Zones 1, 2, and 4), Shanghai (except Zone 1), Guangzhou (except Zones 1 and 2), Chengdu (except Zone 1), Chongqing, Nanjing, and Hong Kong (China) (except Zone 1).
  - Tokyo (except Zone 1), Bangkok (except Zone 1), Virginia (except Zone 1), Silicon Valley (except Zone 1), Mumbai (except Zone 1), and Seoul (except Zone 1).
- Database proxy currently is supported on the following versions: two-node and three-node MySQL v5.7 (the kernel minor version should be 20201230 or above). If you upgrade the kernel minor version of the source instance, the associated read-only and disaster recovery instances will be upgraded at the same time. For more information, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/236/36816).

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, select the source instance for which to enable database proxy and click its ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab and click **Enable Now**.
![](https://main.qcloudimg.com/raw/46d9e9b30975b51bee00a16c64f31c8b.png)
3. In the pop-up window, select the specification and node quantity and click **OK**.
 - Network: currently, only VPC is supported. The VPC of the source instance is selected by default.
 - Proxy Specification: currently, only one specification is supported.
 - Node Quantity: number of proxy nodes. We recommend you set the quantity to 1/8 (rounded up) of the total number of CPU cores on the source and read-only instances; for example, if the source instance has 4 CPU cores, and the read-only instance has 8 CPU cores, then the recommended node quantity will be (4 + 8) / 8 ≈ 2.
![](https://main.qcloudimg.com/raw/a3d8fafb1930d0298deb9cf2f08e706c.png)
4. After successfully enabling the service, you can manage proxy nodes and view their basic information on the database proxy page.
>?
>- You can view **Connections** in the proxy node list or view the performance monitoring data of each proxy node to check whether the numbers of connections on the nodes are unbalanced, and if so, you can distribute the connections by clicking **Rebalance**.
>- Rebalance will cause proxy nodes to restart, and the service will become unavailable momentarily during the restart. We recommend you restart the service during off-peak hours. Make sure that your business has a reconnection mechanism.
>
![](https://main.qcloudimg.com/raw/083d38858367fd7fe65e90fb92210178.png)

