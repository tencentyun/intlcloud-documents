## 1. Backend Architecture
The structure chart is as follows:
![](//mccdn.qcloud.com/static/img/514a1ae9a57038309bb75ac09fb606b7/image.png)
TencentDB for SQL Server consists of a master database and a mirror database that are deployed in different racks. Each database corresponds to a group of monitoring agents which monitor the database in real time based on the heartbeat. The cluster management scheduling center consists of two sets of independently deployed decision-making clusters and configuration clusters and is mainly used to manage the normal operations of the database node group, access gateway cluster and HDFS. The Hadoop distributed file system (HDFS) makes available data disaster recovery service with cold backup. The gateway cluster is accessed to provide a unique IP, and if the data node is switched, the IP won't change.

## 2. Database Mirroring
Currently, TencentDB for SQL Server is supported by the database mirroring (high-availability replication) scheme by default.
![](//mccdn.qcloud.com/static/img/b271b907acf9f9e40a65d289c51d1ad1/image.png)
This enables automatic switching in seconds, lowering the data loss to "zero".

## 3. Automatic Node Recovery
TencentDB for SQL Server supports automatic rebuilding of database nodes, so if a node fails, the failed node will be automatically restored/reconstructed within one hour. The node switch is imperceptible to the business, and the database access IP does not change.
![](//mccdn.qcloud.com/static/img/a30d1011f9dc8646fd3a8eeae8c4cfb0/image.png)


