This document describes the new version of the TencentDB for MySQL database proxy.

Database proxy is a network proxy service between the TencentDB service and the application service. It is used to proxy all requests when the application service accesses the database.
The database proxy access address is independent of the original database access address. Requests arriving at the proxy address are all relayed through the proxy cluster to access the source and replica nodes of the database. Read/Write requests are separated, so that read requests are forwarded to read-only instances, which lowers the load of the source database. This implements high availability, high performance, and Ops support.
TencentDB for MySQL database proxy also provides advanced features such as automatic read/write separation, transaction split, connection pool, cross-AZ read-only instance mounting, and enabling multiple proxy addresses.

## Billing
Currently, database proxy is in beta test free of charge.

## Use cases
- Businesses with low performance when there is a large number of non-persistent connections.
- Businesses that use multiple read-only instances with read/write separation is implemented manually on applications, resulting in higher maintenance costs and risks.
- High instance loading caused by too many connections.
- High source instance load due to a large number of requests in the transaction.
- Businesses that need to be assigned different loads through the access address.
- Nearby access in cross-AZ deployment for reduced latency.

## Read-write attribute
Each database proxy address can have its own read-write attribute.
- **Read/Write**: Supports read/write separation to implement linear business scaling.
This attribute contains at least one source instance and one read-only instance, and write requests are sent to the source instance only. It supports read/write separation features such as transaction split and connection pool as well as policies such as **Remove Delayed RO Instances**, **Least RO Instances**, and **Failover**.
- **Read-Only**: Supports read-only businesses like reports.
This attribute contains at least one read-only instance, and the source instance is not involved in routing. It supports features such as transaction split and connection pool as well as policies such as **Remove Delayed RO Instances** and **Least RO Instances**.

## Features
- **High stability**
The database proxy is deployed in the cluster architecture, with multiple nodes ensuring smooth failover.
- **High availability**
The database proxy adopts cross-AZ deployment to improve its availability.
- **Strong isolation**
The database proxy provides the proxy service for the current instance with independent resources. The resources of each proxy are isolated and not shared.
- **Ultra-high performance**
Each proxy can process up to 100,000 requests per second.
- **Convenient and fast scaling**
You can dynamically add 1–60 proxy nodes, with only 6 nodes supported during the beta test.
- **Comprehensive performance monitoring**
Performance metrics are monitored at the second level, such as the number of read/write requests, CPU, and memory. The number of proxies can be adjusted according to the monitoring data as described in [Viewing Database Proxy Monitoring Data](https://www.tencentcloud.com/document/product/236/42055) and business planning.
- **Hot reload**
If the source instance is switched, has configuration adjustment, or has read-only instances added or removed, the database proxy can dynamically hot load the configuration without causing network disconnections or restarts.
- **Automatic read/write separation**
Enabling the read/write attribute of the database proxy address can effectively reduce the read load of the source instance. Read-only instances can be added to horizontally scale the database cluster and automatically implement read/write separation, which eliminates the complexity of manually separating read and write requests of the business. This is especially suitable for scenarios with a high read load.
For example, only one proxy connection address needs to be configured in the application (when **Read-Write Attribute** is set to **Read/Write Separation**), and this address will automatically implement read/write separation and send read requests to read-only instances and write requests to the source instance. Even if you add or remove read-only instances, you don't need to adjust the application settings.
- **Connection pool**
This feature can mitigate excessively high instance loads caused by too many connections or frequent new connections in non-persistent connection businesses.
- **Transaction split**
This feature separates reads and writes in one transaction to different instances for execution and forwards read requests to read-only instances to reduce the load of the source instance.

## Feature page
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QNE2634_8.png)

