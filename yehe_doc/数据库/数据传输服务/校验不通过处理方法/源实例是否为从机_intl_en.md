## Check details
The source database must be a replica node; otherwise, an alarm will be triggered. The alarm will not stop the task and can be ignored, but you should assess the impact of ignoring it.

During migration, DTS will perform a `BGSAVE` operation on the source database, which will use its memory and resources. If the source database is a master node, business writes will be greatly affected.

- If the source database is a TencentDB for Redis database, a replica node will be used for migration by default.
- If the source database is a local self-built Redis database, the master node may be used for migration. If an alarm is triggered during the check, we recommend you change the source database to a replica node. 


## Troubleshooting
Reconfigure the migration task by changing the parameters of the source database to the information of a replica node.

