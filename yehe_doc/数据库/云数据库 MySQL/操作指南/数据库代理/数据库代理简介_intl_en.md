
This document describes the features and use cases of the database proxy service in TencentDB for MySQL.

Database proxy is a network proxy service between the TencentDB service and the application service. It is used to proxy all requests when the application service accesses the database.
The database proxy access address is independent of the original database access address. Requests arriving at the proxy address are all relayed through the proxy cluster to access the source and replica nodes of the database. Read/Write separation is implemented, so that read requests are forwarded to read-only instances, which lowers the load of the source database.
>?Currently, the database proxy service is in beta test, and you can use it free of charge.
>
## Features
- **High stability**
Database proxy adopts the cluster architecture for deployment, with multiple nodes ensuring smooth failover.
- **Strong isolation**
Database proxy uses independent resources to provide proxy service for the current instance (the resources of different proxies are isolated and not shared).
- **Ultra-High performance**
Each proxy can process up to 100,000 requests per second.
- **Convenient and fast scaling**
You can dynamically add 1–60 proxy nodes (only 6 nodes are supported during the beta test).
- **Complete performance monitoring**
Performance metrics are monitored at the second level, such as the number of read/write requests, CPU, and memory. The number of proxies can be adjusted according to the [monitoring data](https://intl.cloud.tencent.com/document/product/236/41090) and business planning.
- **Hot load**
If the source instance is switched, has configuration adjustment, or has read-only instances added or removed, the database proxy can dynamically hot load the configuration without causing network disconnections or restarts.
- **Support for [automatic read/write separation](https://intl.cloud.tencent.com/document/product/236/41089)**
Enabling the read/write separation feature of the database proxy can effectively reduce the read load of the source instance. Read-Only instances can be added to horizontally scale the database cluster and automatically implement read/write separation, which eliminates the complexity of manually separating read and write requests of the business. This is especially suitable for scenarios with a high read load.
For example, after the read/write separation feature of the database proxy is enabled, only one proxy connection address needs to be configured in the application. This address will automatically implement read/write separation and send read requests to read-only instances and write request to the source instance. Even if you add or remove read-only instances, you don't need to adjust the application settings.

## Use Cases
- Businesses with a large number of non-persistent connection have insufficient performance.
- Businesses use multiple read-only instances, and read/write separation is implemented manually on applications, resulting in higher maintenance costs and risks.
- Too many connections cause the instance loads to be too high.

