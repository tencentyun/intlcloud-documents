## Overview
This document describes how to manage edge node pools of an edge container in the TKE console.
This update reconstructs the UI interaction between the earlier versions of NodeGroup and NodeUnit. Clusters created after March 29, 2022 will use the new interaction logic, and clusters on earlier versions will not be affected. In this update, the edge node pool corresponds to the design of NodeUnit in SuperEdge, and node pool category corresponds to the design of NodeGroup in SuperEdge. For detailed design principles, see [Managing Edge Resources by Application Resource Pool](https://github.com/superedge/superedge/blob/main/docs/components/site-manager_CN.md).

 

## Directions


>!  As operations on an edge node pool will affect the labels of the nodes, perform such operations with caution.

### Creating an edge node pool
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Edge Clusters** on the left sidebar.
2. Click a **Cluster ID** to enter the cluster details page.
3. Select **Node Management** > **Edge Node Pool** on the left sidebar to enter the **Edge Node Pool List** page.
![](https://qcloudimg.tencent-cloud.cn/raw/75f5fd58ee85c455f36986cbed5a4a2e.png)
 Each cluster has a default node pool (`unit-node-all`), which contains all edge nodes added to the cluster.
4. Click **Create Node Pool**. On the **Create Edge Node Pool** page, enter the node pool name and add existing nodes as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/715a4641bdaff203a798eda80afc6cba.png)
5. Click **Done**. You can view added nodes in the edge node pool list.
![](https://qcloudimg.tencent-cloud.cn/raw/ea243361f4d07ff693aa8225ce05be26.png)

 

### Managing an edge node pool
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Edge Clusters** on the left sidebar.
2. Click a **Cluster ID** to enter the cluster details page.
3. Select **Node Management** > **Edge Node Pool** on the left sidebar to enter the **Edge Node Pool List** page.
4. Click **Modify Node List** on the right of an edge node pool. On the **Modify Edge Node Pool** page, you can add and delete existing nodes.


### Deleting an edge node pool
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Edge Clusters** on the left sidebar.
2. Click a **Cluster ID** to enter the cluster details page.
3. Select **Node Management** > **Edge Node Pool** on the left sidebar to enter the **Edge Node Pool List** page.
4. Click **Delete** on the right of an edge node pool to delete the pool.
