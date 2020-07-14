## Feature Overview
This document describes how to roll back component parameters to their previous configuration in the EMR Console.

## Directions 
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select the target cluster in **Cluster List**, and click **Details** to enter the cluster details page.
2. On the cluster details page, select **Cluster Service** and click **Operation** > **Configuration Management** in the top-right corner of the target component block. The following uses HDFS as an example.
![](https://main.qcloudimg.com/raw/3df957fe84cbc905fdefcd8d29ee8d8f.png)
3. Select **Configuration History** to view the configuration history of all components. On this tab, you can roll back to the last parameter configuration. Click **Details** to view the parameter values before and after the rollback. Select **Roll back** > **OK**. After the rollback is successful, the component will be restarted, and the previous configuration will take effect in a short while.
![](https://main.qcloudimg.com/raw/bf67f3da357c8b6592318167dce0cda1.png)![](https://main.qcloudimg.com/raw/b9fa163d09e3a2668d6c2ca2c4c1ad21.png)
