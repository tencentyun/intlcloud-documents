## Overview
You can create a custom image in addition to using available Tencent Cloud public images and marketplace images. The custom image can be used to quickly create Tencent Cloud CVM instances with the same configurations as the image in Tencent Cloud console.


<dx-alert infotype="explain" title="">
Images use the CBS snapshot service for data storage:
 -A free tier of 50 GB is provided in domestic regions. For more information, please see [Free Tier](https://intl.cloud.tencent.com/document/product/362/32415).
 - When creating a custom image, an associated snapshot will also be created by default. As a result, retaining custom images incurs costs. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415).
</dx-alert>




## Notes

- Each region supports a maximum of 10 custom images.
- The following directories and files will be removed.
 - `/var/log/`  
 - `/root/.bash_history` and `/home/ubuntu/.bash_history` (for the Ubuntu operating system)
- When creating a custom image on a Linux instance, make sure `/etc/fstab` does not contain data disk configuration. Otherwise, instances created with this image cannot be launched normally. If the Linux instance that is used to create a custom image with a data disk mounted, comment out or delete the relevant data disk configurations in `/etc/fstab`.
- The creation process takes ten minutes or more, which depends on the data size of the instance. Please prepare in advance to avoid business impacts.
- CPM 2.0 does not support the use of console and API to create custom images. You can use CVM to create them.
- If your Windows instance needs to enter a domain and uses a domain account, please execute Sysprep before creating a custom image to ensure that the SID is unique after the instance enters the domain. For more information, please see [Ensuring Unique SIDs for CVMs Using Sysprep](https://intl.cloud.tencent.com/document/product/213/35876).

## Directions
<dx-tabs>
::: Creating a custom image from an instance through the console

#### Shut down an instance (optional)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) and check whether the corresponding instance needs to be shut down.
<dx-alert infotype="notice" title="">
For CVMs created based on public images after July 2018, creating images online is supported (i.e., you can create images without shutting down the instance). For other CVMs, shut down the instance before creating a custom image to ensure that the image has the same environment deployment as the current instance.
</dx-alert>
  - If the instance needs to be shut down, proceed to the next step.
  - If the instance don’t need to be shut down, please proceed to [Create a custom image](#createOS)
2. On the instance management page, proceed according to the actually used view mode:
  - **List view**: in the row of the target instance, select **More** > **Instance Status** > **Shut down** on the right as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/238862ade0b78fb22702311d0b5e2a71.png)
  - **Tab view**: in the row of the target instance, select **More** > **Instance Status** > **Shut down** on the right as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/faa7bfc8122037333ff5ebd7209550bc.png)


#### Create a custom image[](id:createOS)
1. On the instance management page, proceed according to the actually used view mode:
   - **List view**: select **More** > **Create Image** as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/37a94f32c4d32bb31f04767ccd070e4b.png)
   - **Tab view**: select **More Actions** > **Create Image** in the top-right corner as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/9327ceb162dc61f30be71f7d2f06137b.png)
2. In the pop-up "Create a custom image" window, please refer to the following information for configuration:
  - **Image name** and **Image description**: Custom name and description.
  - **Create a system disk image only**: if your instance only has a system disk, this option will not appear. If your instance has a data disk, select it as needed.
     - If checked, only a system disk image of the instance will be created.
     - If unchecked, a data disk snapshot will be created at the same time when the instance has a data disk mounted.
3. Click **Create image**.
You can click **[Image](https://console.cloud.Tencent.com/CVM/image)** on the left sidebar to view the creation progress in the "Image" page.


#### Use the custom image to create an instance (optional)
Select the image you created in the image list, and click **Create Instance** on the right side to purchase the server with the same custom image, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2d64df77d16b3c26d275770e03a1caf1.png)

:::
::: Creating a custom image by using \sAPI\s
You can use the `CreateImage` API to create a custom image. For more information, please see [CreateImage](https://intl.cloud.tencent.com/zh/document/product/213/33276).
:::
</dx-tabs>

## Best Practices

### Migrating the data on a data disk

If you need to keep the data on the data disk of the original instance when launching a new instance, you can first take a [snapshot](https://intl.cloud.tencent.com/document/product/362/31638) of the data disk, and then use this data disk snapshot to create a new CBS data disk.
For more information, please see [Creating Cloud Disks Using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757).
