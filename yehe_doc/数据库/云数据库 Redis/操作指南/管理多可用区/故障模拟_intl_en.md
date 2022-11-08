## Overview

TencentDB for Redis supports the automatic failover of proxy nodes and Redis servers (data storage nodes) to ensure service availability.

You can use the failure simulation feature in the TencentDB for Redis console to perform failure simulations or tests. The `shutdown` command is sent to all master nodes to trigger the automatic high availability (HA) logic to perform failure simulation.

### Proxy failover

Proxy nodes are used in both standard and cluster architectures of TencentDB for Redis. The standard architecture has three proxy nodes, while the number of proxy nodes in the cluster architecture increases linearly with that of shards. The high availability design of proxy nodes is as follows:

- Multiple proxy nodes support the high availability and load balancing of the proxy service.
- Proxy nodes are deployed on three physical devices to ensure high availability.
- If a proxy node fails, the testing system will detect the failed node and automatically add new one.

### Redis server failover

TencentDB for Redis in standard architecture or cluster architecture adopts the same cluster management mechanism as the Redis Cluster, which uses the Gossip protocol to detect the status of nodes in a cluster. The `cluster-node-timeout` parameter is used to specify the maximum amount of time a Redis cluster node can be unavailable, without it being considered as failing. We recommend you set this parameter to its default value (1500 ms) and do not change it. For more information, see [Scaling with Redis Cluster](https://redis.io/topics/cluster-tutorial).

## Notes

- Only instances in the "Running" status can perform failure simulations.
-Only instances deployed in multi-AZ can perform failure simulations.

## Use Limits

A failure simulation will make Redis unavailable for less than one minute until the failover is completed. The data written during the simulation may be lost.
- The instance service downtime caused by failure simulations won't be counted into [SLA](https://intl.cloud.tencent.com/document/product/239/32288)

## Prerequisites

- The instance has been deployed in multi-AZ. For more information, see [Configuring Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/239/39799).
- The database is on v4.0 or later.
- The instance is in the **Running** status.

## Directions

1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis).
2. Above the **Instance List** on the right, select the region.
3. In the instance list, find the target instance.
4. On the instance management page, click **Node Management** tab, and select **Simulate Failure** in **More** drop-down list.
5. In the **Simulate Failure** pop-up window, check the instance name and ID, learn about how failure simulation works, and click **OK**. The instance status will change to **Processing**.
6. In the left sidebar, click **Task Management**, and wait for the task to be completed. The failure simulation is successfully performed when the instance status becomes **Running**.
   
   

##API

| API | Description |
| ------------------------------------------------------------ | ----------------- |
| [KillMasterGroup](www.tencentcloud.com/document/product/239/41430) | Performs a failure simulation |
| [SwitchProxy](www.tencentcloud.com/document/product/239/49647) | Simulates the failure of a proxy node |

