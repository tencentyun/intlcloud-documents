## Overview
This document describes how to delete clusters that are no longer needed from the TKE console to avoid unnecessary costs. On the **Delete cluster** page, you can view all resources of a cluster, terminated resources, and choose whether to retain some resources as needed. Ensure that you are well aware of the operation risks before deleting clusters.



## Directions
### Disabling cluster deletion protection
#### Method 1
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and click **Cluster** in the left sidebar.
2. On the “Cluster management” page, locate the desired cluster, and select **More** > **Disable deletion protection** in the "Operation" column.
![](https://qcloudimg.tencent-cloud.cn/raw/1a3971617355afd5ded1b0365d031bce.png)
3. Click **OK** in the pop-up window.




#### Method 2
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and click **Cluster** in the left sidebar.
2. On the “Cluster management” page, click the name of the desired cluster to open the cluster details page.
3. On the cluster’s “Basic information” page, disable the deletion protection.
![](https://qcloudimg.tencent-cloud.cn/raw/40eb466fe2e2d7881e6fdbdf7c0febda.png)
4. Click **OK** in the pop-up window.


### Deleting a cluster
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and click **Cluster** in the left sidebar.
2. On the **Cluster management** page, choose **More** > **Delete** on the right of the target cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/ea49cf457b0d3f4598b8b4f0436e046e.png)
3. In the **Delete cluster** window that appears, choose to retain or delete existing resources of the cluster as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/519dddb5f2e1352cc848f12fac4c2aa0.png)
4. Read the risks of the cluster deletion operation, and tick "I have read the notice above and confirmed to delete the cluster".
5. Click **OK** to delete the cluster.



