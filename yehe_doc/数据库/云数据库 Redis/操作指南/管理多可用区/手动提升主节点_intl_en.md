For multi-AZ deployed TencentDB for Redis instances in the standard/cluster architecture, you can manually promote a replica node/node group to master node/node group. You can deploy the master node in a specified AZ/node group.

## Promotion in Standard Architecture

A multi-AZ deployed instance in the standard architecture can have only one master node. You can promote a replica node to master node, and the old master node will be automatically demoted to replica node simultaneously.

The promotion process is as follows:

1. Promote the replica node to master node. (If the node is already a master node, skip the step.)
2. Promote the AZ to master AZ.

### Directions

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the **Node Management** page, click **Promote to Master Node/AZ** in the node list.
   ![](https://main.qcloudimg.com/raw/0ae356733962b9bde8a3b415a5ad9b8c.png)
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.
   ![](https://main.qcloudimg.com/raw/7519780d59c9ac4ced2f201499c599a8.png)

## Promotion in Cluster Architecture

An instance in the cluster architecture has multiple replicas per shard. Master nodes are in the master node group, while replica nodes in the replica node groups. Each group has a name. This makes node management easier.

For a multi-AZ deployed instance in the cluster architecture, you can promote a replica node group to master node group. If the master nodes of some shards are switched from a node group to others, you can promote the node group so that all of its nodes will become master nodes.

The promotion process is as follows:

1. Promote all nodes in the node group to master nodes. (If all of the nodes are already master nodes, skip the step.)
2. Promote the node group to master node group. If a server-level failover occurs after the promotion is completed, some of the nodes in the node group will be demoted to replica nodes and promoted back to master nodes.
3. Promote the AZ to master AZ.

### How it works

- TencentDB for Redis in the standard/cluster architecture runs the `cluster failover` command to promote a replica node/node group to master node/node group.
- Promoting nodes will trigger a master-replica switch. During the switch, database access will be affected for few seconds to 3 minutes, and blocking commands (including BLPOP, BRPOP, BRPOPLPUSH, and SUBSCRIBE) may fail one or more times before they can be executed successfully.
- If the promotion fails, you can try again.
- After promoting a replica node to master node, your access may be routed across multiple AZs, increasing the service response latency and decreasing [QPS](https://intl.cloud.tencent.com/document/product/239/31950#qps.2F.E5.B9.B6.E5.8F.91).

### Directions

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the **Node Management** page, click **Promote to Master Node Group** in the node list.
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.
   ![](https://main.qcloudimg.com/raw/7519780d59c9ac4ced2f201499c599a8.png)
