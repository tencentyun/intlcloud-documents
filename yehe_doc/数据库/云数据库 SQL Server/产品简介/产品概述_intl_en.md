TencentDB for SQL Server is licensed by Microsoft to continuously provide you with the latest features, so you can avoid any risks arising from unauthorized software use. It features out-of-the-box usage, high stability, reliability, and security, elastic scaling, data security protection, and failover in seconds, allowing you to focus on application development.

>? As one of the earliest commercial database products, SQL Server supports complex SQL queries with excellent performance. Thanks to its comprehensive support for applications based on the Windows .NET Framework, it is widely used in such fields as government services, finance, healthcare, retail, education, and gaming.

## Deployment Architecture
TencentDB for SQL Server supports two deployment architectures:

#### Single-node (formerly Basic Edition)
It is deployed on a single node and based on premium cloud disks, with computing and storage separated.

#### Two-node (formerly High Availability/Cluster Edition)
- SQL Server 2008 R2, 2012, 2014, 2016 Enterprise/Standard: The primary/replica architecture of a two-node instance consists of one primary database and one mirror database deployed across racks/AZs.
- SQL Server 2017, 2019 Enterprise/Standard: The primary/replica architecture of a two-node instance adopts the Always On architecture, including one primary and one replica deployed across racks/AZs by default.

## Isolation Policy
- TencentDB for SQL Server single-node (cloud disk) and two-node (cloud disk) instances are deployed based on CVM, where each instance has dedicated CPU, memory, and disk resources in one CVM instance and different instances are completely isolated from each other.
- TencentDB for SQL Server two-node (local disk) instances are deployed based on local physical machines. Each physical machine sustains multiple instances and adopts isolation policies to ensure the complete isolation between different instances with dedicated CPU, memory, and disk resources.
In addition, TencentDB for SQL Server also implements corresponding data isolation policies in multiple dimensions such as account, region, AZ, and network.
