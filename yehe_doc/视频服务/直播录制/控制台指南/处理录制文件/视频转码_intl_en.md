After LVB recording is completed, you can process and distribute the recording files through VOD. Main media asset processing operations of VOD include video transcoding, video acceleration, video playback, etc., all of which can be initiated and executed through task flows.

This document describes how to implement the [video transcoding configuration](#deploy) and [custom transcoding template](#c_template) in the VOD console.

<span id="deploy"></span>
## Video Transcoding Configuration
1. Log in to the VOD console and click **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)** on the left sidebar on the **non-admin** page.
2. Select the video you want to process and click **Video Processing** to directly initiate a transcoding task.
   ![](https://main.qcloudimg.com/raw/eee6369c558d957e79b06faa00cfba7c.png)
<table>
<tr><th >Processing Type</th><th  width="45%">Transcoding Template</th><th width="35%">Watermark Template</th><th width="14%">Video Cover</th></tr>
<tr>
<td>Transcoding</td>
<td>The following options are available: <ul style="margin:0">
	<li>Click **Transcoding Template**: select one or multiple transcoding templates you created in <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings</a>.</li>
	<li>Click **Common Template**: the common transcoding template you set will be automatically selected, and you can delete it by clicking **Delete** in the **Operation** column.</li>
</td>
<td rowspan="2">The following options are available: <ul style="margin:0">
	<li>Click **No Watermark**. </li>
	<li>Click **Default Watermark**: the default watermark template you set will be automatically selected.</li>
	<li>Click **Select Watermark**: select a watermark template you created in <a href="https://intl.cloud.tencent.com/document/product/266/14059#.E6.B0.B4.E5.8D.B0.E6.A8.A1.E6.9D.BF">Template Settings</a>.</li>
</td>
<td rowspan="2">Click to choose whether to use the first frame as the cover.</td>
</tr><tr>
<td>Adaptive bitrate streaming</td>
<td>Click the drop-down list and select an adaptive bitrate streaming template you created in <a href="https://intl.cloud.tencent.com/document/product/266/14059#.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF">Template Settings</a>.</td>
</tr>
</tbody></table>
3. Click **OK** to save the change and directly initiate the transcoding task.

<span id="c_template"></span>
## Custom Transcoding Template
The VOD console has built-in templates, including **Video Transcoding Template**, **TESHD Template**, **Audio Transcoding Template**, and **Adaptive Bitrate Streaming Template**. You can also create custom templates and use them to configure video transcoding.

Take the creation of a "video transcoding template" as an example:

1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and select **Video Processing Settings** > **Template Settings** on the left sidebar on the **non-admin** page.
2. Select **Video Transcoding Template** and click **Create Transcoding Template** to enter the template customization page.
3. Enter the configuration information according to the [video transcoding template configuration description](https://intl.cloud.tencent.com/document/product/266/14059) and click **Create**.

![](https://main.qcloudimg.com/raw/f2f716b669669bf447887f891de9bb71.png)

>?
>- The created template will be displayed in the template list. You can view, edit, or delete the template, or set it as a common template.
>- For more information on template configuration, please see [VOD - Transcoding Template](https://intl.cloud.tencent.com/document/product/266/14059).
