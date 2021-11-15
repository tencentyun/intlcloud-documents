
## Overview
In scenarios where there are many read requests but only few write requests, a single instance may not be able to handle the load of read requests, which even may affect the business. To implement the auto scaling of read capabilities and mitigate the pressure on TencentDB for SQL Server, you can create one or multiple read-only instances and use them to sustain high numbers of database reads.

Unified read/write separation addresses (i.e., read and write requests are separated automatically) are not supported currently. Read-Only instances need to be accessed with separate IPs and ports.

#### Concepts
- Read-Only group: it consists of one or more load balancing-enabled read-only instances. If there are multiple read-only instances in one read-only group, read request volume can be evenly distributed among the instances. read-only groups provide IPs and ports for access to databases.
- Read-Only instance: a single-node (with no replica) instance that supports read requests. It cannot exist independently; instead, it must be in a read-only group.

#### Architecture
Changes in the primary instance (source database) are synced to all read-only instances. Given the single-node architecture (with no replica) of read-only instances, repeated attempts to restore a failing read-only instance will be made. Therefore, we recommend you choose a read-only group rather than a read-only instance for higher availability.

The read-only instance backend architecture and technology slightly vary by TencentDB for SQL Server editions:
- On editions below 2017 Enterprise, the publish/subscribe method is used to create read-only instances.
![](https://qcloudimg.tencent-cloud.cn/raw/8da3f1fd5e18cd5ab42f9c2d7731ebda.png)
>!In this mode, tables without a primary key in the primary instance cannot be synced. You can use the following code to query whether there is such a table:
```
use dbname
select name from sys.sysobjects where xtype='U' and id not in(select parent_obj from sys.sysobjects where xtype='PK')
```
If you need to create read-only instances for tables without a primary key, we recommend you use 2017 Enterprise Cluster Edition.
- On 2017 Enterprise Cluster Edition and above, the Always-On method is used to create read-only instances to ensure the efficiency and stability of data sync.
![](https://qcloudimg.tencent-cloud.cn/raw/c3cee7a40aad567b1bb56811f88d6785.png)


## Strengths
#### Read-Only group mode
You can connect to the VIP of a read-only group to read read-only instances in it, which can reduce the maintenance costs. You can also add the number of read-only instances in the unified read-only group to continuously expand the processing capacity of the system while ensuring the high availability of read-only instances, with no need to make any changes to the application.

#### Cross-AZ/region scaling
TencentDB for SQL Server supports adding read-only instances across AZs and regions, providing a low-latency, high-efficiency, and stable one-stop solution for nearby business access.

#### Automatic removal
The cluster management module automatically checks read-only instances. When it finds that a read-only instance is down or the delay exceeds the threshold, it stops allocating read requests to the instance and instead allocates them among the remaining healthy instances. This ensures that when a single read-only instance fails, the normal access to the application will not be affected. When the failed instance is repaired, it will be automatically added back to the request distribution system.


## Feature Limits
- Up to 3 read-only instances can be created for a primary instance.
- Currently, read-only instances are not supported for Standard Edition.
- Currently, read-only instances cannot be added to instances in finance zones.
- Read-Only instances do not support backup and rollback.
- Data cannot be migrated to read-only instances.
- Read-Only instances do not support database creation/deletion. If needed, please operate on a primary instance.
- Read-Only instances do not support account creation/deletion/authorization and account name/password change. If needed, please operate on a primary instance.
