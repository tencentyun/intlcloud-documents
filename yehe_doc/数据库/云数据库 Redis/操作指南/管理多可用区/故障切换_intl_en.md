
## Automatic Failover
TencentDB for Redis supports the automatic failover of proxy nodes and Redis servers (data storage nodes) to ensure service availability.

### Proxy failover
Proxy nodes are used in both standard and cluster architectures of TencentDB for Redis. The standard architecture has three proxy nodes, while the number of proxy nodes in the cluster architecture increases linearly with that of shards. The high availability design of proxy nodes is as follows:
- Multiple proxy nodes support the high availability and load balancing of the proxy service.
- Proxy nodes are deployed on three physical devices to ensure high availability.
- If a proxy node fails, the testing system will detect the failed node and automatically add new one.

### Redis server failover
TencentDB for Redis in the standard or cluster architecture uses the native cluster management mechanism of Redis Cluster: the Gossip protocol is used to figure out the status of cluster nodes, and the `cluster-node-timeout` parameter defines the maximum amount of time a node can be unavailable, without it being considered as failing. The default value of the parameter is 15000 ms, which should not be modified.
For more information about how to identify a failed node, please see [Redis cluster tutorial](https://redis.io/topics/cluster-tutorial).

## Failure Simulation
You can use the failure simulation feature in the TencentDB for Redis console to perform failure simulations or tests.
How it works: the `shutdown` commands are sent to all master nodes to trigger the automatic high availability (HA) logic. Only instances in the "Running" status can perform failure simulations.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the **Node Management** tab, select **More** > **Failure Simulation** or **Configuration Modification** > **Failure Simulation**.

![](https://main.qcloudimg.com/raw/4b6b66dae7776d37ffb474482d2279f7.png)

3. In the pop-up dialog box, enter the instance password and click **OK**.
>!
>- A failure simulation will make Redis unavailable for less than one minute until the failover is completed. The data written during the simulation may be lost.
>- The instance service downtime caused by failure simulations won't be counted into the "Single Instance Service Downtime" in Redis Service Level Agreement (SLA).
>
![](https://main.qcloudimg.com/raw/3748b50a21dfe36859dbbfc41d18da63.png)

