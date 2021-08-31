## Overview

### Common Steps

**Cross-region replication** can help users deploy the same CVM **across regions** quickly. You can use this feature to copy images across regions, and then create a CVM by copying the images under the new region.

### Notes
 - The copied image must be a custom image. You must create a custom image first. For details, see [Create Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
 - Cross-region replication allows you to copy images in or outside China. If you need to copy images from China to other countries or vice versa, please contact after-sale service.
 - Cross-region replication of images is currently free of charge.
 - Cross-region replication currently does not support custom images larger than 50 GB.
 - Cross-region replication takes 10 to 30 minutes.
 
## Methods
<dx-tabs>
::: Copy\simages\svia\sconsole
 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
 2. In the left sidebar, click **[Images](https://console.cloud.tencent.com/cvm/image)** to enter the image management page.
 3. Select the region where the original image you want to copy resides, and click the **Custom Image** tab, as shown below:
 For example, select Guangzhou region.
 ![](https://main.qcloudimg.com/raw/f845cfeef21663bf8aaff58d5145f08c.png)
 4. Find the instance whose image needs to be copied, click **More** > **Cross-region replication**.
<dx-alert infotype="explain"> For batch operations, select all the images you want to copy and click **Cross-region replication**.
 </dx-alert>
 5. In the pop-up "Cross-region copying" window, select the regions where the image will be copied to and click **OK**.
After the copying is completed, the image list in the destination regions will display images with the same name and different IDs.
 6. Switch to a destination region. Select the successfully copied image in the image list under the region, and click **Create Instance** to create the same CVM instance.
:::
::: Copy\simages\svia\sAPI
You can also use SyncCvmImage API to copy images. 
:::
</dx-tabs>
