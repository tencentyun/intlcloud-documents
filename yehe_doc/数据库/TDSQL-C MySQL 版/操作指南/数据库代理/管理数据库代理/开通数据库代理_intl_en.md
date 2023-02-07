This document describes how to enable the database proxy in the TDSQL-C for MySQL console.

Database proxy is a network proxy service between the TencentDB service and the application service. It is used to proxy all requests when the application service accesses the database. It provides advanced features such as automatic read/write separation, connection pool, connection persistence, and consistency level configuration and boasts high availability, high performance, Ops support, and ease of use.

## Notes
- Database proxy currently is supported in the following regions:
  - Beijing (except Zones 1, 2, and 4), Shanghai (except Zone 1), Guangzhou (except Zones 1 and 2), Chengdu, Chongqing, Nanjing, and Hong Kong (China) (except Zone 1).
  - Tokyo (except Zone 1), Virginia (except Zone 1), Silicon Valley (except Zone 1), Seoul (except Zone 1), and Singapore (except Zones 1 and 2).
- Database proxy currently is supported on the following versions: MySQL 5.7 (with kernel minor version 2.0.19 or later) and MySQL 8.0 (with kernel minor version 3.1.5 or later). If you upgrade the kernel minor version of the cluster, the associated read-write and read-only instances will be upgraded at the same time. For more information, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/1098/44617).
- If the cluster is deployed across AZs, the database proxy feature cannot be enabled currently.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql). In the cluster list, click the ID or **Manage** in the **Operation** column of the target cluster to enter the cluster management page.
2. On the cluster management page, select the **Database Proxy** tab and click **Enable Now**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ee46370_9.png)
3. In the pop-up window, select the specification and node quantity and click **OK**.
    - Network: Only VPC is supported currently. The VPC of the read-write instance instance is selected by default.
    - Proxy Specification: 2-core 4000 MB memory, 4-core 8000 MB memory, or 8-core 16000 MB memory.
    - Node Quantity: Number of proxy nodes. We recommend you set the quantity to 1/8 (rounded up) of the total number of CPU cores on the read-write and read-only instances; for example, if the read-write instance instance has 4 CPU cores, and the read-only instance has 8 CPU cores, then the recommended node quantity will be (4 + 8) / 8 ≈ 2.
    - Connection Pool Status: For more information on connection pool, see [Connection Pool Overview](https://www.tencentcloud.com/document/product/1098/49988).
    - Security Group: It is an important means of network security isolation. You can choose an existing security group or create a new one as needed. 
4. After successfully enabling the service, you can manage proxy nodes and view their basic information on the database proxy page. You can also modify the database proxy address and network type and add remarks in the **Connection Address** section.
>?
>- You can view **Connections** in the proxy node list or view the performance monitoring data of each proxy node to check whether the numbers of connections on the nodes are unbalanced, and if so, you can distribute the connections by clicking **Rebalance**.
>- Rebalance will cause proxy nodes to restart, and the service will become unavailable momentarily during the restart. We recommend you restart the service during off-peak hours. Make sure that your business has a reconnection mechanism.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/M2Sw274_10.png)
