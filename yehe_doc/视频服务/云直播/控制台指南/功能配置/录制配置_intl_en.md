LVB supports recording live streams and storing recording files in VOD for download and preview. This document describes how to create, bind, unbind, modify, and delete recording templates.
You can create a recording template in the following two methods:
- Create a recording template in the LVB console. For detailed directions, please see [Creating Recording Template](#C_record).
- Create a recording template with APIs. For specific parameters and samples, please see [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845).

## Notes
- The recorded video files are stored in the [VOD console](https://console.cloud.tencent.com/vod/overview) by default. We recommend you activate the VOD service in advance so as to avoid service suspension due to overdue payment. For more information, please see [Getting Started with VOD](https://intl.cloud.tencent.com/document/product/266/8757).
- After enabling the recording feature, please make sure that your VOD service is in normal status; if it has not been activated or has been suspended due to overdue payment, LVB recording will not be available, no recording files will be generated, and no recording fees will be incurred.
- During the live streaming, you can get a recording file in about 5 minutes after the recording process ends. For example, if a recording starts at 12:00 and ends at 12:30, you can get the segment of 12:00-12:30 at around 12:35.
- As video format only supports .flv, .mp4, and .hls, video codec can only be H.264 and audio codec can only be AAC.
- After a recording template is created successfully, it can be bound with push domain names. For more information, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224). The binding will take effect in about 5-10 minutes.
- For the naming rules of generated recording files, please see [VodFileName](https://intl.cloud.tencent.com/document/product/267/30767#RecordParam).
- Binding, unbinding, and modifying a template affect only new live streams after the update but not ongoing ones. To make the new rule take effect for ongoing live streams, you need to interrupt them and push them again.


## Prerequisites
- You have activated the LVB service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have activated the [VOD service](https://intl.cloud.tencent.com/document/product/266/8757#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5.BC.80.E9.80.9A.E4.BA.91.E7.82.B9.E6.92.AD).

<span id="C_record"></span>
## Creating a Recording Template
1. Log in to the LVB console and select **Feature Configuration** > **[LVB Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Click **Create Recording Template** to set template information and configure as follows:
![](https://main.qcloudimg.com/raw/74a4ac0636c59ff69c23437e72189567.png)
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
   <td>Custom LVB recording template description, which can contain letters, digits, underscores (_), and hyphens (-).</td>
   </tr><tr>
   <td>Recording File Type</td>
   <td>Videos are recorded in the original bitrate of the live stream and can be outputted in formats of .hls, .mp4, .flv, and .aac (for audio recording).</td>
   </tr><tr>
   <td>Single File Duration (min)</td>
   <td><ul style="margin-bottom:0px">
       <li>There is no upper limit for .hls format. If the recording duration of a file exceeds the timeout period for resumption, a new file will be created to continue recording.</li>
       <li>The duration of a single file recorded in .mp4, .flv, or .aac format ranges from 5 to 120 minutes.</li>
       </ul></td>
   </tr><tr>
   <td>Retention Period (day)</td>
   <td>A single recording file can be retained up to 1,080 days. A retention period of 0 means "never expire".</td>
   </tr><tr>
   <td>Resumption Timeout Period (sec)</td>
   <td>Only the .hls format supports recording resumption after push interruption, and the timeout period for resumption can be set between 0 and 1800 seconds.</td>
   </tr><tr>
   <td>Recording to Subapplication</td>
   <td>Live streams can be recorded to a specified <a href="https://console.cloud.tencent.com/vod/app-manage">subapplication</a> in VOD. They are recorded to the primary application under the account by default. Only writable subapplications are supported.</td>
   </tr>
   </tbody></table>
3. Click **Save**.


<span id="conect"></span>
## Binding a Template with Domain Names
1. Log in to the LVB console and select **Feature Configuration** > **[LVB Recording](https://console.cloud.tencent.com/live/config/record)**.
	- **Directly bind a domain name**: click **Bind Domain Name** in the top-left corner.
	![](https://main.qcloudimg.com/raw/bcb6c5da46a3455f94d441134e49825a.png)
	- **Bind a domain name after creating a recording template:** after successfully [creating a recording template](#C_record), click **Bind Domain Name** in the pop-up window.
	![](https://main.qcloudimg.com/raw/7f26a83d95d0f08ceda1b10e93e30389.png)
1. Select a **recording template** and a **push domain name** in the domain name binding window and then click **Confirm**.
![](https://main.qcloudimg.com/raw/a9411818457b4e708fd624f970d92ab6.png)

>? You can click **Add** to bind multiple push domain names with this template.

<span id="unite"></span>
## Unbinding a Template from a Domain Name

1. Log in to the LVB console and select **Feature Configuration** > **[LVB Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Select a recording template with bound domain names, and click **Unbind** for the target domain name.
   ![](https://main.qcloudimg.com/raw/f7071a4b4f9297124b460ffebcba64d3.png)
3. Confirm whether to unbind the domain name and click **Confirm** to unbind it.
    ![](https://main.qcloudimg.com/raw/a666387f882584860eaf2c229c2b4769.png)

>? 
>- Unbinding the recording template will not affect ongoing live streams.
>- To make the unbinding take effect, interrupt ongoing live streams and push them again. The new live streams will not generate recording files.


<span id="change"></span>
## Modifying a Template
1. Go to **Feature Configuration** > **[LVB Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Select the target recording template and click **Edit** on the right to modify the template information.
3. Click **Save**.

![](https://main.qcloudimg.com/raw/68f4dd1a6452a3e97e7ff4dea6493d7b.png)

<span id="delete"></span>
## Deleting a Template
1. Go to **Feature Configuration** > **LVB Recording**.
2. Select the target recording template and click ![](https://main.qcloudimg.com/raw/220ada95a4b631349543cc8cde96226e.png) at the top.
3. Confirm whether to delete the selected recording template and click **OK** to delete it.
![](https://main.qcloudimg.com/raw/c7c3e300488ba332b84bfd61da0fb999.png)

>! 
>- If the template has been bound with domain names, you need to [unbind](#unite) the template before deleting it.
>- The recording templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you have bound the recording configuration with a specified stream through the recording management API and want to unbind them, you need to call the [DeleteLiveRecordRule API](https://intl.cloud.tencent.com/document/product/267/30843). 


## Operations
For more information about **binding** and **unbinding a domain name** with a recording template, see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224).


## FAQs
<span id="que1"></span>
#### How are videos generated by LVB recording named?
Recording files generated by the callback of a recording template created in the console are named in the following format by default:
`{StreamID}*{StartYear}-{StartMonth}-{StartDay}-{StartHour}-{StartMinute}-{StartSecond}*{EndYear}-{EndMonth}-{EndDay}-{EndHour}-{EndMinute}-{EndSecond} `

 

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
