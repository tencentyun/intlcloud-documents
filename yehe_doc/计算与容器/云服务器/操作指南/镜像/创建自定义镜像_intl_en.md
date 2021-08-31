## Overview
In addition using Tencent Cloud public images, you can create custom images to quickly create Tencent Cloud CVM instances with the same configurations.
>?
>- Images use the CBS snapshot service for data storage. When you create a custom image, a snapshot will be automatically created and associated with the image. You will be charged for this snapshot. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415).
>- For CVMs that are created based on public images after July 2018 and use cloud disks as system disks, you can create images without shutting down the instance. For other CVMs, you need to shut down the instance before creating a custom image to ensure that the image has the same deployment environment as the current instance.


## Notes

- Each region supports a maximum of 10 custom images.
- The following directories and files will be removed.
 - `/var/log/`  
 - `/root/.bash_history` and `/home/ubuntu/.bash_history` (for the Ubuntu operating system)
- When creating a custom image on a Linux instance, make sure `/etc/fstab` does not contain data disk configuration. Otherwise, instances created with this image cannot be started normally. If the Linux instance that is used to create a custom image has a data disk mounted, comment out or delete the relevant data disk configurations in `/etc/fstab`.
- The creation process takes ten minutes or more, which depends on the data size of the instance. Please prepare in advance to avoid business impacts.

## Directions

### Creating a custom image from an instance through the console

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. On the instance management page, select the instance for which images will be created, and click **More** > **Instance Status** > **Shut down**, as shown below:
![Shutdown](https://main.qcloudimg.com/raw/cc0bb1c82b96cca94cb7c1c011b664a7.png)
3. After the instance is shut down, click **More**> **Create Image**, as shown below:
![](https://main.qcloudimg.com/raw/8e3fc28e1a0b1e9e337ff72e34a9fd01.png)
4. In the pop-up window, enter **Image Name** and **Description**, and click **Create Image**.
>? You can click <img src="https://main.qcloudimg.com/raw/31b31c7b27848f0378932f17273feff3.png" style="margin: 0;"></img> in the top-right corner to view the image creation progress.
>
5. After the image is created, click **[Images](https://console.cloud.tencent.com/cvm/image)** on the left sidebar to enter the image management page.
6. In the image list, select the image you have created, and click **Create an Instance** to purchase a server with the same configuations as the image.
![Custom Image](https://main.qcloudimg.com/raw/2d64df77d16b3c26d275770e03a1caf1.png)

### Creating a custom image through API

You can use the `CreateImage` API to create a custom image. For more information, see [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276).

## Best Practices

### Migrating the data on a data disk

If you need to keep the data on the data disk of the original instance when launching a new instance, you can first take a [snapshot](https://intl.cloud.tencent.com/document/product/362/31638) of the data disk, and then use this snapshot to create a new cloud data disk.
For more information, see [Creating Cloud Disks Using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757).