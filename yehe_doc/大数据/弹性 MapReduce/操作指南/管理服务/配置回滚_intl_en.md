## Feature Overview
 The EMR console supports rolling back the latest parameter configuration of components to their previous configuration. This document describes how to do so.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click a cluster ID on the **Cluster List** page to go to the cluster details page.
2. On the cluster details page, select **Cluster Service** and click **Operation** > **Configuration Management** in the top right corner of the target component section. The following uses HDFS as an example.
![](https://main.qcloudimg.com/raw/f6fa95eb30aa3b929bd1ea4dd86462d1.png)
3. Select **Configuration Record** to view the configuration history of all components. On this tab, you can roll back the latest parameter configuration to its previous configuration. Click **Details** to view the parameter values before and after the rollback and click **Rollback** > **Confirm Rollback**. After the rollback is successful, the component will be restarted, and the previous configuration will take effect in a short time.
![](https://main.qcloudimg.com/raw/bf67f3da357c8b6592318167dce0cda1.png)
![](https://main.qcloudimg.com/raw/b9fa163d09e3a2668d6c2ca2c4c1ad21.png)
