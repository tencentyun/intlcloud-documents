## Overview

### Features
**Image replication** offers two options, **Cross-region replication of custom images** and **Intra-region replication of shared images**.

| Type | Use Case | Description |
|---------|---------|---------|
| **Cross-region replication of custom image** | Deploy the same CVM instance **across regions** quickly. | Copy a custom image to another region, and use the created copy to create a CVM in the new region. |
| **Intra-region replication of shared image** | Make a copy of a shared image and use it as a custom image. | The created custom image is not subject to the limits of shared images. |


### Limits
- Custom images can be replicated across regions, and shared images support intra-region replication.
- **Regional limits**:
  - For now, image duplication is supported between two Chinese mainland regions, or two regions outside the Chinese mainland. If you want to copy an image from a Chinese mainland region to a region outside the Chinese mainland, and vice versa, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
- Image replication is free of charge. But you need to pay for snapshot service for store the copied custom images.
- Image replication takes 10 to 30 minutes.
- Cross-region replication is not available for full images.

## Methods
### Cross-region Replication of Custom Images
<dx-tabs>
::: Console
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. In the left sidebar, click **[Images](https://console.cloud.tencent.com/cvm/image)** to enter the image management page.
3. Select the region where the original image you want to copy resides, and click the **Custom image** tab.
For example, select Guangzhou region.
![](https://qcloudimg.tencent-cloud.cn/raw/227e952cb09a5b2cedc61f12b6ccb469.png)
4. Find the instance whose image needs to be copied, click **More** > **Cross-region replication**.
5. In the pop-up window, select the regions where the image will be copied to and click **OK**.
After the copying is completed, the image list in the destination regions will display images with the same name and different IDs.
6. Switch to a destination region. Select the copied image in the image list, and click **Create instance** to create the same CVM instance.
:::
::: API
You can use the `SyncImages` API to copy an image. For more information, see [SyncImages](https://www.tencentcloud.com/document/product/213/33267).
:::
</dx-tabs>


### Intra-region Replication of Shared Images
<dx-tabs>
::: Console
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. In the left sidebar, click **[Images](https://console.cloud.tencent.com/cvm/image)** to enter the image management page.
3. Select the region of the source image, and click the **Shared image** tab.
For example, select Guangzhou region.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ui6Q850_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230403153209.png)
4. Find the instance whose image needs to be copied, click **More** > **Intra-region replication**.
5. In the pop-up window, select the regions where the image will be copied to and click **OK**.
After the copying is completed, the image list in the destination regions will display images with the same name and different IDs.
6. Switch to the **Custom image** tab. Select the successfully copied image, and click **Create instance** to create the same CVM instance. The copied image has features like other custom images.
:::
::: API
You can use the `SyncImages` API to copy an image. For more information, see [SyncImages](https://www.tencentcloud.com/document/product/213/33267).
:::
</dx-tabs>
