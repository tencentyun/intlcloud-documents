 LVB transcoding (including both video transcoding and audio transcoding) refers to the process where the original stream pushed out of the live streaming site is transcoded to streams of different codecs, resolutions, and bitrates in the cloud before being pushed to viewers. This helps meet the playback needs in different network environments on different devices. This document describes how to create, modify, and delete a transcoding template in the console.

**You can create a transcoding template in the following two methods:**

- Create a transcoding template in the LVB Console. For detailed directions, please see [Creating General Transcoding Template](#C_trans) and [Creating Top Speed Codec Template](#C_topspeed).
- Create a transcoding template for live channels with APIs. For specific parameters and samples, please see [CreateLiveTranscodeTemplate](https://intl.cloud.tencent.com/document/product/267/30790).


## Note:

- LVB supports general transcoding and top speed codec transcoding. Please read the relevant billing description before using them:
>? Compared with general transcoding, top speed codec transcoding has higher image quality at lower bitrate. Based on the technologies such as intelligent scenario recognition, dynamic encoding, and three-level (CTU/line/frame) precise bitrate control model, it enables your live streaming business to provide higher-definition streaming services at lower bitrates (reduced by over 30% on average), which effectively reduces your bandwidth costs.
- After a template is successfully created, it can be associated with a playback domain name. For more information, please see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062). The association will take effect in about 5–10 minutes.
- After you specify a transcoding template, the backend will generate different playback addresses with different bitrates for easier use. The original resolution of the stream will be as close as possible to the original aspect ratio of the video to avoid stretched and distorted display.
- The transcoding templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated the transcoding configuration with a specified stream through the transcoding management API and want to unassociate them, you need to call the [DeleteLiveTranscodeRule API](https://intl.cloud.tencent.com/document/product/267/30789).



<span id="C_trans"></span>
## Creating General Transcoding Template

1. Log in to the LVB Console, and select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **+**, select **General Transcoding** as the transcoding type, set the configuration items, and click **Save**.


![](https://main.qcloudimg.com/raw/d846e6c9038e539f3e7932d6657affaf.png)

<table>
   <thead><tr><th width="20%">General Transcoding Configuration Item</th><th width="80%">Description</th></tr></thead>
   <tbody><tr>
   <td>Applicable template</td>
	 <td>It supports four types of templates: <b>LD, SD, HD, and pure audio</b>. Default template: SD.<ul style="margin:0">
       <li>After you select a template, the system will automatically enter the recommended video bitrate and video height. You can also modify them manually.</li>
       <li>You do not need to enter the video bitrate and video height for a pure audio template.</li>
       </ul></td>
   </tr><tr>
   <td>Template name</td>
   <td>LVB transcoding template name, which can contain 1–10 letters and digits.</td>
   </tr> <tr>
   <td>Template description</td>
   <td>LVB transcoding template description, which can contain only letters, digits, underscores, and hyphens.</td>
   </tr><tr>
   <td>Video bitrate<br>(in Kbps)</td>
   <td>Average output bitrate. Value range: 100–8,000 Kbps.<ul style="margin:0">
       <li>A value below 1,000 Kbps must be a multiple of 100.</li>
       <li>A value above 1,000 Kbps must be a multiple of 500.</li>
       </ul>Note: the specified output bitrate remains at the original bitrate if it is higher than the input original bitrate. </li></td>
   </tr><tr>
   <td>Video height<br>(in px)</td>
   <td>Video height. The width will be scaled proportionally. Value range: 0–3,000 px.<br>Note: the value must be a multiple of 4.</td>
   </tr><tr>
   <td>Keyframe interval/GOP<br>(in seconds)</td>
   <td>Value range: 2-6 seconds. The larger the GOP, the higher the delay. If it is not set, the system default value will be used.</td>
   </tr>
   </tbody></table>





<span id="C_topspeed"></span>
## Creating Top Speed Codec Transcoding Template

1. Log in to the LVB Console, and select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Click **+**, select **Top Speed Codec** as the transcoding type, set the configuration items, and click **Save**.

<img src="https://main.qcloudimg.com/raw/39f2a3a1348f0ba26281bb7ea545f645.png" width="800px"></img>
<table>
   <thead><tr><th width="20%">Top Speed Codec Transcoding Configuration Item</th><th width="80%">Description</th></tr></thead>
   <tbody><tr>
   <td>Applicable template</td>
	 <td>It supports three types of templates: <b>LD, SD, and HD</b>. Default template: SD. <br>After you select a template, the system will automatically enter the recommended video bitrate and video height. You can also modify them manually.</td>
   </tr><tr>
   <td>Template name</td>
   <td>LVB transcoding template name, which can contain 1–10 letters and digits.</td>
   </tr><tr>
   <td>Template description</td>
   <td>LVB transcoding template description, which can contain only letters, digits, underscores, and hyphens.</td>
   </tr><tr>
   <td>Video bitrate<br>(in Kbps)</td>
   <td>Average output bitrate. Value range: 100–8,000 Kbps.<ul style="margin:0">
       <li>A value below 1,000 Kbps must be a multiple of 100.</li>
       <li>A value above 1,000 Kbps must be a multiple of 500.</li>
       </ul>Note: the specified output bitrate remains at the original bitrate if it is higher than the input original bitrate. </li></td>
   </tr><tr>
   <td>Video height<br>(in px)</td>
   <td>Video height. The width will be scaled proportionally. Value range: 0–3,000 px.<br>Note: the value must be a multiple of 4.</td>
   </tr><tr>
   <td>Bitrate compression ratio</td>
   <td>Percentage of bitrate to be lowered based on the configured video bitrate, which is used to dynamically adjust the bitrate without modifying other configuration items. Value range: 10–50.<br>Note: please enter an integer between 10 and 50.<br>Example: if the video bitrate is set to 1,000 Kbps and the bitrate compression ratio is set to 20%, the actual encoding bitrate will be 800 Kbps.</b></td>
   </tr><tr>
   <td>Keyframe interval/GOP<br>(in seconds)</td>
   <td>Value range: 2-6 seconds. The larger the GOP, the higher the delay. If it is not set, the system default value will be used.</td>
   </tr>
   </tbody></table>



<span id="modify"></span>
## Modifying Template
1.Select **Feature Configuration** > **[LVB Transcoding](https://console.cloud.tencent.com/live/config/transcode)**.
2. Select the target transcoding template and click **Edit** on the right to modify the template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/cda8daca20edabb43974de18a2c70e55.png)

<span id="delect"></span>
## Deleting Template
If a template has been associated, you need to unassociate it before deleting it. For detailed directions, please see [Unassociating Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062#Untie). 
1. Select **Feature Configuration** > **LVB Transcoding**.
2. Select the target transcoding template and click "Delete" at the top.
3. Confirm whether to delete the selected transcoding template and click **OK** to delete it.

![](https://main.qcloudimg.com/raw/af5f6c3cc83c8ed5b1f50d37a054ce1d.png)


<span id="related"></span>
## Associating the Template with a Domain Name
For more information, see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062).
