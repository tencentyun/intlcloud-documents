## Operation Scenarios
This document describes how to modify component parameter configurations in the EMR Console.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and select **Component Management** on the left sidebar. In the **Operation** column of the component whose parameters you want to modify, click **Configure**. Here, taking HDFS as an example, click **Configure** to proceed to the next step.
![](https://main.qcloudimg.com/raw/1201009f394fc9453eb23f8265c6c18c.png)
2. Click **Configuration Management**, select the dimension and file where the parameters to be modified are located, and click **Modify Configuration** to add, modify, or delete parameters.
>The dimension refers to the range of nodes to which the configurations will be distributed. Three dimensions are supported: cluster (default value), server, and configuration group.
>- To configure all nodes that contain the selected component in the cluster, select cluster dimension.
>- To configure parameters of the selected component on a specific server, select server dimension.
>- To configure parameters of the selected component on multiple servers, you can create a configuration group and use it as the dimension.
>
![](https://main.qcloudimg.com/raw/683de629ff0fdc130d76af389a6e8ee0.png)
3. Click **Modify Configuration** and enter the new parameter value for the target parameter. If needed, you can click **Restore** to restore a parameter to its default value. **Delete** next to a parameter indicates that this parameter can be deleted. To delete a parameter, select **Delete** > **OK**.
![](https://main.qcloudimg.com/raw/9a005948931a0a46ac15b4d87b8a5d5e.png)
If the parameter you want to configure does not exist, you can click **Add Configuration Item** on the right to enter the "Add Parameter" page. Enter the new parameter name and value and click **OK**.
![](https://main.qcloudimg.com/raw/9d8ed6fbe5d6a9c454970809c029077a.png)
The new parameter will be displayed on the parameter page.
![](https://main.qcloudimg.com/raw/fd2925efe79ecb873b5270a199bcaf10.png)
4. Click **Save Configuration** to view the changes. You are recommended to enter a reason of change for future reference. After confirming that all values are correct, click **Save and Distribute**. After the configurations are successfully distributed, click **Restart Component** to make the parameters take effect.
>If you modify the component parameters on the Shell command line, and then modify them again in the EMR Console, the previous modifications made on the command line will be overridden.
>
![](https://main.qcloudimg.com/raw/7eb976becea5d56bd973a3102ae0cf35.png)
