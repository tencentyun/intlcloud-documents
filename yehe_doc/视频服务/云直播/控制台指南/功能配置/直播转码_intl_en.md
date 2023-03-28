Live transcoding (including video transcoding and audio transcoding) refers to the process where the original stream pushed from the live streaming site is converted into streams of different codecs, resolutions, and bitrates in the cloud before being pushed to viewers. This meets playback needs in varying network environments on different devices. This document describes how to create, bind, unbind, modify, and delete a transcoding template via the CSS console.

**You can create a transcoding template in two ways:**

- Create a transcoding template in the CSS console. For detailed directions, see [Creating a standard transcoding template](#C_trans), [Creating a TSC transcoding template](#C_topspeed), and [Creating an audio-only transcoding template](#C_audio).
- Create a transcoding template for live streams using an API. For the API parameters and examples, see [CreateLiveTranscodeTemplate](https://www.tencentcloud.com/document/product/267/30790).


## Must-Knows
- CSS supports standard transcoding, Top Speed Codec (TSC) transcoding, and audio-only transcoding. Please read the billing documents before using the services.
   - Standard transcoding: [Standard Transcoding Packages](https://www.tencentcloud.com/document/product/267/52220#standard_pag), [Standard Transcoding (pay-as-you-go)](https://intl.cloud.tencent.com/document/product/267/39604)
   - TSC transcoding: [TSC Transcoding Packages](https://www.tencentcloud.com/document/product/267/52220#topspeed_pag), [TSC Transcoding (pay-as-you-go)](https://intl.cloud.tencent.com/document/product/267/39604)
- Compared with **standard transcoding**, **TSC transcoding** provides higher video quality at lower bitrate. Leveraging technologies including intelligent scene recognition, dynamic encoding, and CTU/line/frame-level bitrate control, TSC transcoding allows you to provide higher-definition streaming services at lower bitrates (50% lower on average). It is widely used for game streaming, showroom streaming, and event streaming.
- After creating a template, you can bind it with a playback domain name. The binding takes effect in 5-10 minutes.
- After binding a template, you can add the template name (`_template name`) after `StreamName` in the original URL to generate a URL for the transcoding output. Note that the **template name** and **stream name** cannot have the same suffix. For example, if the template name is `hd`, and `StreamName` is `test_a1_hd`, the system will use `test_a1` as the stream name and `hd` as the transcoding template, and playback will fail.
- If you have specified the height and width or short and long sides of the transcoding output, to prevent image distortion, keep the resolution of published streams as close to the values set as possible.
- On the **Live Transcoding** page of the console, you can view the domain a template is bound to, as well as finer-granularity bindings performed via APIs. You can also [unbind](#untie) a template here.
- You can bind one playback domain name with **multiple transcoding templates**, or bind one transcoding template with **multiple playback domain names**.
- You can create up to **50** transcoding templates.

[](id:create)
## Creating a Transcoding Template
[](id:C_trans)
### Creating a standard transcoding template

1. Log in to the CSS console and select **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Template**, select **Standard Transcoding** for transcoding type, and complete the following configuration:
  - Basic configuration: Template name, video bitrate, video resolution and more. For details, see [Basic Configuration for Standard Transcoding](#C_trans_normal).
  - Advanced configuration (optional): Click **Advanced Configuration** to show advanced settings. For details, see [Advanced Configuration for Standard Transcoding](#C_trans_high).
3. Click **Save**.

<img src="https://qcloudimg.tencent-cloud.cn/raw/d67e6aa3cc7d5bc0ddfe6f47342b6a24.png" style="zoom:67%;" />

<table id="C_trans_normal">
<tr><th width="20%">Basic Configuration for Standard Transcoding</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Transcoding type</td>
<td>Yes</td>
<td>The transcoding type, which can be <b>standard transcoding</b>, TSC transcoding, or audio-only transcoding.</td>
</tr><tr>
<td>Template name</td>
<td>Yes</td>
<td>The template name, which must be 1-10 characters long and can contain letters only or a combination of digits and letters.</td>
</tr><tr>
<td>Template description</td>
<td>No</td>
<td>The template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Video quality</td>
<td>No</td>
<td>You can choose <b>Smooth, SD, or HD</b>. After you select a value, the system will automatically enter the recommended video bitrate and height, which can be modified.</td>
</tr><tr>
<td>Video bitrate<br>(in Kbps)</td>
<td>Yes</td>
<td>The average output bitrate. Value range: 101-8000.<ul style="margin:0">
  <li>If you enter a value not larger than 1,000, it must be a multiple of 100.</li>
  <li>If you enter a value larger than 1,000, it must be a multiple of 500.</li></ul>
</td>
</tr><tr>
<td>Video resolution (px)</td>
<td>Yes</td>
<td><li>You can set either the <b>height</b> (default) or <b>short side</b> of the output video.</li><li>Value range: 0-3000. The value must be a multiple of 2. The other side will be auto-scaled.</li></td>
</tr><tr>
<td>DRM encryption</td>
<td>No</td>
<td>To enable DRM encryption, you need to first configure DRM key information in "DRM Management". DRM schemes including Widevine, FairPlay, and NormalAES are supported for HLS playback. For FairPlay encryption, you need to upload the certificate you obtain from Apple to your player.</td>
</tr></table>



<table id="C_trans_high">
<tr><th width="20%">Advanced Configuration for Standard Transcoding</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Codec</td>
<td>No</td>
<td>The original codec is used by default. You can choose H.264, H.265, or AV1.</td>
</tr><tr>
<td>Video frame rate (fps)</td>
<td>No</td>
<td>Value range: 0-60. If this parameter is left empty, `0` (the original frame rate) will be used.</td>
</tr><tr>
<td>GOP<br>(seconds)</td>
<td>No</td>
<td>Value range: 2-6. The larger the GOP, the higher the delay. If this parameter is left empty, the default value will be used.</td>
</tr><tr>
<td>Parameter limit</td>
<td>No</td>
<td>Parameter limits are disabled by default.<br>After a limit is enabled, if you enter a value higher than the original, the original will be used. This can avoid video quality issues caused by using high video quality settings to transcode videos of low quality.</td>
</tr></table>

[](id:C_topspeed)

### Creating a TSC transcoding template
1. Log in to the CSS console and select **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode).
2. Click **Create Template**, select **Top Speed Codec Transcoding** for transcoding type, and complete the following configuration:
  - Basic configuration: Template name, video bitrate, video resolution, etc. For details, see [Basic Configuration for TSC Transcoding](#C_topspeed_normal).
  - Advanced configuration (optional): Click **Advanced Configuration** to show advanced settings. For details, see [Advanced Configuration for Top Speed Codec Transcoding](#C_topspeed_high).
3. Click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/54965fbb96dc3a1ac6c51793b579954a.png)

<table  id="C_topspeed_normal">
<tr><th width="20%">Basic Configuration for TSC Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>The transcoding type, which can be standard transcoding, <b>TSC transcoding</b>, or audio-only transcoding.</td>
</tr><tr>
<td>Template name</td>
<td>Yes</td>
<td>The template name, which must be 2-10 characters long and can contain letters only or a combination of digits and letters.</td>
</tr><tr>
<td>Template description</td>
<td>No</td>
<td>The template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Video quality</td>
<td>No</td>
<td>You can choose <b>Smooth, SD, or HD</b>. After you select a value, the system will automatically enter the recommended video bitrate and height, which can be modified.</td>
</tr><tr>
<td>Video bitrate<br>(in Kbps)</td>
<td>Yes</td>
<td>The average output bitrate. Value range: 101-8000. <li>If you enter a value not larger than 1,000, it must be a multiple of 100.</li><li>If you enter a value larger than 1,000, it must be a multiple of 500.</li></td>
</tr><tr>
<td>Video resolution (px)</td>
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
<td>Video frame rate (fps)</td>
<td>No</td>
<td>Value range: 0-60. If this parameter is left empty, `0` will be used.</td>
</tr><tr>
<td>GOP<br>(seconds)</td>
<td>No</td>
<td>Value range: 2-6. The larger the GOP, the higher the delay. If this parameter is left empty, the default value will be used.</td>
</tr><tr>
<td>Parameter limit</td>
<td>No</td>
<td><li/>Disabled by default and can be enabled manually.<li/>After a limit is enabled, the original value of the input stream will be used if you enter a value larger than the original. This can avoid video quality issues caused by using high video quality settings to transcode videos of low quality.</td>
</tr></table>

[](id:C_audio)
### Creating an audio-only transcoding template

1. Log in to the CSS console and select **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode).
2. Click **Create Template**, select **Audio-only Transcoding** for transcoding type, complete the [configuration](#C_audio_normal), and then click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/6e51f4ba0d495176203d2a65a4a4dc57.png)

<table id="C_audio_normal">
<tr><th width="20%">Basic Configuration for Audio-only Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Transcoding type</td>
<td>Yes</td>
<td>The transcoding type, which can be standard transcoding, TSC transcoding, or <strong>audio-only transcoding</strong>.</td>
</tr>
<tr>
<td>Template name</td>
<td>Yes</td>
<td>The template name, which must be 1-10 characters long and can contain letters only or a combination of digits and letters.</td>
</tr>
<tr>
<td>Template description</td>
<td>No</td>
<td>The template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr>
<tr>
<td>Audio bitrate (Kbps)</td>
<td>Yes</td>
<td>You can <b>use the original audio bitrate</b> or <b>set a custom bitrate</b>. Value range: 101-500.</td>
</tr>
</tr><tr><td>DRM encryption</td><td>No</td><td>To enable DRM encryption, you need to first configure DRM key information in "DRM Management". DRM schemes including Widevine, FairPlay, and NormalAES are supported for HLS playback. For FairPlay encryption, you need to upload the certificate you obtain from Apple to your player.</td>
</tbody></table>

[](id:related)
## Binding a Domain Name
1. Log in to the CSS console and select **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode).
2. Bind a domain name in either of two ways:
  - **Bind a domain to an existing template**: Click **Bind Domain Name** in the top left.
    ![](https://qcloudimg.tencent-cloud.cn/raw/6e7b5d21d7211b08993ccd648c08ea39.png)
  - **Bind a domain name after creating a transcoding template**: After [creating a template](#create), click **Bind Domain Name** in the pop-up window.
    ![](https://qcloudimg.tencent-cloud.cn/raw/e46853c98ef7a78b4758b5d516d2db22.png)
3. Select a transcoding template and a playback domain in the domain binding window and then click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/19098af218a1e131310677e3fa4b6cd7.png)
>? You can click **Add** to bind a template to multiple playback domains.

[](id:untie)
## Unbinding a Domain Name
1. Log in to the CSS console and select **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode).
2. Select the target template and click **Unbind**.
![](https://qcloudimg.tencent-cloud.cn/raw/06d982f8c5ce34375945196485dfee59.png)
3. In the pop-up window, click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/fcb7537e8ab238617920fd54347da6da.png)

[](id:modify)
## Modifying a Template
1. Log in to the CSS console and select **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode).
2. Select the target transcoding template and click **Edit** on the right to modify it.
3. After modification, click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/995e1529ba890505c2db7ecc0788fac4.png)

[](id:delect)
## Deleting a Template
>! If a template has been bound to domains, you need to [unbind](#untie) them before you can delete the template. 

1. Log in to the CSS console and select **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode).
2. Select the target template (make sure it’s not bound to a domain), and click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/201fbd96756e417eb01bc4c4162c3a3e.png)
3. In the pop-up window, click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/e9062327d9cae6164254af7454c878de.png)


## More
You can also **unbind** and **bind** domains and transcoding templates on the **Domain Management** page. For details, see [Template Configuration](https://intl.cloud.tencent.com/document/product/267/31062).
