
## Overview
Tencent Container Registry (TCR) allows users to configure replica instances in other regions of the world for premium instances. Users can use the unified domain name and access credentials to access the replica instances, so as to realize single-region upload, multi-region high-speed real-time synchronization, and image pulling from the nearest region over the private network. Compared with the cross-instance synchronization, this feature can unify the publish configuration of multi-regional clusters, improve the cross-region synchronization speed of cloud native artifacts, and help users realize the global synchronization update of service applications.

The instance replication feature allows users to configure replication instances in multiple regions for premium instances. The replica instances will synchronize data with the primary instance in real time. Users can use the domain name and access credentials of the primary instance to access the replica instances through the private network. By using the instance replication feature, users can uniformly manage the application images of the multi-regional services, and do not need to purchase multiple Enterprise Edition instances, which can reduce the usage cost, increase the speed of container image distribution, and simplify the deployment and configuration.
![](https://main.qcloudimg.com/raw/96e4f98d287af0d7b8c6ae54c631e33b.png)

## Prerequisites

Before creating and managing the replica instance of a TCR Enterprise Edition instance, complete the following preparations:
- You have [purchased an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088) with premium specification.
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Creating and managing a replica instance
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Instance** in the left sidebar.
2. Select an instance in the instance list and go to its details page.
3. In the **Instance Replication** tab, click **Create** and set the following parameters in the pop-up window.
![](https://main.qcloudimg.com/raw/a1f8c93664f0fcaaeb1313a26d4ba6c0.png)
 - **Primary Instance Name**: the name of the currently selected premium instance.
 - **Default Region**: the region where the currently selected premium instance is located.
 - **Replicate to**: the region where the replica instance is located, which cannot be the same as the region of the current primary instance.
4. Click **OK** to complete the creation of the replica instance.
>! If the replica instance in the specified region is no longer needed, the replica instance can be deleted. If a premium instance has configured the replica instances, you need to delete all the replica instances first to delete the premium instance.


### Accessing the replica instance via the private network
1. After completing the instance replication, you can push images to this instance through public network or private network. The container images will be replicated to the replication region in real-time, as shown in the figure below:
![](https://main.qcloudimg.com/raw/1d977f305dee27b3e40a1afa06291a30.png)
2. To ensure that the container clusters or CVMs in the replication region can access the instance through the private network, you need to connect the VPCs in the replication region to the instance. Please refer to [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492), and choose the VPC in the replication region.
3. After the above configuration is completed, the container clusters or CVMs in the replication region can access the instance through the private network. The image access address and access credentials are the same as those of the premium instance in the original region.
