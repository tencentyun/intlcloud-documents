As the minimum management unit in TencentDB for SQL Server, a database instance is a database environment running independently in Tencent Cloud and represents an independent TencentDB for SQL Serve instance. You can create, modify, and delete instances in the console and create and manage multiple databases in each instance.

This document describes TencentDB for SQL Server database instance types.

## Instance types and descriptions

<table>
<thead><tr><th width=19%>Instance Type</th><th>Overview</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Standalone instance - single-node (formerly Basic Edition) instance</td>
<td><li>A single database node architecture is adopted, which is very cost-effective.</li><li>Computing and storage are separated, and the underlying data is stored in three replicas in cloud disks.</li><li>A Basic Edition node is deployed in a CVM instance, which has a higher database performance than self-built databases.</li><li>Premium cloud disk is used as the underlying storage media, suitable for 90% I/O scenarios with a stable performance.</li></td>
<td>This instance type is suitable for personal learning, ISV software for small and medium-sized enterprises, web applications, and non-core small corporate systems. If a standalone instance fails, it takes a slightly longer time to recover than a CVM instance.</td></tr>
<tr>
<td rowspan="2">Primary/Replica instances - two-node (formerly High Availability/Cluster Edition) instances</td>
<td>SQL Server 2008 R2/2012/2014/2016 Enterprise or SQL Server 2012/2014/2016 Standard: It consists of one primary database and one mirror database. <li>The classic one-primary-one-replica architecture is adopted, and all primary/replica instance nodes have the same specification.</li><li>The primary and replica instances are deployed across racks/AZs. Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time.</li><li>Cross-AZ high availability is supported; that is, the primary and replica instances can be deployed in different AZs.</li><li>COS provides the data disaster recovery and cold data backup services.</li><li>Independently deployed decision-making and scheduling cluster and configuration cluster serve as the management and scheduling center of database clusters. They are responsible for managing the normal operations of database node groups, access gateway clusters, and COS.</li></td><td><li>Replica instances improve the instance reliability. When a primary instance is created, a replica instance will be created at the same time, which will be invisible to users.</li><li>When the primary instance fails, primary-replica switch will be automatically triggered, and the database client will be disconnected momentarily. Therefore, the database client needs to support reconnection.</li><li>The TencentDB for SQL Server primary and replica instances are async by default, so are the primary and read-only instances.</li></td></tr>
<tr><td>SQL Server 2017/2019 Enterprise: The Always On architecture is adopted, where you can add up to five read-only instances to create a cluster with higher availability, reliability, and scalability. The primary and replica instances are deployed across racks/AZs. Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time.</td><td>This instance type is suitable for industry application scenarios, such as gaming, healthcare, medicine, internet, IoT, retail, ecommerce, logistics, insurance, securities, media, technical service, and automobile.</td></tr>
<tr>
<td>Read-only instance</td>
<td><li>It is a single-node (with no replica) instance that supports read requests.</li><li>It cannot exist independently; instead, it must be in a read-only group and bound to a two-node primary instance.</li><li>A read-only group is a read-only instance group with the load balancing feature.</li></td>
<td><li>A read-only instance is standalone. When the physical server fails or a database replication exception occurs, it will take a long time (subject to the data volume) for the instance to recover.</li><li>For business scenarios with a strong dependency on read-only requests, we recommend that you create multiple read-only instances to share the read pressure.</li></td></tr>
</tbody></table>

>? You can create and manage instances of various types in the [TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver) console.

## References
- [Features and Differences](https://intl.cloud.tencent.com/document/product/238/46495)
