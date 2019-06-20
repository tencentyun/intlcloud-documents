## Operation Scenario

TKE has the feature to upgrade the Kubernetes version, which allows you to upgrade your running Kubernetes clusters.

## Precautions

- When upgrading a cluster, you need to upgrade the Master before the Node.
- When upgrading a node, the Pods running on the node will be evicted. Therefore, it is recommended that you create a node of appropriate configuration in advance to ensure that the cluster has enough resources to store the evicted Pods.
- When upgrading a node, the system will be reinstalled. Please back up the data in advance.
- Please check whether the nodes in the cluster are healthy before upgrading it. If there are unhealthy nodes, you can fix them by yourself or [submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to contact us for assistance.

## Steps

1. [Submit a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to contact us for upgrading the Master.
2. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
3. In the left navigation pane, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** to go to the cluster management page.
4. In the row of the cluster to be upgraded, click **More** > **Upgrade cluster**.
4. Select the node to be upgraded (you can upgrade nodes in batches, but you need to ensure that all nodes in the cluster are upgraded), and enter the node-related configuration.
5. Click **Finish** to complete the upgrade. You can view the upgrade status of the nodes in the node list.

 The nodes will be upgraded on a rolling basis, i.e., one node can be upgraded only after the previous one is upgraded.

