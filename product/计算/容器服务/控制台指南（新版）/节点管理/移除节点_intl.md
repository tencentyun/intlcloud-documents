## Operation Scenario

This document guides you through the process of removing a node from a cluster.

## Precautions

- A prepaid node will not be terminated after it is removed from the cluster.
- A pay-as-you-go node can be retained or terminated as you wish, but if it is not terminated, fees will continue to be incurred.
- If a node is removed from and then added back to the cluster, the system will be reinstalled. Please be cautious when doing so.

## Steps

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left navigation pane, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. Click the ID/name of the cluster from which to remove the node to go to the management page of the cluster. See the figure below:
![](https://main.qcloudimg.com/raw/a81fa565be60dbddafe55010319a4e08.png)
4. In the left navigation pane, select "Node Management" > "Nodes" to go to the "Node list" page.
5. In the node list, select the row of the node to be removed and click **Remove**.
6. In the "Are you sure you want to remove the following nodes?" window that pops up, click **OK** to complete the removal.
