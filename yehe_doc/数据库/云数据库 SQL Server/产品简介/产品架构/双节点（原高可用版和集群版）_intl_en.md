
TencentDB for SQL Server two-node instances support SQL Server 2008 R2, 2012, 2014, 2016, 2017, 2019 Enterprise and SQL Server 2012, 2014, 2016 Standard. The primary/replica architecture varies by version in the following two scenarios.

## Scenario 1
SQL Server 2008 R2, 2012, 2014, 2016 Enterprise or SQL Server 2012, 2014, 2016 Standard: The primary/replica architecture of a two-node instance consists of one primary database and one mirror database deployed across racks/AZs. Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time.
- Tencent Cloud management cluster: It consists of the independently deployed decision-making and scheduling cluster as well as configuration cluster. As the management and scheduling hub of clusters, it manages the normal operations of database node groups, access gateway clusters, and COS.
- COS: It provides data disaster recovery and cold backup services.
- Access gateway cluster: It provides a unique IP externally, so that even if data nodes are switched, the IP for users to connect to the instance stays unchanged.
- The scaling of read-only instances is implemented through the publish/subscribe model.

>? A mirror has a complete copy of data but does not provide read/write services by itself; instead, it implements data sync by receiving update logs from the principal and allows the creation of snapshots for reporting. In a mirror cluster, data sync between the principal and mirror relies on transaction logs. SQL Server's transaction logs are at the database level rather than instance level, and each database has separate transaction logs, so SQL Server mirroring is implemented at the database level.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/QhhY713_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16802432625707.png)

## Scenario 2
SQL Server 2017, 2019 Enterprise: The primary/replica architecture of a two-node instance adopts the Always On architecture, including one primary and one replica deployed across racks/AZs. Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time.
- Tencent Cloud management cluster: It consists of the independently deployed decision-making and scheduling cluster as well as configuration cluster. As the management and scheduling hub of clusters, it manages the normal operations of database node groups, access gateway clusters, and COS.
- COS: It provides data disaster recovery and cold backup services.
- Access gateway cluster: It provides a unique IP externally, so that even if data nodes are switched, the IP for users to connect to the instance stays unchanged.

>?Basic sync process of Always On:
>The logs (commits and log block writes) of the primary node will be flushed from the log cache to the disk. At the same time, the Log Capture thread of the primary node will also send the logs to all other replica nodes, and the Log Receive threads of the corresponding nodes will also flush the received logs from the log cache to the disk. Eventually, the Redo thread flushes these logs to the data file.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/pFDt463_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16802433238535.png)
