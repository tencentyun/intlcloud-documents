## Overview

Kubernetes Events contains information about the operations of Kubernetes clusters and the scheduling of various resources, which can help OPS personnel monitor daily changes in resources and locate problems. EKS supports event persistence for all clusters and also supports the search of event flows by using PAAS services provided by Tencent Cloud or open-source software tools. After enabling this feature, your cluster events will be exported to the configured storage in real time. This document describes how to enable and use persistent storage of cluster events.


## Directions


### Enabling event storage
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Choose **Cluster OPS** > **Feature Management** in the left sidebar to go to the **Feature Management** page.
3. At the top of the **Feature Management** page, select the region and select **Elastic Cluster** as **Cluster Type**. On the right side of the cluster for which you want to enable event storage, click **Set**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/7cf4d24bb5e0e10d8102495c778b3e33.png)
4. On the **Configure Features** page, click **Edit** for event storage.
5. On the **Event Storage** editing page, select **Enable Event Storage** and configure logsets and log topics, as shown in the figure below:
![](https://main.qcloudimg.com/raw/24ec7b1276b7c5752db54c54eeeddb43.png)
6. Click **Confirm** to enable event storage.


### Updating logsets or log topics
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Choose **Cluster OPS** > **Feature Management** in the left sidebar to go to the **Feature Management** page.
3. At the top of the **Feature Management** page, select the region and select **Elastic Cluster** as **Cluster Type**. On the right side of the cluster for which you want to enable event storage, click **Set**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/7cf4d24bb5e0e10d8102495c778b3e33.png)
4. On the **Configure Features** page, click **Edit** for event storage.
5. On the **Event Storage** editing page, reselect logsets and log topics. Then, click **OK** to update the logsets and log topics.


### Disabling event storage
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Choose **Cluster OPS** > **Feature Management** in the left sidebar to go to the **Feature Management** page.
3. At the top of the **Feature Management** page, select the region and select **Elastic Cluster** as **Cluster Type**. On the right side of the cluster for which you want to enable event storage, click **Set**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/7cf4d24bb5e0e10d8102495c778b3e33.png)
4. On the **Configure Features** page, click **Edit** for event storage.
5. On the **Event Storage** editing page, deselect **Enable Event Storage**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/1b71e6bdbc862a44a3c32430f2bc1af3.png)
6. Click **Confirm** to disable event storage.

### Viewing event in the CLS console
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Select **Log Search** on the left side bar to go to the **Search and Analysis** page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/b876944806657fd1b1f2eb26e065b542.png)
3. Select the logset and log topic configured in [Event Storage](#open), set the **Showed Field** as needed, and click **Search and Analysis**. For more information, see [Log Analysis](https://intl.cloud.tencent.com/document/product/614/37803).
>! When you enable event storage, the index will be enabled for your Topic by default.
