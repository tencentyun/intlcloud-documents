## Overview
Besides public images, you can also create custom images, with which you can create CVM instances with the same configurations.


<dx-alert infotype="explain" title="">
Images use the CBS snapshot service for data storage:
 - Upon the creation of a custom image, a snapshot is automatically created and associated with the image. As a result, retaining custom images incurs costs. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415).
</dx-alert>




## Note

- Each region supports a maximum of 10 custom images.
- When the Linux instance has a data disk attached, and you only create an image on the system disk, make sure `/etc/fstab` does not include data disk configuration. Otherwise, instances created with this image cannot be started normally.
- The creation process takes ten minutes or longer, which depends on the data size of the instance. Please prepare in advance to avoid business impacts.
- You can not create an image by using a CBM instance in the console or via API. You can use CVM to create them.
- If your Windows instance needs to enter a domain and uses a domain account, please execute Sysprep before creating a custom image to ensure that the SID is unique after the instance enters the domain. For more information, please see [Ensuring Unique SIDs for CVMs Using Sysprep](https://intl.cloud.Tencent.com/document/product/213/35876).

## Directions
<dx-tabs>
::: Console

#### Shut down an instance (optional)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) and check whether the corresponding instance needs to be shut down.
<dx-alert infotype="notice" title="">
For CVMs created based on public images after July 2018, you can create images without shutting down the instance. For other CVMs, shut down the instance before creating a custom image to ensure that the image has the same environment deployment as the current instance.
</dx-alert>
  - If the instance needs to be shut down, proceed to the next step.
  - If the instance doesn’t need to be shut down, please proceed to [Create a custom image](#createOS).
2. On the instance management page, proceed according to the actually used view mode:
  - **List view**: In the row of the target instance, select **More** > **Instance status** > **Shut down** on the right as shown below:
![](https://main.qcloudimg.com/raw/cc0bb1c82b96cca94cb7c1c011b664a7.png)
  - **Tab view**: Select **Shut down** on the instance details page.
![](https://qcloudimg.tencent-cloud.cn/raw/bd0d10a80c75a653adee564105a9820b.png)


#### Create a custom image [](id:createOS)
1. On the instance management page, proceed according to the actually used view mode:
   - **List view**: Select **More** > **Create image**.
   ![](https://main.qcloudimg.com/raw/8e3fc28e1a0b1e9e337ff72e34a9fd01.png)
   - **Tab view**: Select **More actions** > **Create image** in the top-right corner.
   ![](https://qcloudimg.tencent-cloud.cn/raw/27d7f6f19bc115c501bb1157ebe37cab.png)
2. In the **Create a custom image** popup window, complete the configuration.
  - **Image name** and **Image description**: Custom name and description.
  - **Tag**: You can add tags for the instance as needed, which are used to categorize, search for, and aggregate cloud resources. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/651/13334).
<dx-alert infotype="explain" title="">
To create custom images that include system disks and data disks, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category). 
</dx-alert>
3. Click **Create image**.
You can click **[Image](https://console.cloud.Tencent.com/CVM/image)** on the left sidebar to view the creation progress in the **Image** page.


#### Use the custom image to create an instance (optional)
Select the image you created in the image list, and click **Create instance** on the right side to purchase a server with the same configuration as the image, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2d64df77d16b3c26d275770e03a1caf1.png)

:::
::: API
You can use the `CreateImage` API to create a custom image. For more information, see [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276).
:::
</dx-tabs>

## Best Practices

### Migrating the data on a data disk

If you need to keep the data on the data disk of the original instance when launching a new instance, you can first take a [snapshot](https://intl.cloud.tencent.com/document/product/362/31638) of the data disk, and then use this data disk snapshot to create a new CBS data disk.
For more information, please see [Creating Cloud Disks Using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757).
