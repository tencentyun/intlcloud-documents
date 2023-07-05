## Scenario

This document describes how to delete custom images.

## Notes
Before deleting custom images, please note the following items:
 - After a custom image is deleted, it can no longer be used to start a new CVM instance, but will not affect instances that have already been started. If you want to delete all instances started from this image, see [Reclaiming Instances](https://intl.cloud.tencent.com/document/product/213/4931) or [Terminate Instances](https://intl.cloud.tencent.com/document/product/213/4930).
 - A custom image that has been shared with others cannot be deleted. To delete it, you need to cancel image sharing first. For more information, see [Cancel Image Sharing](https://intl.cloud.tencent.com/document/product/213/7148).
 - You can only delete the custom image, not common image or shared image.

## Directions
<dx-tabs>
::: Delete\simages\sthrough\sthe\sconsole
1. Log in to the CVM Console, on the left sidebar, click [**Images**](https://console.cloud.tencent.com/cvm/).
2. Select the **Custom Image** tab to enter the custom image management page.
3. Select the method to delete custom images based on actual needs.
 - **Deleting a single image**: locate the custom image to be deleted in the image list and click **More** > **Delete**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/1211de56434b4b6034dccb1ff9ce4aa1.png)
 - **Deleting multiple images**: select all custom images to be deleted in the image list and click **Delete** on the top.
 ![](https://qcloudimg.tencent-cloud.cn/raw/9f002d5cce1cfa2c94931ea3bca25ac2.png)
4. In the pop-up window, click **OK**.
If the deletion fails, possible reasons will be prompted.
:::
::: Delete\simages\sthrough\sAPI
You can use the DeleteImages API to delete images. For details, see [Delete Images](https://intl.cloud.tencent.com/document/product/213/33275).
:::
</dx-tabs>
