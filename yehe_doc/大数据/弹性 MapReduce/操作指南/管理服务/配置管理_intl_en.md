## Feature Overview
Configuration management allows you to modify key configuration parameters of common open-source components such as HDFS, YARN, Hive, and Spark. You can modify the service configurations at the cluster, node, or configuration group level as needed. This document describes how to configure service parameters in the console.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select the target cluster in **Cluster List**, and click **Service** to enter the cluster service list.
2. In the cluster service list, select **Operation** > **Configuration Management** in the top-right corner of the target service block. After entering the "Configuration Management" page, click **Modify Configuration** to add, modify, or delete parameters. You can also click **Create Configuration File** to add a custom configuration file and set its parameters.
![](https://main.qcloudimg.com/raw/f5ffa451824dc44731119181a0b3ad12.png)
 - To configure the parameters of all nodes of the selected service in the cluster, select cluster level.
 - To configure the parameters of a specified node of the selected service, select node level.
 - To configure the parameters of multiple specified nodes of the selected service, you can create a configuration group and use it as the level.
 ![](https://main.qcloudimg.com/raw/1934d86e9cdf2e908966e09b8a0ee47a.png)
3. Click **Modify Configuration** and enter the new parameter value for the target parameter. If needed, you can click **Recover** to recover a parameter to its original value. You can also click **Default Value** to recover the parameter to the default value recommended by the system. **Delete** next to a parameter indicates that this parameter can be deleted. To delete a parameter, select **Delete** > **Confirm**.
 ![](https://main.qcloudimg.com/raw/a31adba32e7f090d9ba8579278f7f15d.png)
4. If the parameter you want to configure does not exist, you can click **Add a configuration item** on the right to enter the "Add parameter" page. Enter the new parameter name and value and click **Confirm**.
 ![](https://main.qcloudimg.com/raw/6cf666b6bdde136fa74e1947f1289358.png)
5. If the configuration file you want to configure does not exist, you can click **Create Configuration File** on the bottom-left corner to enter the configuration file configuration page, configure the configuration file, and click **Save configuration**. The parameters will be delivered, and the configuration file name will be updated in the configuration file list.
 ![](https://main.qcloudimg.com/raw/92202b758597c9241a6095d7b23a0e74.png)
 After the custom configuration file is delivered and takes effect, it can be modified and deleted:
![](https://main.qcloudimg.com/raw/69ab9980a4415b86ab59e89eea611b44.png)
Save the configuration:
 ![](https://main.qcloudimg.com/raw/cf75abe561c0e8270400f6337644f2a8.png)
6. After completing parameter modification, click **Save configuration** and confirm the changes. We recommend you enter a reason of change for future reference. After confirming that all values are correct, click **Save and Deliver**. After the configurations are successfully delivered, click **Restart Service** to make the parameters take effect.
>!If you modify the service parameters on the Shell command line, and then modify them again in the EMR Console, the previous modifications made on the command line will be overridden.
>
 ![](https://main.qcloudimg.com/raw/7c5cf8771c4d2aae871e985197c9f4bb.png)
