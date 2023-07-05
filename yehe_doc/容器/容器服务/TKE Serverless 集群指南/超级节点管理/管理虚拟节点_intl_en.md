This document describes how to manage super nodes in the serverless cluster on the TKE console.



## Prerequisites

- Please ensure the serverless cluster has been created.
- You have known [Notes on Scheduling Pod to Super Node](https://intl.cloud.tencent.com/zh/document/product/457/39760).



### Deleting a super node

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the management page of clusters, click the serverless cluster ID to open the basic information page.
3. Click **Super Node** in the left sidebar to open **Super Nodes** list page.
4. On the list page, click **Remove** on the right side of the selected super node.
5. Click **OK** to delete the node on the **Delete Node** pop-up window
<dx-alert infotype="explain" title="">
  - At least one super node is required for the cluster. If there is only one super node, it cannot be deleted.
  - The super node with a running Pod cannot be deleted. Please cordon and drain the node before remove it. Once drained, the Pod will be rebuilt.

</dx-alert>

### Managing a super node


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the management page of clusters, click the serverless cluster ID to open the basic information page.
3. Click **Super Node” in the left sidebar to open **Super Nodes** list page.
5. Click the super node name to open its details page. You can manage the Pods on the super node, and view super node events, YAML and other information.


### Modifying configuration of a super node

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the management page of clusters, click the serverless cluster ID to open the basic information page.
3. Click **Super Node** in the left sidebar to open **Super Nodes** list page.
4. Select the desired node, and click **Edit Label & Taint** on the right side of the super node.
5. In the **Modify Super Node Label & Taint** pop-up, modify the Label&Taint configuration of the super node.
6. Click **OK** to complete the modification.

