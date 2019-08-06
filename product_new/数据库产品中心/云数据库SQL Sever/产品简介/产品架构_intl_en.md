## Backend Architecture
The architecture is as follows:
![](https://main.qcloudimg.com/raw/ece530a79e57cf0c0fd2d725772ceb1a.png)
TencentDB for SQL Server consists of a master database and a mirror database that are deployed in different racks. Each database corresponds to a group of monitoring agents which monitor the database in real time based on the heartbeat. The cluster management scheduling center consists of two sets of independently deployed decision-making clusters and configuration clusters and is mainly used to manage the normal operations of the database node group, access gateway cluster and HDFS. The Hadoop distributed file system (HDFS) makes available data disaster recovery service with cold backup. The gateway cluster is accessed to provide a unique IP, and if the data node is switched, the IP won't change.

## Database Mirroring
Currently, TencentDB for SQL Server is supported by the database mirroring (high-availability replication) scheme by default.
![](https://main.qcloudimg.com/raw/c93d18bdf946afbaefb2f9d345186913.jpg)
This enables automatic switching in seconds, lowering the data loss to "zero".

## Automatic Node Recovery
TencentDB for SQL Server supports automatic rebuilding of database nodes, so if a node fails, it will be automatically restored/reconstructed. The node switchover is imperceptible to the business, and the database access IP does not change.
![](https://main.qcloudimg.com/raw/cd4b73ec5c53454a3248ac413078ef3f.png)


