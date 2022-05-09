This document describes the TDSQL-C for MySQL use limits that you must follow to ensure the stable and secure operation of your cluster.

## Naming

| Limit | Description |
|---------|---------|
| Cluster name | It can contain up to 60 letters, digits, hyphens, underscores, and dots. |
| Read-write/Read-only instance name | It can contain up to 60 letters, digits, hyphens, underscores, and dots. |
| Account name | It can contain 1–16 letters, digits, and underscores and must start with a letter and end with a letter or digit. <br>It cannot be the same as an existing account name. |
| Database name | It can contain up to 64 lowercase letters, digits, hyphens, and underscores and must start with a letter and end with a letter or digit. <br>It cannot be the same as an existing database name and cannot be changed. |

## Quota Limits
| Quota | Limit |
|---------|---------|
| Read-only instance | A cluster can have 0–15 read-only instances. |
| Tag | Tag keys must be unique. There can be up to 20 tags. A tag can be bound to up to 50 instances at a time. |
| Free tier of backup space | TDSQL-C for MySQL backup space currently is free of charge. In the future, a free tier of backup space will be set according to the storage space selected during cluster purchase, and any excessive usage will incur fees. |
| Backup retention period | Backups can be retained for 7 (default) to 2,555 days. To modify the backup retention period, [submit a ticket](https://console.cloud.tencent.com/workorder/category). |
| Log retention period | Logs can be retained for 7 (default) to 2,555 days. To modify the log retention period, [submit a ticket](https://console.cloud.tencent.com/workorder/category). |
| Project | A project is defined on a cluster basis, and multiple instances in the same cluster belong to the same project. |


## Operation Limits
| Limit | Description |
|---------|---------|
| Kernel version upgrade | Cluster switch will be required after version upgrade is completed (that is, the database may be disconnected for seconds). We recommend you use applications configured with auto reconnection feature and conduct the switch during the instance maintenance window. <br>If the number of tables in a single instance exceeds one million, upgrade may fail and database monitoring may be affected. Make sure that the number of tables in a single instance is below one million. <br>The kernel minor version cannot be downgraded. |
| Failover | When the source node fails, TDSQL-C for MySQL will switch to a replica node. As a disconnection for less than 30 seconds will occur during the switch, make sure that your business has an automatic reconnection mechanism. |
| Network switch | Switching the network may cause all of the instance's private IPs to change. The system will automatically assign new IPs, so you need to modify the instance IPs on the client promptly. <br>The original IPs will expire after 24 hours by default. The expiration time can be customized during the network switch. If it is set to zero, the original IPs will be repossessed immediately after the network switch. <br>When switching the network, you can only select a new VPC and subnet in the same region and AZ where the instance resides. |
| Storage space | There is a limit on the storage space of each computing instance specification in the pay-as-you-go or serverless billing mode. For more information, see [Product Specifications](https://intl.cloud.tencent.com/document/product/1098/46430). <br>The storage space in the monthly subscription billing mode is as purchased. <br>The computing instance specification has a storage upper limit. If you need more storage space, upgrade the specification. |
| Data recovery | We recommend you back up important data to avoid data loss before restoring data through rollback or cluster cloning. |
| Configuration adjustment | TDSQL-C for MySQL supports fast in-place configuration upgrade or downgrade, and a momentary disconnection may occur in special circumstances. Make sure that your business has an automatic reconnection mechanism. We recommend you perform this operation during off-peak hours. |
