This document describes how to create [watermark configuration](https://intl.cloud.tencent.com/document/product/267/31064) in the [LVB Console](https://console.cloud.tencent.com/live). After the configuration is successfully created, you need to associate it with the corresponding push domain name. The association will take effect in about 5–10 minutes. You can also add watermarks to live channels through APIs. 


## Creating Watermark Template
Log in to the LVB Console, select **Feature Template** > **[Watermark Configuration](https://console.cloud.tencent.com/live/config/watermark)** on the left sidebar, click **+**, and enter basic information of the watermark.
The display position of the watermark can be customized by dragging the watermark image or adjusting the directions of the X axis and Y axis.
![](https://main.qcloudimg.com/raw/573023a1d1d6fd921209799edbfa96e8.png)

> For optimal visual effects, the watermark should be a transparent image in .png format of less than 2 MB in size.

## Associating Domain Name
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, select a push address, and click **Manage** to enter the push domain name details page.
2. Select **Configure Template** and then select the configured watermark template in watermark configuration to specify it for the domain name.
![](https://main.qcloudimg.com/raw/637ec4e2692c9b1fdd06ccf336e439d8.png)
>
>- If you want to unbind the watermark configuration from the domain name, click **Edit** in **Configure Template**, deselect the corresponding template, and click **Save**.
>- The watermarking templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated the configuration with a specified stream through the watermark management API and want to disassociate them, you need to call the [DeleteLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30824) API.
