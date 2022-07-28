CDWPG adopts the shared-nothing (SN) massively parallel processing (MPP) architecture as shown below, where the master and standby master nodes are deployed on two servers.
![](https://main.qcloudimg.com/raw/04b9a1451cab04df95f43a7734c2bc6e.png)

- **Master Node:** A master node stores only data dictionaries but not business data. It is responsible for generating and distributing SQL execution plans to each segment node, interacting with clients, and verifying permissions.
- **Segment Node:** A segment node stores business data and executes SQL statements distributed by the master node. To ensure that each segment service is at the same performance level, each segment node server has the same resource configuration, and no model change will be made during scaling.

To ensure a high cluster availability, each segment node houses a primary segment of the current node and a mirror segment of another node that works as a standby node. When a segment node becomes unavailable, its mirror node will take over. When the master node becomes unavailable, the standby master node will take over to ensure the cluster availability. Changes will be automatically synced when the master node is restarted.

All the business data of the cluster is stored in the databases of all segment nodes, and each data table is sharded into each segment node. During analysis, all segment nodes work simultaneously to compute their part of data, greatly improving the efficiency.

CDWPG supports data backup and restoration. After data backup is enabled, each segment node will create a dump file containing data rebuild commands, and the master node will create several dumps files containing system targets, metadata files, DDL statements, and other information. During data restoration, all segments restore data from local backup files at the same time.

