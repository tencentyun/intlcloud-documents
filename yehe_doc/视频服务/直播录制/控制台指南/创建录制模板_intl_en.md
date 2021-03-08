LVB supports recording live streams and storing recording files in VOD for download and preview. This document describes how to create, bind, unbind, modify, and delete recording templates.
You can create a recording template in either of the following two methods:
- Create a recording template in the LVB console. For detailed directions, please see [Creating Recording Template](#C_record).
- Create a recording template with APIs. For specific parameters and samples, please see [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/zh/document/product/267/30845).

## Notes
- The recorded video files are stored in the [VOD console](https://console.cloud.tencent.com/vod/overview) by default. We recommend you activate the VOD service in advance. For more information, please see [Getting Started with VOD](https://intl.cloud.tencent.com/document/product/266/8757).
- After enabling the recording feature, please make sure that your VOD service is in normal status. If it is not activated or is suspended due to overdue payment, LVB recording will not be available, no recording files will be generated, and no recording fees will be incurred.
- During the live streaming, you can get a recording file in about 5 minutes after the recording process ends. For example, if you start recording a live stream at 12:00, you can get the corresponding clip for 12:00 to 12:30 at around 12:35.
- Subject to the audio and video file formats (FLV/MP4/HLS), the video encoding format of H.264 and audio encoding format of ACC are supported.
- After a recording template is created successfully, it can be bound to a push domain name. For more information, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224). The binding will take effect in about 5–10 minutes.
- For the naming rules of generated recording files, please see [VodFileName](https://intl.cloud.tencent.com/zh/document/product/267/30767).
- Binding, unbinding, and modifying a template affect only new live streams after the update but not ongoing ones. To make the new rule take effect for ongoing live streams, you need to interrupt them and push them again.
- Stream mix-based recording does not support mixing streams in and outside Chinese mainland, as recording file errors will occur and affect normal playback.


## Prerequisites
- You have activated the LVB service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have activated the [VOD service](https://intl.cloud.tencent.com/document/product/266/8757#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5.BC.80.E9.80.9A.E4.BA.91.E7.82.B9.E6.92.AD).

<span id="C_record"></span>
## Creating Recording Template
1. Log in to the LVB console and select **Feature Configuration** > **[LVB Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Click **Create Recording Template** to set template information and configure as follows:
![](https://main.qcloudimg.com/raw/ff493f1885c86c013bfb0ac6d3c4f9d2.png)
<table>
   <thead><tr><th>Configuration Item</th><th>Configuration Description</th></tr></thead>
   <tbody><tr>
   <td>Default Template</td>
   <td>Default template type for LVB recording, which can be FLV, MP4, or HLS.</td>
   </tr><tr>
   <td>Template Name</td>
   <td>Custom LVB recording template name, which can contain letters, digits, underscores (_), and hyphens (-).</td>
   </tr><tr>
   <td>Template Description</td>
   <td>Custom LVB recording template description, which can contain letters, digits, underscores, and hyphens.</td>
   </tr><tr>
   <td>Recording File Type</td>
   <td>Videos are recorded based on the original bitrate of the live stream and can be output in .hls, .mp4, .flv, and .aac formats. The .aac format records the audio only.</td>
   </tr><tr>
   <td>Single File Duration (min)</td>
   <td><ul style="margin-bottom:0px">
       <li>There is no upper limit for .hls format. After the resuming timeout period elapses, a new file will be created to continue recording.</li>
       <li>The length of a single file recorded in .mp4, .flv, or .aac format ranges from 5 to 120 minutes.</li>
       </ul></td>
   </tr><tr>
   <td>Retention Period (day)</td>
   <td>A single recording file can be retained for up to 1,080 days. A retention period of 0 means "never expire".</td>
   </tr><tr>
   <td>Resuming Timeout (sec)</td>
   <td>Only the .hls format supports recording resumption after push interruption, and the timeout period for resumption can be set between 0 and 1,800 seconds.</td>
   </tr><tr>
   <td>Recording to Subapplication</td>
   <td>Live streams can be recorded to a specified <a href="https://console.cloud.tencent.com/vod/app-manage">subapplication</a> in VOD. They are recorded to the primary application under the account by default. Only writable subapplications are supported.</td>
   </tr>
   </tbody></table>
3. Click **Save**.


<span id="conect"></span>
## Binding Domain Name
1. Log in to the LVB console and select **Feature Configuration** > **[LVB Recording](https://console.cloud.tencent.com/live/config/record)**.
	- **Directly bind a domain name**: click **Bind Domain Name** in the top-left corner.
	![](https://main.qcloudimg.com/raw/71efeb1c60eca4446add2764005e3af4.png)
	- **Bind a domain name after creating a recording template:** after successfully [creating a recording template](#C_record), click **Bind Domain Name** in the pop-up.
	![](https://main.qcloudimg.com/raw/941e2a0101511e908fee52e0ff83cb38.png)
1. Select a **recording template** and a **push domain name** in the domain name binding window and then click **OK**.
![](https://main.qcloudimg.com/raw/77d815dd4ff49f7439b363e8bb2cf58e.png)

>? You can click **Add** to bind multiple push domain names with this template.

<span id="unite"></span>
## Unbinding

1. Log in to the LVB console and select **Feature Configuration** > **[LVB Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Select the recording template bound to the domain name and click **Unbind**.
   ![](https://main.qcloudimg.com/raw/d6bafcefe50a615e1ccbd073e509b7f4.png)
3. Confirm whether to unbind the domain name and click **OK** to unbind it.
    ![](https://main.qcloudimg.com/raw/67366e0d33fec809a175c79dd128fe64.png)

>? 
>- Unbinding the recording template will not affect ongoing live streams.
>- To make the unbinding take effect, interrupt ongoing live streams and push them again. The new live streams will not generate recording files.

<span id="change"></span>
## Modifying Template
1. Go to **Feature Configuration** > **[LVB Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Select the target recording template and click **Edit** on the right to modify the template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/c3a2e012eb0b5d147975174b6de19dce.png)

<span id="delete"></span>
## Deleting Template
1. Go to **Feature Configuration** > **LVB Recording**.
2. Select the target recording template and click ![](https://main.qcloudimg.com/raw/220ada95a4b631349543cc8cde96226e.png) above.
3. Confirm whether to delete the selected recording template and click **OK** to delete it.
![](https://main.qcloudimg.com/raw/b7cb69ff6c9f17578799770b9995c3a8.png)

>! 
>- If the template has been bound with a domain name, you need to [unbind](#unite) the template before deleting it.
>- The recording templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you bound the recording configuration to a specified stream through the recording management API and want to unbind them, you need to call the [DeleteLiveRecordRule API](https://intl.cloud.tencent.com/document/product/267/30843). 


## Relevant Operations
For more information on how to **bind/unbind** a **domain name** to/from a recording template, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224).


## FAQs
<span id="que1"></span>
#### How are videos generated by LVB recording named?
Recording files generated by the callback of a recording template created in the console are named in the following format by default:
`{StreamID}*{StartYear}-{StartMonth}-{StartDay}-{StartHour}-{StartMinute}-{StartSecond}*{EndYear}-{EndMonth}-{EndDay}-{EndHour}-{EndMinute}-{EndSecond} `

**Among them:**

| Placeholder             | Description          |
| ------------------ | ------------- |
| {StreamID}         | Stream ID          |
| {StartYear}        | Start time - year   |
| {StartMonth}       | Start time - month   |
| {StartDay}         | Start time - day   |
| {StartHour}        | Start time - hour |
| {StartMinute}      | Start time - minute |
| {StartSecond}      | Start time - second   |
| {EndYear}          | End time - year   |
| {EndMonth}         | End time - month   |
| {EndDay}           | End time - day   |
| {EndHour}          | End time - hour |
| {EndMinute}        | End time - minute |
| {EndSecond}        | End time - second   |
