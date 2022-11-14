## Overview

### Common Steps
**Image replication** includes two features: **Custom images - cross-region replication** and **Shared images - intra-region replication**.

| Image replication | Strengths | Description |
|---------|---------|---------|
| **Custom images - cross-region replication** | It helps users deploy the same CVM instance **across regions**quickly. | You can use this feature to copy custom images across regions, and then create a CVM by copying the images in the new region. |
| **Shared images - intra-region replication** | It helps users copy the shared images to use them as custom images. | The copied custom images have features like other custom images. |


### Notes
- Custom images only support cross-region replication, and shared images only support intra-region replication.
- Image replication allows you to copy images in or outside China. If you need to copy images from China to other countries or vice versa, please contact after-sale service.
- The feature of image replication is currently free of charge, but you need to pay for snapshot service for retaining the copied custom images.
- Image replication takes 10 to 30 minutes.

## Methods
### Custom images - cross-region replication
<dx-tabs>
::: Copy images via console
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. In the left sidebar, click **[Images](https://console.cloud.tencent.com/cvm/image)** to enter the image management page.
3. Select the region where the original image you want to copy resides, and click the **Custom image** tab.
For example, select Guangzhou region.
![](https://qcloudimg.tencent-cloud.cn/raw/227e952cb09a5b2cedc61f12b6ccb469.png)
4. Find the instance whose image needs to be copied, click **More** > **Cross-region replication**.
5. In the pop-up window, select the regions where the image will be copied to and click **OK**.
After the copying is completed, the image list in the destination regions will display images with the same name and different IDs.
6. Switch to a destination region. Select the successfully copied image in the image list under the region, and click **Create instance** to create the same CVM instance.
:::
::: Copy images via API
You can use the `SyncImages` API to copy an image. For more information, see [SyncImages](https://intl.cloud.tencent.com/document/product/213/33267).
:::
</dx-tabs>


### Shared images - intra-region replication
<dx-tabs>
::: Copy images via console
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. In the left sidebar, click **[Images](https://console.cloud.tencent.com/cvm/image)** to enter the image management page.
3. Select the region where the original image you want to copy resides, and click the **Shared image** tab.
For example, select Shenzhen region.
![](https://qcloudimg.tencent-cloud.cn/raw/27b6a301053adc319789ecaeffde8652.png)
4. Find the instance whose image needs to be copied, click **More** > **Intra-region replication**.
5. In the pop-up window, select the regions where the image will be copied to and click **OK**.
After the copying is completed, the image list in the destination regions will display images with the same name and different IDs.
6. Switch to the “Custom image” tab. Select the successfully copied image, and click **Create instance** to create the same CVM instance. The copied image has features like other custom images.
:::
::: Copy images via API
You can use the `SyncImages` API to copy an image. For more information, see [SyncImages](https://intl.cloud.tencent.com/document/product/213/33267).
:::
</dx-tabs>
