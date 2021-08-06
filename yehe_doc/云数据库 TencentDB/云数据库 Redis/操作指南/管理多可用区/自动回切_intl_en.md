TencentDB for Redis provides the auto-failback feature for instances deployed across AZs. After the feature is enabled, if the master node is switched from the master AZ or master node group (cluster architecture) to another AZ or group after a failover occurs, it will be automatically switched back, simplifying subsequent OPS operations. You can enable or disable this feature by setting a database parameter.

## Master AZ

You can deploy nodes of a TencentDB for Redis instance in master and replica AZs. The auto-failback is enabled by default. If the master node is switched from the master AZ or master node group (cluster architecture) to another AZ or group after a failover occurs, it will be automatically switched back after all of the failed nodes are replaced.

You can specify the master AZ when creating an instance. Or, you can manually promote a replica AZ to master after the instance is created (after a replica node/node group is promoted to master, its AZ will become the master AZ).

## Enabling/Disabling Auto-Failback

You can manage the auto-failback feature with a database parameter. The feature is enabled by default. Enabling/disabling it does not affect your access to Redis.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the **Parameter Settings** page, set `auto-failback` to `yes` or `no` to enable or disable the auto-failback feature.
   ![](https://main.qcloudimg.com/raw/254792ffab482fd3c092ea63b001a7c1.png)

