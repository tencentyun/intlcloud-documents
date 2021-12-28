## Overview
In addition to public images, you can also use custom images to quickly create Tencent Cloud CVM instances with the same configurations. 


<dx-alert infotype="explain" title="">
Images use the CBS snapshot service for data storage:
 - A free tier of 50 GB is provided for the Chinese mainland regions. For more information, please see [Free Tier] (https://intl.cloud.Tencent.com/document/product/362/32415).
 - Upon the creation of a custom image, a snapshot will also be created by default, which may incur snapshot fees. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415).
</dx-alert>




## Notes

- Each region supports a maximum of 10 custom images.
- The following directories and files will be removed.
 - `/var/log/`  
 - `/root/.bash_history` and `/home/ubuntu/.bash_history` (for the Ubuntu operating system)
- When creating a custom image on a Linux instance, make sure `/etc/fstab` does not contain data disk configuration. Otherwise, instances created with this image cannot be launched normally. If the Linux instance that is used to create a custom image with a data disk attached, comment out or delete the relevant data disk configurations in `/etc/fstab`.
- The creation process takes ten minutes or more, which depends on the data size of the instance. Please prepare in advance to avoid business impacts.
- CPM 2.0 instances can not be used to create custom images. 
- To add a Windows instance to a domain and use a domain account, please execute Sysprep before creating a custom image to ensure that the SID is unique after the instance joins the domain. For more information, please see [Ensuring Unique SIDs for CVMs Using Sysprep] (https://intl.cloud.Tencent.com/document/product/213/35876).

## Directions
<dx-tabs>
::: Creating a custom image on the console

#### Shut down an instance (optional)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) and check whether the corresponding instance needs to be shut down.
<dx-alert infotype="notice" title="">
For CVMs created based on public images after July 2018, you can create images without shutting down the instance. For other CVMs, shut down the instance before creating a custom image to ensure that the image has the same environment deployment as the current instance.
</dx-alert>
  - If yes, proceed to the next step.
  - If no, proceed to [Create a custom image](#createOS) 
2. On the instance management page, locate the desired instance, and select **More** > **Instance Status** > **Shut down**, as shown in the following figure:
![Shut down](https://main.qcloudimg.com/raw/cc0bb1c82b96cca94cb7c1c011b664a7.png)


#### Create a custom image[](id:createOS)
1. Locate the desired instance, and select **More** > **Create Image**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8e3fc28e1a0b1e9e337ff72e34a9fd01.png)
2. In the pop-up **Create a custom image** window, complete the configuration as instructed below:
  - **Image name** and **Image description**: Custom name and description.
  - **Create a system disk image only**: If checked, only a system disk image of the instance will be created. Otherwise a snapshot of the data disk (if any) will be created at the same time.
3. Click **Create image**.
You can click **[Image](https://console.cloud.Tencent.com/CVM/image)** on the left sidebar to view the creation progress in the "Image" page.


#### Use the custom image to create an instance (optional)
Select the image you created in the image list, and click **Create Instance** on the right side to purchase the server with the same custom image, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2d64df77d16b3c26d275770e03a1caf1.png)

:::
::: Creating a custom image using \sAPI\s
You can use the `CreateImage` API to create a custom image. For more information, please see [CreateImage](https://intl.cloud.tencent.com/zh/document/product/213/33276).
:::
</dx-tabs>

## Best Practices

### Migrating the data on a data disk

If you need to keep the data on the data disk of the original instance when launching a new instance, you can first take a [snapshot](https://intl.cloud.tencent.com/document/product/362/31638) of the data disk, and then use this data disk snapshot to create a new CBS data disk.
For more information, please see [Creating Cloud Disks Using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757).
