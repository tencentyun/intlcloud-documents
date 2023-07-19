## Overview
When the resources of your EMR cluster are excessive, you can remove task nodes in the console. When the cluster has router nodes that do not share the load of the master node or that serve as task submitters in the cluster, you can remove nodes to achieve cluster scale-in.

## Preparations
Since core nodes store data, we recommend you not terminate them to avoid data security issues. After a node is terminated, the data stored in it will be deleted. By terminating a node, you confirm that the data in it can be deleted.
- Pay-as-you-go cluster: Once terminated, the cluster will not be retained in the recycle bin but will be permanently terminated. Please proceed with caution.

>! Before terminating a cluster, please make sure that your data has been backed up as it cannot be recovered after cluster termination.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list.
2. On the **Cluster details** page, select **Cluster resources > Resources**, select cloud resources (task or router nodes) that can scale in from the node list. If two or more types of nodes are selected, the **Scale in** button will be unavailable.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/BnzD883_%E5%9B%BD%E9%99%85124.png)
3. In the pop-up window, confirm the instances to be terminated (removed). If the cluster metaDB is a shared metadatabase, the disk will be retained in this operation and needs to be manually removed in the CDB console.
