LVB transcoding (including video transcoding and audio transcoding) refers to the process where the original stream pushed from the live streaming site is converted into streams of different codecs, resolutions, and bitrates in the cloud before being pushed to viewers. This meets playback needs in varying network environments on different devices. This document describes how to create, modify, bind, unbind, and delete a transcoding template in the console.

**You can create a transcoding template in two ways:**

- Create a transcoding template in the LVB console. For detailed directions, please see [Creating standard transcoding template](#C_trans), [Creating top speed codec transcoding template](#C_topspeed), and [Creating pure audio transcoding template](#C_audio).
- Create a transcoding template for live channels with APIs. For specific parameters and samples, please see [CreateLiveTranscodeTemplate](https://intl.cloud.tencent.com/document/product/267/30790).


## Notes
- LVB supports standard transcoding, top speed codec transcoding, and pure audio transcoding. Please read the billing overview before using the service.
   - Standard transcoding: [standard transcoding pay-as-you-go billing mode](https://intl.cloud.tencent.com/document/product/267/2818#lvb-transcoding).
   - Top speed codec transcoding: [top speed codec transcoding pay-as-you-go billing mode](https://intl.cloud.tencent.com/document/product/267/2818#top-speed-codec-transcoding).
- Compared with **standard transcoding**, **top speed codec transcoding** provides higher image quality at a lower bitrate. Top speed codec transcoding comes with features including intelligent scene recognition, dynamic encoding, and three-level (CTU/line/frame) precise bitrate control model, enabling your live streaming platform to provide higher-definition streaming services at lower bitrates (30% less on average), which effectively reduces your bandwidth costs. This service is widely used in live games, live fashion shows, and other live events.
- After creating a template, you can bind it to a playback domain name. The binding will take effect in 5–10 minutes.
- After creating the template, you can add `_transcoding template name` after the `StreamName` of a live stream to generate a transcoding stream address. If values of the height and width or the short and long sides of the screen are entered, the resolution of the pushed video should follow the entered values as much as possible to avoid image distortion.
- After a transcoding template is bound, the configured settings will be displayed in the template. You can also use this template to view and [unbind](#untie) granular settings created through APIs.
- You can bind one playback domain name to **multiple transcoding templates** or bind one transcoding template to **multiple playback domain names**.

<span id="create"></span>
## Creating Transcoding Template
<span id="C_trans"></span>
### Creating standard transcoding template

1. Log in to the LVB console and select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Transcoding Template**, select **Standard Transcoding** as the transcoding type, and configure as follows.
  - Basic settings include template name, video bitrate, video resolution, and more. For more information, please see [Basic Configuration Description for Standard Transcoding](#C_trans_normal).
  - Advanced settings (optional): click **Advanced Configuration** to configure advanced settings. For more information, please see [Advanced Configuration Description for Standard Transcoding](#C_trans_high).
3. After completing the configuration, click **Save**.

![](https://main.qcloudimg.com/raw/cde1db91ea2796656a0297889e918daa.png)

<table id="C_trans_normal">
<tr><th width="20%">Basic Settings for Standard Transcoding</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>You can select <b>standard transcoding</b>, top speed codec transcoding, or pure audio transcoding.</td>
</tr><tr>
<td>Template Name</td>
<td>Yes</td>
<td>LVB transcoding template name, which can contain only letters and alphanumeric combinations. Please enter 1–10 characters.</td>
</tr><tr>
<td>Template Description</td>
<td>No</td>
<td>LVB transcoding template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Recommended Parameter</td>
<td>No</td>
<td>Three types of templates are supported: <b>LD, SD, and HD</b>. After you select a template, the system will automatically enter the recommended video bitrate and video height. You can also modify them manually.</td>
</tr><tr>
<td>Video Bitrate<br>(in Kbps)</td>
<td>Yes</td>
<td>Average output bitrate. Value range: 100–8000 Kbps.<ul style="margin:0">
  <li>A value below 1,000 Kbps must be a multiple of 100.</li>
  <li>A value above 1,000 Kbps must be a multiple of 500.</li></ul>
</td>
</tr><tr>
<td>Video resolution</td>
<td>Yes</td>
<td>Default setting: **Set by height**.<li>You should enter the height. You can also switch to **Set the short side length** and then enter the length of the short side of the screen. <li>Value range: 0–3000 px. The value should be a multiple of 2 and the other side of the screen will be scaled proportionally.</td>
</tr></table>


<table id="C_trans_high">
<tr><th width="20%">Advanced Settings for Standard Transcoding</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Codec</td>
<td>No</td>
<td>Default setting: original bitrate. You can also select H.264 or H.265 as the codec. </td>
</tr><tr>
<td>Video Frame Rate</td>
<td>No</td>
<td>Value range: 0–60 fps. If this parameter is left empty, the default value 0 fps will be used.</td>
</tr><tr>
<td>Keyframe Interval/GOP<br>(in seconds)</td>
<td>No</td>
<td>Value range: 2–6 seconds. The larger the GOP, the higher the delay. If this parameter is not set, the system default value will be used.</td>
</tr><tr>
<td>Parameter Limit</td>
<td>No</td>
<td>This is disabled by default and can be enabled manually.<br>After the parameter limit is enabled, the original parameter of the input live stream will be the output if the entered parameter is higher than the original parameter. This prevents image quality issues where a low resolution video stream is forced to play back in a higher resolution.</td>
</tr></table>


   

<span id="C_topspeed"></span>

### Creating top speed codec transcoding template
1. Log in to the LVB console and select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Transcoding Template**, select **Top Speed Codec Transcoding** as the transcoding type, and configure as follows.
  - Basic settings include template name, video bitrate, video resolution, and more. For more information, please see [Basic Configuration Description for Top Speed Codec Transcoding](#C_topspeed_normal).
  - Advanced settings (optional): click **Advanced Configuration** to configure advanced settings. For more information, please see [Advanced Configuration Description for Top Speed Codec Transcoding](#C_topspeed_high).
3. Click **Save**.

![](https://main.qcloudimg.com/raw/68e80755dce7d3fa52210d7237f89418.png)

<table  id="C_topspeed_normal">
<tr><th width="20%">Basic Settings for Top Speed Codec Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>You can select standard transcoding, <b>top speed codec transcoding</b>, or pure audio transcoding.</td>
</tr><tr>
<td>Template Name</td>
<td>Yes</td>
<td>LVB transcoding template name, which can contain only letters and alphanumeric combinations. Please enter 3–10 characters.</td>
</tr><tr>
<td>Template Description</td>
<td>No</td>
<td>LVB transcoding template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr><tr>
<td>Recommended Parameter</td>
<td>No</td>
<td>Three types of templates are supported: <b>LD, SD, and HD</b>. After you select a template, the system will automatically enter the recommended video bitrate and video height. You can also modify them manually.</td>
</tr><tr>
<td>Video Bitrate<br>(in Kbps)</td>
<td>Yes</td>
<td>Average output bitrate. Value range: 100–8000 Kbps. <li>A value below 1,000 Kbps must be a multiple of 100.</li><li>A value above 1,000 Kbps must be a multiple of 500.</li></td>
</tr><tr>
<td>Video Resolution</td>
<td>Yes</td>
<td>Default setting: **Set by height**.<li>You should enter the height. You can also switch to **Set the short side length** and then enter the length of the short side of the screen. </li><li>Value range: 0–3000 px. The value should be a multiple of 2 and the other side of the screen will be scaled proportionally.</li></td>
</tr>
</table>

<table  id="C_topspeed_high">
<tr><th width="20%">Advanced Settings for Top Speed Codec Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Codec</td>
<td>No</td>
<td>Default setting: original bitrate. You can also select H.264 or H.265 as the codec. </td>
</tr><tr>
<td>Video Frame Rate</td>
<td>No</td>
<td>Value range: 0–60 fps. If this parameter is left empty, the default value 0 fps will be used.</td>
</tr><tr>
<td>Keyframe Interval/GOP<br>(in seconds)</td>
<td>No</td>
<td>Value range: 2–6 seconds. The larger the GOP, the higher the delay. If this parameter is not set, the system default value will be used.</td>
</tr><tr>
<td>Parameter Limit</td>
<td>No</td>
<td>This is disabled by default and can be enabled manually.<br>After the parameter limit is enabled, the original parameter of the input live stream will be the output if the entered parameter is higher than the original parameter. This prevents image quality issues where a low resolution video stream is forced to play back in a higher resolution.</td>
</tr></table>

<span id="C_audio"></span>
### Creating pure audio transcoding template

1. Log in to the LVB console and select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **Create Transcoding Template**, select **Pure Audio Transcoding** as the transcoding type, configure [settings](#C_audio_normal), and then click **Save**.

![](https://main.qcloudimg.com/raw/c12170c861b0ed188aed7047822902a6.png)

<table id="C_audio_normal">
<tr><th width="20%">Basic Settings for Pure Audio Transcoding</th><th>Required</th><th>Description</th>
</tr><tr>
<td>Transcoding Type</td>
<td>Yes</td>
<td>You can select standard transcoding, top speed codec transcoding, or <strong>pure audio transcoding</strong>.</td>
</tr><tr>
<td>Template Name</td>
<td>Yes</td>
<td>LVB transcoding template name, which can contain only letters and alphanumeric combinations. Please enter 3–10 characters.</td>
</tr><tr>
<td>Template Description</td>
<td>No</td>
<td>LVB transcoding template description, which can contain only letters, digits, underscores (_), and hyphens (-).</td>
</tr>
</table>

<span id="related"></span>
## Binding Domain Name
1. Log in to the LVB console and select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Enter the domain name binding page in either of the following ways:
  - **Directly bind a domain name**: click **Bind Domain Name** in the top-left corner.
	![](https://main.qcloudimg.com/raw/ffa3a7d7c8392dc0509bf679f8d56c14.png)
  - **Bind a domain name after creating the transcoding template**: after the [template is created](#create), click **Bind Domain Name** in the pop-up.
	![](https://main.qcloudimg.com/raw/82060d2edf81b37a0706cc11833c9d9a.png)
3. Select a **transcoding template** and a **playback domain name** in the domain name binding window and then click **OK**.
![](https://main.qcloudimg.com/raw/8d0f571fab2c3765e3cebe5f5a819720.png)
>?You can click **Add** to bind multiple playback domain names to this template.



<span id="untie"></span>
## Unbinding
1. Log in to the LVB console and select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select domain names bound to the transcoding template and click **Unbind**.
![](https://main.qcloudimg.com/raw/59ecf14bea1e5b3ffa7b1fe6da0d565b.png)
3. Confirm whether to unbind the domain name and click **OK** to unbind it.
![](https://main.qcloudimg.com/raw/e335a8c597413b90dfabda9a1f7f3150.png)



<span id="modify"></span>
## Modifying Template
1. Log in to the LVB console and select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select the target transcoding template and click **Edit** on the right to modify the template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/202923ad5334c6ee3e5a879042aa0d5c.png)



<span id="delect"></span>
## Deleting Template
>!   If the template has been bound to a domain name, you need to [unbind](#untie) the template before deleting it. 

1. Log in to the LVB console and select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select a template which is not bound to any playback domain name and click **Delete**.
![](https://main.qcloudimg.com/raw/c3109628fcb4a5a4fabce8ad58c03db5.png)
3. Confirm whether to delete the selected transcoding template and click **OK** to delete it.
![](https://main.qcloudimg.com/raw/af5f6c3cc83c8ed5b1f50d37a054ce1d.png)




## Relevant Operations
For more information on **binding**/**unbinding** a domain name to/from a transcoding template, please see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062).














