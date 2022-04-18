## Feature Overview
The cluster scale-in feature allows you to remove task nodes in the console when your EMR cluster has excessive computing resources. If there are router nodes in the cluster that do not need to share the load of the master nodes or serve as cluster task submitters, they can also be removed through the cluster scale-in.

## Prerequisites
You are not recommended to terminate the core node after the scale-out, as it stores your data and you may lose your data if it is terminated. After a node is terminated, the data stored in it will be deleted. By terminating a node, you confirm that the data in it can be deleted.
- On-demand cluster: once terminated, the cluster will not be retained in the recycle bin but will be completely terminated and cannot be recovered. Please do so with caution.

>! Before terminating a cluster, please make sure that your data has been backed up as it cannot be recovered after termination.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster List**, and click the ID/Name of the target cluster to enter the cluster details page.
2. Select **Cluster Resource** > **Resource Management** on the cluster details page and select the Tencent Cloud resources (task or router node) that support scale-in in the node list, and click **Scale In**. If you select nodes of other types, the **Scale In** button will be grayed out.
![](https://main.qcloudimg.com/raw/b146684f52a16a53ba8e92b9ab69ae67.png)
3. In the pop-up window, confirm the instance for termination (scale-in). If the data disk of a node is a shared metadatabase, the node will be retained, and you need to manipulate it the CBS Console.
