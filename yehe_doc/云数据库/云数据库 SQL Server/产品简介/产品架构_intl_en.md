## Cluster Edition
### Supported versions
SQL Server 2017 Enterprise

### Architecture
TencentDB for SQL Server Cluster Edition adopts the Always On architecture, including one primary and one replica deployed across racks/AZs. Each of them corresponds to a monitoring agent that monitors the database through heartbeat in real time.
- Tencent Cloud management cluster: it consists of the independently deployed decision-making and scheduling cluster and configuration cluster as the management and scheduling center of clusters and is responsible for managing the normal operations of database node groups, access gateway clusters, and COS.
- COS: it provides data disaster recovery and cold backup services.
- Access gateway cluster: it provides a unique IP externally, so that even if data nodes are switched, the IP for users to connect to the instance stays unchanged.


>?Basic sync process of Always On:
>The logs (commits and log block writes) of the primary node will be flushed from the log cache to the disk. At the same time, the Log Capture thread of the primary node will also send the logs to all other replica nodes, and the Log Receive threads of the corresponding nodes will also flush the received logs from the log cache to the disk. Eventually, the Redo thread flushes these logs to the data file.
>
![](https://main.qcloudimg.com/raw/32fbdee7b03ed0b44aae3b539f0ca78f.png)


## Dual-Server High Availability Edition
### Supported versions
- SQL Server 2008/2012/2014/2016/2017 Enterprise
- SQL Server 2008/2012/2014/2016/2017 Standard

### Architecture
TencentDB for SQL Server Dual-Server High Availability Edition consists of one primary database and one mirror database deployed across racks/AZs. Each of them corresponds to a monitoring agent that monitors the database through heartbeat in real time.
- Tencent Cloud management cluster: it consists of the independently deployed decision-making and scheduling cluster and configuration cluster as the management and scheduling center of clusters and is responsible for managing the normal operations of database node groups, access gateway clusters, and COS.
- COS: it provides data disaster recovery and cold backup services.
- Access gateway cluster: it provides a unique IP externally, so that even if data nodes are switched, the IP for users to connect to the instance stays unchanged.
- The scaling of read-only instances is implemented through the publish/subscribe model.

>? A mirror has a complete copy of data but does not provide read/write services by itself; instead, it implements data sync by receiving update logs from the primary and allows the creation of snapshots for reporting. In a mirror cluster, data sync between the primary and mirror relies on transaction logs. SQL Server's transaction logs are at the database level rather than instance level, and each database has separate transaction logs, so SQL Server mirroring is implemented at the database level.

![](https://main.qcloudimg.com/raw/908fda85784c6d198536e44980715d5a.png)

## Basic Edition
### Supported versions
SQL Server 2008/2012/2014/2016/2017 Enterprise

### Architecture
The Basic Edition adopts a single-node deployment method and offers extremely high cost effectiveness. Its features are highlighted as below:
- It supports computation-storage separation. If a computing node fails, fast recovery can be achieved by switching to another node. Underlying data is stored in three copies on cloud disks, which ensures a certain level of data reliability and enables quick data restoration from disk snapshots in case of disk failures.
- It offers over 20 monitoring metrics such as database connection, access, and resource and supports configuring alarm policies as needed. Compared with a CVM-based self-built database, a Basic Edition instance is also deployed on a CVM instance but is more convenient and provides higher database performance at lower costs.
- It uses premium cloud disks as its underlying storage media, making it suitable for 90% I/O scenarios with low costs and stable performance.
>!
>- It is suitable for personal learning, ISV software for small and medium-sized enterprises (such as financial, CRM, and ERP customers), web applications, and non-core small corporate systems.
> - As it adopts a single-node architecture, when the node fails, it takes slightly longer to recover than CVM (due to instance startup and data restoration).
>- If your business requires high availability, we recommend you use the Dual-Server High Availability Edition or Cluster Edition.

![](https://main.qcloudimg.com/raw/e16d9a236cf2c6f9c6ce174486c1fcce.svg)

