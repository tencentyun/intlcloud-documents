## Operation Scenarios
Configuration groups can be used to group and manage configurations of nodes with different specifications or for different purposes where the same component is deployed. This document describes how to use configuration groups to manage component configuration.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and select **Component Management** on the left sidebar. In the **Operation** column of the component whose parameters you want to modify, click **Configure**. Here, taking HDFS as an example, click **Configure** to proceed to the next step.
2. Click **Configuration Management**, set "Dimension" to **Configuration Group**, select the target configuration group and file where the parameters to be modified are located, and click **Modify Configuration** to add, modify, or delete parameters.
>After a cluster is created, a default configuration group will be generated for each component, which can be modified but cannot be deleted. During initialization, the default configuration group will inherit the cluster configuration. You can add configuration groups based on your needs, and each component can have up to 10 configuration groups.
3. Click **Manage Configuration Group** to set a configuration group.
![](https://main.qcloudimg.com/raw/ff447e9c6676627682ca593f857900b9.png)
 Enter the "Manage Configuration Group" page. You can click **Add Configuration Group**, **Modify**, or **Delete** to add, modify, or delete a configuration group, respectively.
![](https://main.qcloudimg.com/raw/2fce4a94775737259e58268c2038e1a9.png)
4. If the configuration of a node is different from that in the current configuration group, click **Sync Configuration** in the top-right corner to distribute the configuration in the configuration group to the node.
![](https://main.qcloudimg.com/raw/7286e6eb52685a59dfb0e53eed087dd5.png)
Enter the "Sync Configuration" page. You can click **Details** to view the detailed information or click **Sync Configuration** to sync the configuration group.
![](https://main.qcloudimg.com/raw/b1a3b1f5152d7632e3ae601d09084d5e.png)
