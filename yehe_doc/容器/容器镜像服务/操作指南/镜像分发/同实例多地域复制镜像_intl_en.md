
## Overview
Tencent Container Registry (TCR) allows users to create replicas of a premium instance in multiple regions with the same access domain name and credential as the original premium instance. It realizes the single-region upload, multi-region high-speed real-time synchronization, and image pulling from the nearest region over the private network. Compared with the cross-instance synchronization, this feature can unify the publish configuration of multi-regional clusters, improve the cross-region synchronization speed of cloud native artifacts, and help users realize the global synchronization update of service applications.

The instance replication feature allows users to create replicas of a premium instance in multiple regions. The replica instances will synchronize data with the primary instance in real time. Users can use the domain name and access credentials of the primary instance to access the replica instances through the private network. By using the instance replication feature, users can uniformly manage the application images of the multi-regional services, and do not need to purchase multiple Enterprise Edition instances, which can reduce the usage cost, increase the speed of container image distribution, and simplify the deployment and configuration.
![](https://main.qcloudimg.com/raw/96e4f98d287af0d7b8c6ae54c631e33b.png)

## Prerequisites

Before creating and managing the replica instance of a TCR Enterprise Edition instance, complete the following preparations:
- You have [purchased an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/39088) with premium specification.
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Creating and managing a replica instance
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Synchronization and Replication** > **Instance Replication** on the left sidebar.
2. On the **Instance Replication** page, select a region and an instance, and click **Create**.
3. In the **Create Replica Instance** window, complete the following configurations:
![](https://main.qcloudimg.com/raw/a1f8c93664f0fcaaeb1313a26d4ba6c0.png)
 - **Primary Instance Name**: the name of the currently selected premium instance.
 - **Default Region**: the region where the currently selected premium instance is located.
 - **Replicate to**: the region where the replica instance is located, which cannot be the same as the region of the current primary instance.
4. Click **OK**.

<dx-alert infotype="notice" title="">
You can delete the replication instances that are no longer needed in the specified region. If a premium instance has configured the replica instances, you need to delete all the replica instances first to delete the premium instance.
</dx-alert>

### Viewing image replication logs
After configuring a replica instance, if you push an image to the primary instance, the image data will be automatically replicated to the replica instance.

### Accessing the replica instance via the private network
1. To ensure that the container clusters or CVMs in the replication region can access the instance through the private network, you need to connect the VPCs in the replication region to the instance. Please refer to [Private Network Access Control](https://intl.cloud.tencent.com/document/product/1051/35492), and choose the VPC in the replication region.
2. After the above configuration is completed, the container clusters or CVMs in the replication region can access the instance through the private network. The image access address and access credentials are the same as those of the premium instance in the original region.

## References

You can also use the `CreateReplicationInstance` API to create a replica instance. For more information, see [CreateReplicationInstance](https://intl.cloud.tencent.com/document/product/1051/42673).

