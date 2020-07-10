## Feature Overview
Configuration delivery is used to modify the parameter configurations in some key usage cases of various components in the EMR Console, but some components may not contain all the parameters of open-source features. If modification is needed, you can add or modify parameters for the component through the configuration management feature in the EMR Console. Added or modified parameters will be saved in the configuration file of the component, take effect after component restart, and be delivered at the node level.

The level refers to the range of nodes to which the configurations will be delivered. Three levels are supported: cluster (default value), server, and configuration group. This document describes how to configure component parameters in the console.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select the target cluster in **Cluster List**, and click **Details** to enter the cluster details page.
2. Select **Cluster Service** on the cluster details page and click **Operation** > **Configuration Management** in the top-right corner of the target component block. After entering the **Configuration Management** page, click **Modify Configuration** to add, modify, or delete parameters.
![](https://main.qcloudimg.com/raw/f20c5dc2cf851396c9b8cdae2c189f78.png)
 - To configure all nodes that contain the selected component in the cluster, select cluster level.
 - To configure parameters of the selected component on a specific server, select server level.
 - To configure parameters of the selected component on multiple servers, you can create a configuration group and use it as the level.
![](https://main.qcloudimg.com/raw/1934d86e9cdf2e908966e09b8a0ee47a.png)
3. Click **Modify Configuration** and enter the new parameter value for the target parameter. If needed, you can click **Recover** to restore a parameter to its default value. **Delete** next to a parameter indicates that this parameter can be deleted. To delete a parameter, select **Delete** > **OK**.
![](https://main.qcloudimg.com/raw/a31adba32e7f090d9ba8579278f7f15d.png)
If the parameter you want to configure does not exist, you can click **Add Configuration Item** on the right to enter the "Add Parameter" page. Enter the new parameter name and value and click **OK**. Then, the new parameter will be displayed on the parameter page.
![](https://main.qcloudimg.com/raw/6cf666b6bdde136fa74e1947f1289358.png)
![](https://main.qcloudimg.com/raw/cf75abe561c0e8270400f6337644f2a8.png)
4. Click **Save Configuration** to view the changes. You are recommended to enter a reason for change for future reference. After confirming that all values are correct, click **Save and Deliver**. After the configurations are successfully delivered, click **Restart Component** to make the parameters take effect.
>If you modify the component parameters on the Shell command line, and then modify them again in the EMR Console, the previous modifications made on the command line will be overridden.
>
![](https://main.qcloudimg.com/raw/4a7139cc288c097ec38803cd0c87e784.png)
