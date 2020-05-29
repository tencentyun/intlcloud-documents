## Scenario

When creating an image, you can start an instance with a public image, connect it to the instance, and deploy your software environment. If the instance runs normally, you can create a new custom image based on this as needed, so you can use this image to start more new instances that have the same custom configurations as the original one.

> 
> - When you create a custom image, the system creates a related snapshot by default. You need to delete the associated images before deleting this snapshot. Because snapshot has been commercialized, retaining a custom image will incur a certain snapshot fee. For more information on snapshot billing, please see [Commercialization FAQs](https://intl.cloud.tencent.com/document/product/362/32413).
> - For CVMs created based on public images after July, 2018, creating images online is supported (i.e., you can create images without shutting down the instance).
> - For other CVMs, shut down the instance before creating a custom image to ensure that the image has the same deployment environment as the current instance.

## Notes

- Each region supports a maximum of 10 custom images.
- The following directories and files will be removed.
 - /var/log/  
 - /root/.bash_history、/home/ubuntu/.bash_history（Ubuntu system）
- When Linux instance creates a custom image, make sure /etc/fstab does not include data disk configuration. Otherwise, instances created with this image cannot be started normally. If the Linux instance that creates the custom image has a data disk mounted, note or delete the relevant data disk configurations in /etc/fstab.
- The creation process takes ten minutes or more, which depends on the data size of the instance. Please prepare in advance to avoid business impacts.

## Directions

### Create a custom image from an instance through the console

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm).
2. On the instance management page, select the instance for which images will be created, and click **More** > **Instance Status** > **Shutdown**.
3. After the instance is shut down, click **More**> **Create Image**.
4. In the pop-up "Create custom image" window, enter "Image Name" and "Description", and click **Create Image**.
> You can click <img src = "https://main.qcloudimg.com/raw/31b31c7b27848f0378932f17273feff3.png" style = "margin: 0;"> </ img> at the top right of the console to view the image creation progress.
>
5. After the image is created, click **[Images](https://console.cloud.tencent.com/cvm/image)** on the left sidebar to enter the image management page.
6. To purchase a server with the same image as the previous one, select the image you created in the image list, and click **Create Instance**.

### Create a custom image through API

You can use the CreateImage API to create a custom image. For more information, see [CreateImage API](https://intl.cloud.tencent.com/document/product/213/33276).

## Best Practices

### Migrate data on a data disk

If you need to keep the data on the data disk of the original instance when starting a new instance, you can first take a [snapshot](https://intl.cloud.tencent.com/document/product/362/31638) of the data disk, and then use this data disk snapshot to create a new CBS data disk.
For more information, see [Creating Cloud Disks Using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757).




