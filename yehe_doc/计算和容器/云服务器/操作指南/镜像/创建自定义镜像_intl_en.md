## Overview
Besides public images provided by Tencent Cloud, you can also create custom images, with which you can create CVM instances with the same configurations.


<dx-alert infotype="explain" title="">
Images use the CBS snapshot service for data storage:
 - Upon the creation of a custom image, a snapshot is automatically created and associated with the image. As a result, retaining custom images incurs costs. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415).
</dx-alert>




## Notes

- Each region supports a maximum of 10 custom images.
- The image does not include contents in the following directories and files:
 - `/var/log/`  
 - `/root/.bash_history` and `/home/ubuntu/.bash_history` (for the Ubuntu operating system)
- When creating a custom image by using a Linux instance, make sure that `/etc/fstab` does not contain data disk configuration. Otherwise, instances created with this image cannot be launched normally. If the Linux instance is mounted with a data disk, comment out or delete the relevant data disk configurations in `/etc/fstab`.
- The creation process takes ten minutes or longer, which depends on the data size of the instance. Prepare in advance to avoid business impacts.
- You cannot create an image by using a CPM instance in the console or via the API. You can use CVM to create it.
- If your Windows instance needs to enter a domain and uses a domain account, execute Sysprep before creating a custom image to ensure that the SID is unique after the instance enters the domain. For more information, see [Ensuring Unique SIDs for CVMs Using Sysprep](https://intl.cloud.tencent.com/document/product/213/35876).

## Directions
<dx-tabs>
::: Console

#### Shutting down the instance (optional)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) and check whether the corresponding instance needs to be shut down.
<dx-alert infotype="notice" title="">
For CVM instances created based on public images after July 2018, you can create images without shutting down the instances. For other CVM instances, shut down them before creating an image to ensure that the image has the same environment deployment as the current instances.
</dx-alert>
  - If the instance needs to be shut down, proceed to the next step.
  - If the instance doesn't need to be shut down, proceed to [Creating custom image](#createOS).
2. On the instance management page, proceed according to the actually used view mode:
  - **List view**: In the row of the target instance, select **More** > **Instance Status** > **Shut down**.
![Shut down](https://main.qcloudimg.com/raw/cc0bb1c82b96cca94cb7c1c011b664a7.png)
  - **Tab view**: In the tab of the instance, click **Shutdown** on the top right.
![Shut down](https://qcloudimg.tencent-cloud.cn/raw/bd0d10a80c75a653adee564105a9820b.png)


#### Creating custom image[](id:createOS)
1. On the instance management page, proceed according to the actually used view mode:
   - **List view**: Select **More** > **Create Image**.
   ![](https://main.qcloudimg.com/raw/8e3fc28e1a0b1e9e337ff72e34a9fd01.png)
   - **Tab view**: Select **More Actions** > **Create Image** in the top-right corner.
   ![](https://qcloudimg.tencent-cloud.cn/raw/27d7f6f19bc115c501bb1157ebe37cab.png)
2. In the **Create custom image** pop-up window, complete the configuration.
  - **Image name** and **Description**: Custom name and description.
  - **Create only system disk image**: This option only appears when there are data disks attached to the instance.
     - If it’s checked, only a system disk image of the instance will be created.
     - If it’s unchecked, a data disk snapshot will be created at the same time.
3. Click **Create image**.
You can click **[Image](https://console.cloud.tencent.com/cvm/image)** on the left sidebar to view the creation progress on the **Image** page.


#### Using custom image to create instance (optional)
Select the image you created in the image list, and click **Create Instance** on the right side to purchase a server with the same configuration as the image.
![](https://main.qcloudimg.com/raw/2d64df77d16b3c26d275770e03a1caf1.png)

:::
::: API
You can use the `CreateImage` API to create a custom image. For more information, see [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276).
:::
</dx-tabs>

## Best Practices

### Migrating data on data disk

If you need to keep the data on the data disk of the original instance when launching a new instance, you can first take a [snapshot](https://intl.cloud.tencent.com/document/product/362/31638) of the data disk, and then use this data disk snapshot to create a new CBS data disk.
For more information, see [Creating Cloud Disks Using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757).
