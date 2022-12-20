Live transcoding (including video transcoding and audio transcoding) refers to the process where the original stream pushed from the live streaming site is converted into streams of different codecs, resolutions, and bitrates in the cloud before being pushed to viewers. This meets playback needs in varying network environments on different devices. This document describes how to create, bind, unbind, modify, and delete a transcoding template via the CSS console.

**You can create a transcoding template in two ways:**

- Create a transcoding template in the CSS console. For detailed directions, see [Creating a standard transcoding template](#C_trans), [Creating a TSC transcoding template](#C_topspeed), and [Creating an audio-only transcoding template](#C_audio).
- Create a transcoding template for live channels using an API. For the API parameters and examples, see [CreateLiveTranscodeTemplate](https://intl.cloud.tencent.com/document/product/267/30790).


## Notes
- CSS supports standard transcoding, Top Speed Codec (TSC) transcoding, and audio-only transcoding. Please read the billing overview before using the service.
   - [Live Transcoding > Standard Transcoding](https://intl.cloud.tencent.com/document/product/267/39604)
   - [Live Transcoding > TSC Transcoding](https://intl.cloud.tencent.com/document/product/267/39604)
- Compared with **standard transcoding**, **TSC transcoding** provides higher video quality at lower bitrate. Leveraging technologies including intelligent scene recognition, dynamic encoding, and CTU/line/frame-level bitrate control, TSC transcoding allows you to provide higher-definition streaming services at lower bitrates (50% lower on average). It is widely used for game streaming, showroom streaming, and event streaming.
- After creating a template, you can bind it with a playback domain name. The binding takes effect in 5-10 minutes.
- You can append the name of a transcoding template to the `StreamName` of a live stream to generate a URL of the transcoded stream. If you have specified the height and width or short and long sides of the transcoded stream, keep the original resolution as close to the values set as possible to prevent image distortion.
- On the **Live Transcoding** page of the console, you can view the domain a template is bound to, as well as finer-granularity bindings performed via APIs. You can also [unbind](#untie) a template here.
- You can bind one playback domain name with **multiple transcoding templates**, or bind one transcoding template with **multiple playback domain names**.
- You can create up to **50** transcoding templates.

[](id:create)
## Creating a Transcoding Template
[](id:C_trans)
### Creating a standard transcoding template

1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Transcoding Template**, select **Standard Transcoding** for transcoding type, and complete the following configuration:
  - Basic configuration: Template name, video bitrate, video resolution and more. For details, see [Basic Configuration for Standard Transcoding](#C_trans_normal).
  - Advanced configuration (optional): Click **Advanced Configuration** to show advanced settings. For details, see [Advanced Configuration for Standard Transcoding](#C_trans_high).
3. Click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/a687312d5f0cb459a9684fe9f2de6459.png)

<table id="C_trans_normal">
<tr><th width="20%">Basic Configuration for Standard Transcoding</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>The transcoding type, which can be <b>standard transcoding</b>, TSC transcoding, or audio-only transcoding.</td>
</tr><tr>
<td>Template Name</td>
<td>Yes</td>
<td>The template name, which must be 1-10 characters long and can contain letters only or a combination of digits and letters.</td>
</tr><tr>
<td>Template Description</td>
<td>No</td>
<td>The template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Recommended Parameter</td>
<td>No</td>
<td>You can choose <b>Smooth, SD, or HD</b>. After you select a value, the system will automatically enter the recommended video bitrate and height, which can be modified.</td>
</tr><tr>
<td>Video Bitrate<br>(in Kbps)</td>
<td>Yes</td>
<td>The average output bitrate. Value range: 100-8000.<ul style="margin:0">
  <li>If you enter a value not larger than 1,000, it must be a multiple of 100.</li>
  <li>If you enter a value larger than 1,000, it must be a multiple of 500.</li></ul>
</td>
</tr><tr>
<td>Video Resolution (px)</td>
<td>Yes</td>
<td><li>You can set either the <b>height</b> (default) or <b>short side</b> of the output video.</li><li>Value range: 0-3000. The value must be a multiple of 2. The other side will be auto-scaled.</li></td>
</tr></table>


<table id="C_trans_high">
<tr><th width="20%">Advanced Configuration for Standard Transcoding</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Codec</td>
<td>No</td>
<td>The original codec is used by default. You can choose H.264 or H.265.</td>
</tr><tr>
<td>Video Frame Rate (fps)</td>
<td>No</td>
<td>Value range: 0-60. If this parameter is left empty, `0` will be used, which means to use the original frame rate.</td>
</tr><tr>
<td>GOP<br>(in seconds)</td>
<td>No</td>
<td>Value range: 2-6. The larger the GOP, the higher the delay. If this parameter is left empty, the default value will be used.</td>
</tr><tr>
<td>Parameter Limit</td>
<td>No</td>
<td>Disabled by default and can be enabled manually.<br>After a limit is enabled, the original value of the input stream will be used if you enter a value larger than the original. This can avoid video quality issues caused by using high video quality settings to transcode videos of low quality.</td>
</tr></table>


   

[](id:C_topspeed)

### Creating a TSC transcoding template
1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Transcoding Template**, select **Top Speed Codec Transcoding** for transcoding type, and complete the following configuration:
  - Basic configuration: Template name, video bitrate, video resolution, etc. For details, see [Basic Configuration for TSC Transcoding](#C_topspeed_normal).
  - Advanced configuration (optional): Click **Advanced Configuration** to show advanced settings. For details, see [Advanced Configuration for TSC Transcoding](#C_topspeed_high).
3. Click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/54a0334f1d24f7e0acb4e4f923b27d23.png)

<table  id="C_topspeed_normal">
<tr><th width="20%">Basic Configuration for TSC Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>The transcoding type, which can be standard transcoding, <b>TSC transcoding</b>, or audio-only transcoding.</td>
</tr><tr>
<td>Template Name</td>
<td>Yes</td>
<td>The template name, which must be 2-10 characters long and can contain letters only or a combination of digits and letters.</td>
</tr><tr>
<td>Template Description</td>
<td>No</td>
<td>The template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Recommended Parameter</td>
<td>No</td>
<td>You can choose <b>Smooth, SD, or HD</b>. After you select a value, the system will automatically enter the recommended video bitrate and height, which can be modified.</td>
</tr><tr>
<td>Video Bitrate<br>(in Kbps)</td>
<td>Yes</td>
<td>The average output bitrate. Value range: 100-8000. <li>If you enter a value not larger than 1,000, it must be a multiple of 100.</li><li>If you enter a value larger than 1,000, it must be a multiple of 500.</li></td>
</tr><tr>
<td>Video Resolution (px)</td>
<td>Yes</td>
<td><li>You can set either the <b>height</b> (default) or <b>short side</b> of the output video.</li><li>Value range: 0-3000. The value must be a multiple of 2. The other side will be auto-scaled.</li></td>
</tr>
</table>

<table  id="C_topspeed_high">
<tr><th width="20%">Advanced Configuration for TSC Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Codec</td>
<td>No</td>
<td>The original codec is used by default. You can choose H.264 or H.265.</td>
</tr><tr>
<td>Video Frame Rate (fps)</td>
<td>No</td>
<td>Value range: 0-60. If this parameter is left empty, `0` will be used.</td>
</tr><tr>
<td>GOP<br>(in seconds)</td>
<td>No</td>
<td>Value range: 2-6. The larger the GOP, the higher the delay. If this parameter is left empty, the default value will be used.</td>
</tr><tr>
<td>Parameter Limit</td>
<td>No</td>
<td><li/>Disabled by default and can be enabled manually.<li/>After a limit is enabled, the original value of the input stream will be used if you enter a value larger than the original. This can avoid video quality issues caused by using high video quality settings to transcode videos of low quality.</td>
</tr></table>

[](id:C_audio)
### Creating an audio-only transcoding template

1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Transcoding Template**, select **Audio-only Transcoding** for transcoding type, complete the [configuration](#C_audio_normal), and then click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/3cfe98bcc9f21c445e5db220a9ea0673.png)

<table id="C_audio_normal">
<tr><th width="20%">Basic Configuration for Audio-only Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>The transcoding type, which can be standard transcoding, TSC transcoding, or <strong>audio-only transcoding</strong>.</td>
</tr>
<tr>
<td>Template Name</td>
<td>Yes</td>
<td>The template name, which must be 1-10 characters long and can contain letters only or a combination of digits and letters.</td>
</tr>
<tr>
<td>Template Description</td>
<td>No</td>
<td>The template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr>
<tr>
<td>Audio Bitrate (Kbps)</td>
<td>Yes</td>
<td>You can <b>use the original audio bitrate</b> or <b>set a custom bitrate</b>. Value range: 101-500.</td>
</tr>
</tbody></table>


[](id:related)
## Binding a Domain Name
1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Bind a domain name in either of two ways:
  - **Bind a domain name to an existing transcoding template**: Click **Bind Domain Name** in the top left.
    ![](https://qcloudimg.tencent-cloud.cn/raw/7bcbc02fbc3ec3390ed16475b62482c5.png)
  - **Bind a domain name after creating a transcoding template**: After [creating a template](#create), click **Bind Domain Name** in the pop-up window.
    ![](https://qcloudimg.tencent-cloud.cn/raw/2927d94d3e07f7344b6d740593265a0b.png)
3. Select a transcoding template and a playback domain name in the domain name binding window and then click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/1dc995d90d354e72613c699d59836f05.png)
>? You can click **Add** to bind multiple playback domain names to a template.



[](id:untie)
## Unbinding a Domain Name
1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select a template, find the target domain name, and click **Unbind**.
![](https://main.qcloudimg.com/raw/59ecf14bea1e5b3ffa7b1fe6da0d565b.png)
3. In the pop-up window, click **Confirm**.
![](https://main.qcloudimg.com/raw/e335a8c597413b90dfabda9a1f7f3150.png)



[](id:modify)
## Modifying a Template
1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select the target transcoding template and click **Edit** on the right to modify it.
3. After modification, click **Save**.
![](https://main.qcloudimg.com/raw/202923ad5334c6ee3e5a879042aa0d5c.png)



[](id:delect)
## Deleting a Template
>! If the template has been bound with a domain name, you need to [unbind](#untie) it before deleting the template. 

1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select a template which is not bound with any playback domain name, and click **Delete**.
![](https://main.qcloudimg.com/raw/c3109628fcb4a5a4fabce8ad58c03db5.png)
3. In the pop-up window, click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/0e27dc5c0ebfc2915161894c3d6a337c.png)




## See Also
For more information about **binding** and **unbinding** domain names, see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062).


