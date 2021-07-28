## Feature Overview
A configuration group is used to group and manage nodes that are equipped with the same services but have different specifications or purposes. This document describes how to use a configuration group to manage service configuration.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select the target cluster in **Cluster List**, and click **Details** to enter the cluster details page.
2. On the cluster details page, select **Cluster Services** and click **Operation** > **Configuration Management** in the top-right corner of the target component block. The following uses HDFS as an example.
3. Click **Configuration Management**, set "Level" to **Configuration Group**, select the target configuration group and file where the parameters to be modified are located, and click **Modify Configuration** to add, modify, or delete parameters.
>?After a cluster is created, a default configuration group that inherits the cluster-level configuration is generated for each component, which can be modified but cannot be deleted. You can add new configuration groups to a component as needed. Each component can have up to 10 configuration groups.
4. Click **Manage Configuration Group** to enter the "Manage Configuration Group" page. You can click **Add Configuration Group**, **Modify**, or **Delete** to add, modify, or delete a configuration group, respectively.
![](https://main.qcloudimg.com/raw/ff447e9c6676627682ca593f857900b9.png)
![](https://main.qcloudimg.com/raw/a0b2473ce46ffa36cf7ee5c090777b65.png)
![](https://main.qcloudimg.com/raw/9f7d7373ed884a0251e52ee133c98fa0.png)
5. If the configuration of a node is different from that in the current configuration group, click **Sync Configuration** in the top-right corner to deliver the configuration in the configuration group to the node.
![](https://main.qcloudimg.com/raw/7286e6eb52685a59dfb0e53eed087dd5.png)
Enter the "Sync Configuration" page. You can click **Details** to view the detailed information or click **Sync Configuration** to sync the configuration group.
![](https://main.qcloudimg.com/raw/b1a3b1f5152d7632e3ae601d09084d5e.png)
