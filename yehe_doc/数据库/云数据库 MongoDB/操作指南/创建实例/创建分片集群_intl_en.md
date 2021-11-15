
## Creation of Sharded Cluster Instance
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb/sharding), select **Sharded Cluster Instance** on the left sidebar, and click **Create Instance** to enter the [purchase page](https://buy.cloud.tencent.com/mongodb?clusterType=1).
2. Select **Sharded Cluster** as the instance type and select the number of shards, number of nodes in a shard, and node specification as needed. Each shard is a multi-node replica set, and the multiple nodes in each shard implement automatic disaster recovery to ensure high service availability.
3. After confirming that everything is correct, click **Buy Now**.

## Sharded Cluster Console
Click an instance ID in the instance list to enter the details page where you can view the details of the sharded cluster instance, such as shard composition, shard node specification, and used capacity. You can also expand instance capacity in the console.
![](https://main.qcloudimg.com/raw/ff86a7a08d4990d542b64749440e4896.png)

## Sharded Cluster Expansion
You can only expand the capacity of a TencentDB for MongoDB sharded cluster by expanding all nodes. Capacity expansion based on node scale-out is not supported currently.
Click **Adjust Configuration** on the instance list page, select the target capacity specification, and click **Submit**.
![](https://main.qcloudimg.com/raw/dffa3325bae3f76d4ae889d2c07b8a51.png)

## Backup and Rollback
Backup and rollback operations in sharded cluster instances are the same with those in replica set instances. Currently, you can only back up and roll back data at the instance level.
Click an instance ID in the instance list to enter the management page and select **Backup and Rollback**.
![](https://main.qcloudimg.com/raw/b211048c4e8d23bd0f0ebea8c0c6d5f7.png)
You need to enter a date to which you want to roll the instance back. You can enter any time point within the last 6 days, but you can only select a time between two backups (backup succeeds and oplog is not fully occupied). If there are no backups to satisfy this condition, please perform manual backup.
![](https://main.qcloudimg.com/raw/99545980a00cb7c8a4bc34351bb6efbf.png)

## Cluster Instance Monitoring
Monitoring metrics in three dimensions are provided to monitor data in an entire TencentDB for MongoDB sharded cluster: instance, shard, and node. Monitoring data of multiple metrics is provided, such as operation requests, capacity usage, and load.
Click an instance ID in the instance list to enter the management page and select **System Monitoring** for query.
![](https://main.qcloudimg.com/raw/7f1957c3dbdf9b71959cf5494718b949.png)

