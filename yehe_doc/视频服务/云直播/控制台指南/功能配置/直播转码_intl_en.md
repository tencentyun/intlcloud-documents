Live transcoding (including video transcoding and audio transcoding) refers to the process where the original stream pushed from the live streaming site is converted into streams of different codecs, resolutions, and bitrates in the cloud before being pushed to viewers. This meets playback needs in varying network environments on different devices. This document describes how to create, bind, unbind, modify, and delete a transcoding template via the CSS Console.

**You can create a transcoding template in two ways:**

- Create a transcoding template in the CSS console. For detailed directions, please see [Creating standard transcoding template](#C_trans), [Creating top speed codec transcoding template](#C_topspeed), and [Creating audio-only transcoding template](#C_audio).
- Create a transcoding template for live channels with APIs. For specific parameters and samples, please see [CreateLiveTranscodeTemplate](https://intl.cloud.tencent.com/document/product/267/30790).


## Notes
- CSS supports standard transcoding, top speed codec transcoding, and audio-only transcoding. Please read the billing overview before using the service.
   - Standard transcoding: [standard transcoding pay-as-you-go billing mode](https://intl.cloud.tencent.com/document/product/267/39604#n_trans).
   - Top speed codec transcoding: [top speed codec transcoding pay-as-you-go billing mode](https://intl.cloud.tencent.com/document/product/267/39604#s_trans).
- Compared with **standard transcoding**, **top speed codec transcoding** provides higher video quality at lower bitrate. Leveraging technologies including intelligent scene recognition, dynamic encoding, and CTU/line/frame-level bitrate control, top speed codec transcoding allows you to provide higher-definition streaming services at lower bitrates (30% lower on average). It is widely used for the streaming of games, shows, and other events.
- After creating a template, you can bind it with a playback domain name. The binding takes effect in 5-10 minutes.
- You can append the name of a transcoding template to the `StreamName` of a live stream to generate a URL of the transcoded stream. If you have specified the height and width or short and long sides of the transcoded stream, keep the original resolution as close to the values set as possible to prevent image distortion.
- After a transcoding template has been bound, the configured settings will be displayed on the template. You can also use this template to view and [unbind](#untie) granular settings created via APIs.
- You can bind one playback domain name with **multiple transcoding templates**, or bind one transcoding template with **multiple playback domain names**.
- You can create up to **50** transcoding templates.

[](id:create)
## Creating Transcoding Template
[](id:C_trans)
### Creating standard transcoding template

1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Transcoding Template**, select **Standard Transcoding** for transcoding type, and complete the following configuration:
  - Basic configuration: template name, video bitrate, video resolution and more. For details, see [Basic Configuration for Standard Transcoding](#C_trans_normal).
  - Advanced configuration (optional): click **Advanced Configuration** to show advanced settings. For details, see [Advanced Configuration for Standard Transcoding](#C_trans_high).
3. Click **Save**.

![](https://main.qcloudimg.com/raw/cde1db91ea2796656a0297889e918daa.png)

<table id="C_trans_normal">
<tr><th width="20%">Basic Configuration for Standard Transcoding</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>Transcoding type, which can be <b>standard transcoding</b>, top speed codec transcoding, or audio-only transcoding.</td>
</tr><tr>
<td>Template Name</td>
<td>Yes</td>
<td>Live transcoding template name, which must be 1-10 characters long and can contain letters only or a combination of digits and letters.</td>
</tr><tr>
<td>Template Description</td>
<td>No</td>
<td>Live transcoding template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Recommended Parameter</td>
<td>No</td>
<td>You can choose <b>Smooth, SD, or HD</b>. After you select a value, the system will automatically enter the recommended video bitrate and height, which can be modified.</td>
</tr><tr>
<td>Video Bitrate<br>(in Kbps)</td>
<td>Yes</td>
<td>Average output bitrate. Value range: 100-8,000 Kbps.<ul style="margin:0">
  <li>A value below 1,000 must be a multiple of 100.</li>
  <li>A value above 1,000 must be a multiple of 500.</li></ul>
</td>
</tr><tr>
<td>Video Resolution</td>
<td>Yes</td>
<td>Default: **Set the height**.<li>The value entered will be the height of the transcoded video. You can also select **Set the short side length**, and the value entered will be the short side of the transcoded video. <li>Value range: 0-3000 px. The value must be a multiple of 2. The other side will be auto-scaled.</td>
</tr></table>


<table id="C_trans_high">
<tr><th width="20%">Advanced Configuration for Standard Transcoding</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Codec</td>
<td>No</td>
<td>Default setting: original bitrate. You can also select H.264 or H.265.</td>
</tr><tr>
<td>Video Frame Rate</td>
<td>No</td>
<td>Value range: 0-60 fps. If this parameter is left empty, `0` will be used.</td>
</tr><tr>
<td>GOP<br>(in seconds)</td>
<td>No</td>
<td>Value range: 2-6. The larger the GOP, the higher the delay. If this parameter is left empty, the default value will be used.</td>
</tr><tr>
<td>Parameter Limit</td>
<td>No</td>
<td>Disabled by default and can be enabled manually.<br>After this feature is enabled, the original parameter of the input stream will be used for the output stream if you enter a value higher than the original parameter. This prevents image quality issues where a low resolution video stream is played back in a high resolution.</td>
</tr></table>


   

[](id:C_topspeed)

### Creating top speed codec transcoding template
1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Transcoding Template**, select **Top Speed Codec Transcoding** for transcoding type, and complete the following configuration:
  - Basic configuration: template name, video bitrate, video resolution and more. For details, see [Basic Configuration for Top Speed Codec Transcoding](#C_topspeed_normal).
  - Advanced configuration (optional): click **Advanced Configuration** to show advanced settings. For details, see [Advanced Configuration for Top Speed Codec Transcoding](#C_topspeed_high).
3. Click **Save**.

![](https://main.qcloudimg.com/raw/68e80755dce7d3fa52210d7237f89418.png)

<table  id="C_topspeed_normal">
<tr><th width="20%">Basic Configuration for Top Speed Codec Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>Transcoding type, which can be standard transcoding, <b>top speed codec transcoding</b>, or audio-only transcoding.</td>
</tr><tr>
<td>Template Name</td>
<td>Yes</td>
<td>Live transcoding template name, which must be 3-10 characters long and can contain letters only or a combination of digits and letters.</td>
</tr><tr>
<td>Template Description</td>
<td>No</td>
<td>Live transcoding template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Recommended Parameter</td>
<td>No</td>
<td>You can choose <b>Smooth, SD, or HD</b>. After you select a value, the system will automatically enter the recommended video bitrate and height, which can be modified.</td>
</tr><tr>
<td>Video Bitrate<br>(in Kbps)</td>
<td>Yes</td>
<td>Average output bitrate. Value range: 100-8,000 Kbps. <li>A value below 1,000 Kbps must be a multiple of 100.</li><li>A value above 1,000 Kbps must be a multiple of 500.</li></td>
</tr><tr>
<td>Video Resolution</td>
<td>Yes</td>
<td>Default: **Set the height**.<li>The value entered will be the height of the transcoded video. You can also select **Set the short side length**, and the value entered will be the short side of the transcoded video.</li><<li>Value range: 0-3000 px. The value must be a multiple of 2. The other side will be auto-scaled.</td>
</tr>
</table>

<table  id="C_topspeed_high">
<tr><th width="20%">Advanced Configuration for Top Speed Codec Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Codec</td>
<td>No</td>
<td>Default setting: original bitrate. You can also select H.264 or H.265.</td>
</tr><tr>
<td>Video Frame Rate</td>
<td>No</td>
<td>Value range: 0-60 fps. If this parameter is left empty, the default value 0 fps will be used.</td>
</tr><tr>
<td>GOP<br>(in seconds)</td>
<td>No</td>
<td>Value range: 2-6. The larger the GOP, the higher the delay. If this parameter is left empty, the default value will be used.</td>
</tr><tr>
<td>Parameter Limit</td>
<td>No</td>
<td>Disabled by default and can be enabled manually.<br>After this feature is enabled, the original parameter of the input stream will be used for the output stream if you enter a value higher than the original parameter. This prevents image quality issues where a low resolution video stream is played back in a high resolution.</td>
</tr></table>

[](id:C_audio)
### Creating audio-only transcoding template

1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Transcoding Template**, select **Audio-only Transcoding** for transcoding type, complete the [configuration](#C_audio_normal), and then click **Save**.

![](https://main.qcloudimg.com/raw/c12170c861b0ed188aed7047822902a6.png)

<table id="C_audio_normal">
<tr><th width="20%">Basic Configuration for Audio-only Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>Transcoding type, which can be standard transcoding, top speed codec transcoding, or <strong>audio-only transcoding</strong>.</td>
</tr><tr>
<td>Template Name</td>
<td>Yes</td>
<td>Live transcoding template name, which must be 3-10 characters long and can contain letters only or a combination of digits and letters.</td>
</tr><tr>
<td>Template Description</td>
<td>No</td>
<td>Live transcoding template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr>
</table>

[](id:related)
## Binding Domain Name
1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Enter the domain name binding page in either of the following ways:
  - **Bind a domain name to an existing transcoding template**: click **Bind Domain Name** in the top left
    ![](https://main.qcloudimg.com/raw/ffa3a7d7c8392dc0509bf679f8d56c14.png)
  - **Bind a domain name after creating a transcoding template**: after [creating a template](#create), click **Bind Domain Name** in the pop-up
    ![](https://main.qcloudimg.com/raw/82060d2edf81b37a0706cc11833c9d9a.png)
3. Select a transcoding template and a playback domain name in the domain name binding window and then click **Confirm**.
![](https://main.qcloudimg.com/raw/8d0f571fab2c3765e3cebe5f5a819720.png)

>? You can click **Add** to bind multiple playback domain names to a template.



[](id:untie)
## Unbinding Domain Name
1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select a template, find the target domain name, and click **Unbind**.
![](https://main.qcloudimg.com/raw/59ecf14bea1e5b3ffa7b1fe6da0d565b.png)
3. In the pop-up, click **Confirm**.
![](https://main.qcloudimg.com/raw/e335a8c597413b90dfabda9a1f7f3150.png)



[](id:modify)
## Modifying Template
1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select the target transcoding template and click **Edit** on the right to modify it.
3. After modification, click **Save**.

![](https://main.qcloudimg.com/raw/202923ad5334c6ee3e5a879042aa0d5c.png)



[](id:delect)
## Deleting Template
>!   If the template has been bound with a domain name, you need to [unbind](#untie) it before deleting the template. 

1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select a template which is not bound with any playback domain name, and click **Delete**.
![](https://main.qcloudimg.com/raw/c3109628fcb4a5a4fabce8ad58c03db5.png)
3. In the pop-up window, click **Confirm**.
![](https://main.qcloudimg.com/raw/af5f6c3cc83c8ed5b1f50d37a054ce1d.png)




## Related Operations
For more information about **binding** and **unbinding** a domain name with a transcoding template, see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062).


