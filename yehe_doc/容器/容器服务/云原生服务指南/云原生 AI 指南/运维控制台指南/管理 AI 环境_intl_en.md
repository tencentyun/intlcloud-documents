
This document describes AI environments and how to manage them, such as how to create, view, and delete them.

## AI Environment Overview 
AI environment is an important abstract concept of Cloud Native AI. An AI environment runs in a TKE/EKS container cluster, and the Ops team can manage its lifecycle as needed. For example, for different upper-layer AI businesses, the AI Ops team can combine applicable add-ons to set up diverse AI environments based on various business needs.




## Directions
### Creating an AI environment
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native AI** on the left sidebar.
2. On the **AI Environment** list page, click **Create** to enter the **Create AI Environment** page and set the parameters.
 - **Environment Name**: Custom environment name. You can name the environment based on information such as business needs to facilitate subsequent resource management.
 - **Region**: The region of the cluster where the AI environment is to be deployed.
 - **Cluster Type**: The type of cluster where the AI environment is to be deployed.
 - **Cluster**: The cluster where the AI environment is to be deployed.
 - **Deploy Add-On**: Add-ons to be deployed in the AI environment. You can also install and delete add-ons in [Add-On Management](https://intl.cloud.tencent.com/document/product/457/49370) after environment creation.
5. Click **Create**.

### Viewing an AI environment

After creating an AI environment, you can view it on the **AI Environment** list page.



### Deleting an AI environment

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cloud Native AI** on the left sidebar.
2. On the **AI Environment** list page, click **Delete** on the right of the target environment.
3. In the **Delete AI Environment** pop-up window, read the notes on deletion and click **Confirm**.




