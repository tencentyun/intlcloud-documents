## Overview

This document describes how to manage virtual nodes in the elastic cluster on the TKE console.



## Prerequisites

- Please ensure the elastic cluster has been created.
- You have known [Notes on Scheduling Pod to Virtual Node](https://intl.cloud.tencent.com/zh/document/product/457/39760).



### Deleting a virtual node

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Elastic Container** > **Elastic Cluster** in the left sidebar to go to the list page of elastic clusters.
2. On the list page of clusters, click the desired cluster ID to open the **Deployment** page.
3. Click **Virtual Node” in the left sidebar to open **Virtual Nodes** list page.
4. On the list page, click **Remove** on the right side of the selected virtual node.
5. Click **OK** to delete the node on the **Delete Node** pop-up window
<dx-alert infotype="explain" title="">
  - At least one virtual node is required for the cluster. If there is only one virtual node, it cannot be deleted.
  - The virtual node with a running Pod cannot be deleted. Please cordon and drain the node before remove it. Once drained, the Pod will be rebuilt.

</dx-alert>

### Managing a virtual node


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Elastic Container** > **Elastic Cluster** in the left sidebar to go to the list page of elastic clusters.
2. On the list page of clusters, click the desired cluster ID to open the **Deployment** page.
3. Click **Virtual Node” in the left sidebar to open **Virtual Nodes** list page.
5. Click the virtual node name to open its details page. You can manage the Pods on the virtual node, and view virtual node events, YAML and other information.


### Modifying configuration of a virtual node

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Elastic Container** > **Elastic Cluster** in the left sidebar to go to the list page of elastic clusters.
2. On the list page of clusters, click the desired cluster ID to open the **Deployment** page.
3. Click **Virtual Node” in the left sidebar to open **Virtual Nodes** list page.
4. Select the desired node, and click **Edit Label & Taint** on the right side of the virtual node.
5. In the **Modify Virtual Node Label & Taint** pop-up, modify the Label&Taint configuration of the virtual node.
6. Click **OK** to complete the modification.

