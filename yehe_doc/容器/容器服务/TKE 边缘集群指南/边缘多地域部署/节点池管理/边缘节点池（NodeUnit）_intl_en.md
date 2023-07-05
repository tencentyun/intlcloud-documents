## Overview
This document describes how to manage edge node pools of an edge container in the TKE console.
This update reconstructs the UI interaction between the earlier versions of NodeGroup and NodeUnit. Clusters created after March 29, 2022 will use the new interaction logic, and clusters on earlier versions will not be affected. In this update, the edge node pool corresponds to the design of NodeUnit in SuperEdge, and node pool category corresponds to the design of NodeGroup in SuperEdge. For detailed design principles, see [Managing Edge Resources by Application Resource Pool](https://github.com/superedge/superedge/blob/main/docs/components/site-manager_CN.md).

## Overview
In edge scenarios, nodes are assigned more attributes. For example, different nodes can be placed in different network environments, architectures, and cloud services. In some specific scenarios, users can divide nodes with the same characteristics into different groups. For example, if three nodes are located in the Beijing region and the other five nodes are located in the Guangzhou region, we can divide them into two node pools, Beijing and Guangzhou, according to their geographical attributes. Different node pools can schedule and deploy different applications. We name a node pool 'NodeUnit' resource, as a CRD resource implemented for Kubernetes. The platform interacts with users through this CRD and manages nodes in groups by labeling nodes through Kubernetes, as shown in the figure below:

<div><img src="https://qcloudimg.tencent-cloud.cn/raw/fd961e6095e2188ee836720b23b47c50.png" width="100%" alt=""></img></div>

## Directions


>!  As operations on an edge node pool will affect the labels of the nodes, perform such operations with caution.

### Creating an edge node pool
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the **Cluster Management** page, click the ID of the target cluster to go to its details page.
3. Select **Node management** > **Edge node pool** in the left sidebar to go to the **Edge node pool list** page.
![](https://qcloudimg.tencent-cloud.cn/raw/75f5fd58ee85c455f36986cbed5a4a2e.png)
 Each cluster has a default node pool (`unit-node-all`), which contains all edge nodes added to the cluster.
4. Click **Create node pool**. In the **Create edge node pool** pop-up window, enter the node pool name and add available nodes as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/715a4641bdaff203a798eda80afc6cba.png)
5. Click **Done**. You can view added nodes in the edge node pool list.

 

### Managing edge node pools
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the **Cluster Management** page, click the ID of the target cluster to go to its details page.
3. Select **Node management** > **Edge node pool** in the left sidebar to go to the **Edge node pool list** page.
4. Click **Update configuration** on the right of an edge node pool. On the **Update node pool** page, you can add and delete existing nodes.


### Deleting an edge node pool
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the **Cluster Management** page, click the ID of the target cluster to go to its details page.
3. Select **Node management** > **Edge node pool** in the left sidebar to go to the **Edge node pool list** page.
4. Click **Delete** on the right of an edge node pool to delete the pool.
