LVB supports the watermark feature. It adds watermarks to the live streaming screen to protect video content from theft. This document describes how to create, modify, and delete a watermark template in the console.
**You can create a watermark template in the following ways:**
- Create a template in the LVB Console. For more information, please see [Creating a Watermark Template](#Watermark).
- Create a watermark template through APIs. For more information, please see [AddLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30826) API overview.



## Notes
- After a template has been created, you can associate it with a push domain name. The association will take effect in about 5–10 minutes.
- The watermark templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled for the time being. If you associated a template with a specified stream through the watermark management APIs and want to unassociate it, you need to call the [DeleteLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30824) API.

## Prerequisites

You have activated the LVB service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).

<span id="Watermark"></span>
## Creating a Watermark Template

1. Log in to the LVB Console, and select **Feature Configuration** > **[ LVB Watermark](https://console.cloud.tencent.com/live/config/watermark)**.
2. Click **+** to create a watermark template.
3. Enter a watermark name, which contains only letters, digits, underscores, and dashes, with a length of up to 30 characters.
4. Click **Select image** to upload an image as the watermark.
> For optimal visual effects, the watermark should be a transparent image in .png format of less than 2 MB in size.
5. Specify the watermark location in the following ways:
	- Drag the watermark image in the configuration pane.
	- Adjust the coordinates of the X axis and Y axis.
6. Click **Save**.
![](https://main.qcloudimg.com/raw/944534ffbf8625b36a8883087bdf29f6.png)



## Modifying a Template

1. Select **Feature Configuration** > **[LVB Watermark](https://console.cloud.tencent.com/live/config/watermark)**.
2. Find the desired watermark template that you have created, and click **Edit** on the right to modify template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/aceffbdffb9dd2b892500c97d8d1654f.png)

> You can click **Preview** to view how the watermark will be displayed on the screen.


## Deleting a Template
If the template is associated, you need to unassociate it before you can delete it. For more information, please see [Unassociating a Watermark Template](https://intl.cloud.tencent.com/document/product/267/31064).
1. Select **Feature Configuration** > **[LVB Watermark](https://console.cloud.tencent.com/live/config/watermark)**.
2. Find the desired watermark template that you have created, and click the deletion icon ![img](https://main.qcloudimg.com/raw/220ada95a4b631349543cc8cde96226e.png) at the top.
3. In the pop-up dialog box, click **OK** to confirm the deletion.

![](https://main.qcloudimg.com/raw/20b838fcbfbe5feffdd29f2d033d4f71.png)

## Associating the Template with a Domain Name

For more information, see [Associating a Watermark Template](https://intl.cloud.tencent.com/document/product/267/31064).
