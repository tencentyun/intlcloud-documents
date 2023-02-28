## Overview
Besides the public and Tencent Cloud office images provided by CVD, you can also create a custom image based on a CVD instance configured with the required office applications. Then, you can quickly create more CVD instances with the same configuration as the image in the CVD console.

## Notes
- CVD instances are pre-installed with `cloudbase-init` and `Tencent CVD Assistant` services. Make sure that you have enabled auto-start (enabled by default); otherwise, the created image will be unusable.
- You can create a custom image based on a pay-as-you-go instance when it is online but not when it is shut down. The creation takes about 30 minutes.
- Note that you can use an image containing a data disk to create but not reinstall a CVD instance.
- The data disk for image creation can be up to 1,000 GB.
- The custom image feature is currently in beta test, and each account can have up to five custom images. In the future, storage fees may be charged based on the size and number of images.
- Select `C:\Program Files` or `C:\Program Files (x86)` rather than `C:\Users\xxxxxx` for application installation; otherwise, the applications cannot be used by CVD instances created based on the image.

## Directions
1. On the **Desktop List** page, click **More** > **Create custom image**:
![](https://qcloudimg.tencent-cloud.cn/raw/5bcfc0f3fb5f89eabc4c6a1f4e2aa109.png)
2. In the **Create custom image** pop-up window, configure the following items:
 - **Image name** and **Description**: Enter the custom name and description.
 - **Includes data disk**: If your instance only has a system disk, this option will not appear. If your instance has a data disk, select it as needed.
    - If you select it, the created custom image will contain a data disk.
    - Otherwise, an image containing only the CVD instance's system disk will be created.

<img style="width:550px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/487c4a26e956e4b14b71631b98e994e5.png" />

3. Start creating the custom image. You can view the progress in [**Images**](https://console.cloud.tencent.com/cvd/image) > **Custom image** in the **CVD console**.
<img style="width:600px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/6afa50d0fafb55e82f9d74216ec3ce68.png" />

4. The custom image is created.
<img style="width:1100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/6c8a472c1a81ceea69a015ace2884edb.png" />

## Creating a CVD instance based on a custom image
When creating a CVD instance, select **Custom image** for **Image type** and select the target custom image from the drop-down list.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8674ae2ff352de26a5d35751e4ba9360.png" style="zoom:50%;" />

>?
>- The selected system disk space must be greater than or equal to that of the custom image.
>- If the custom image contains a data disk, the selected data disk space must be greater than or equal to that of the custom image.

## Deleting a custom image
A deleted custom image cannot be used for CVD instance creation. The deletion will not affect CVD instances that are already launched.
1. In the **CVD console**, select [**Images**](https://console.cloud.tencent.com/cvd/image) > **Custom image**, select the target image, and click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/f0c20da0e56e576a6400fc99b1dca4a6.png)
2. In the pop-up window, select **I understand that deleted images cannot be recovered** and click **Confirm**.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/cea7ef362d6b4bacd20d0a75ef407a4f.png" style="zoom:67%;" />