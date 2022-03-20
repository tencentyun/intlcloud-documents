CSS supports the watermark feature. It adds watermarks to the live streaming screen to protect video content from theft. This document describes how to create, modify, bind, unbind, and delete a watermark template in the console.
**You can create a watermark template in the following ways:**
- Create a watermark template in the CSS console. For more information, please see [Creating Watermark Template](#Watermark).
- Create a watermark template by calling an API. For more information, please see [AddLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30826).


## Notes
- After creating a template, you can bind it to a push domain name. The binding will take effect in 5–10 minutes.
- The watermark templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you bound the watermark configuration to a specified stream through the watermark management API and want to unbind them, you need to call the [DeleteLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30824) API.
- Binding, unbinding, and modifying a template affect only new live streams after the update but not ongoing ones. To make the new rule take effect for ongoing live streams, you need to interrupt them and push them again.


## Prerequisites

You have activated the CSS service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).

<span id="Watermark"></span>
## Creating Watermark Template

1. Log in to the CSS console and select **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark).
2. Click **Create Watermark Template**.
3. Enter a watermark name, which can contain up to 30 letters, digits, underscores (_), and hyphens (-).
4. Click **Select image** to upload an image as the watermark.
>! For optimal visual effects, the watermark should be a transparent image in .png format of less than 2 MB in size.
5. Specify the watermark location in the following ways:
	- Drag the watermark image in the configuration pane.
	- Adjust the coordinates of the X axis and Y axis.
6. Click **Save**.
![](https://main.qcloudimg.com/raw/944534ffbf8625b36a8883087bdf29f6.png)

<span id="conect"></span>
## Binding Domain Name

1. Log in to the CSS console and select **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark).
2. Enter the domain name binding page in either of the following ways:
	- **Directly bind a domain name**: click **Bind Domain Name** in the top-left corner.
	- **Bind a domain name after creating the watermark template**: after the [watermark template is created](#Watermark), click **Bind Domain Name** in the pop-up window.
3. Select a **watermark template** and a **push domain name** in the domain name binding window and then click **Confirm**.
>? You can click **Add** to bind multiple push domain names to this template.

<span id="untie"></span>
## Unbinding
1. Log in to the CSS console and select **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark).
2. Select domain names bound to the watermark template and click **Unbind**.
3. Confirm whether to unbind the domain name and click **Confirm** to unbind it.

<span id="change"></span>
## Modifying Template
1. Go to **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark).
2. Select the target watermark template and click **Edit** on the right to modify the template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/aceffbdffb9dd2b892500c97d8d1654f.png)

>? You can click **Preview** to view how the watermark will be displayed on the screen.

<span id="delete"></span>
## Deleting Template
If a template has been bound to a domain name, you need to unbind the template before deleting it. For detailed directions, please see [Unbinding](#untie).
1. Go to **Feature Configuration** > [**Live Watermarking**](https://console.cloud.tencent.com/live/config/watermark).
2. Find the target watermark template that you have created and click the deletion icon ![img](https://main.qcloudimg.com/raw/220ada95a4b631349543cc8cde96226e.png) at the top.
3. In the pop-up dialog box, click **Confirm** to confirm the deletion.

![](https://main.qcloudimg.com/raw/20b838fcbfbe5feffdd29f2d033d4f71.png)

## Relevant Operations
For more information on how to **bind/unbind** a **domain name** to/from a watermark template, please see [Watermark Configuration](https://intl.cloud.tencent.com/document/product/267/31064).
