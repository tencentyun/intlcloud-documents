CSS supports recording live streams and storing recording files in VOD for download and preview. This document describes how to create, bind, unbind, modify, and delete recording templates.
You can create a recording template in either of the following two methods:
- In the CSS console: For detailed directions, please see [Creating Recording Template](#C_record).
- Through an API: For the API parameters and examples, please see [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845).

## Notes
- The recorded video files are stored in the [VOD console](https://console.cloud.tencent.com/vod/overview) by default. We recommend you activate the VOD service in advance. For more information, please see [Getting Started with VOD](https://intl.cloud.tencent.com/document/product/266/8757).
- After enabling the recording feature, please make sure that your VOD service is in normal status. If it is not activated or is suspended due to overdue payment, live recording will not be available, no recording files will be generated, and no recording fees will be incurred.
- A recording file is available in about 5 minutes after recording ends. For example, if you start recording a live stream at 12:00 and stop at 12:30, you can get the recorded video at around 12:35.
- As only .flv, .mp4, and .hls video formats are supported, the video codec can only be H.264 and audio codec can only be AAC.
- After creating a recording template, you can bind it with push domain names. For more information, please see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224). The binding will take effect in about 5-10 minutes.
- For the naming rules of generated recording files, please see [VodFileName](https://intl.cloud.tencent.com/document/product/267/30767#RecordParam).
- Binding, unbinding, and modifying a template affect only new live streams after the update but not ongoing ones. To make the new rule take effect for ongoing live streams, you need to interrupt them and push them again.
- Stream mix-based recording does not support mixing streams in and outside Chinese mainland, as recording file errors will occur and affect normal playback.



## Prerequisites
- You have activated the CSS service and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have activated the [VOD service](https://intl.cloud.tencent.com/document/product/266/8757#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5.BC.80.E9.80.9A.E4.BA.91.E7.82.B9.E6.92.AD).

[](id:C_record)
## Creating Recording Template
1. Log in to the CSS console and select **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Click **Create Recording Template** and set template information as follows:
![](https://main.qcloudimg.com/raw/ccf133a64c38ce579a9fd91e37514193.png)

<table>
   <thead><tr><th width="20%">Item</th><th>Description</th></tr></thead>
   <tbody><tr>
   <tr>
   <td>Template Name</td>
   <td>Custom live recording template name, which can contain letters, digits, underscores (_), and hyphens (-).</td>
   </tr><tr>
   <td>Template Description</td>
   <td>Custom live recording template description, which can contain letters, digits, underscores (_), and hyphens (-).</td>
   </tr><tr>
   <td>Recording Format</td>
   <td>Videos are recorded in the original bitrate of a live stream and can be outputted in formats of .hls, .mp4, .flv, and .aac (for audio-only recording).</td>
   </tr>
   </tbody></table>
3. You can select multiple formats. For each format selected, a section appears for you to fill in the details.

![](https://main.qcloudimg.com/raw/74a4ac0636c59ff69c23437e72189567.png)

<table>
   <thead><tr width="24%"><th colspan=2>Item</th><th>Description</th></tr></thead>
   <tbody><tr>
      <tr>
      <td colspan=2>Max Recording Time Per File (min)</td>
      <td><ul style="margin-bottom:0px">
          <li>There is no upper limit on the recording time of a file in .hls format. If a live stream is interrupted and the timeout period for resumption elapses, a new recording file will be generated to continue recording.</li>
          <li>The length of a single file recorded in .mp4, .flv, or .aac format ranges from 1 to 120 minutes.</li>
          </ul></td>
      </tr><tr>
      <td colspan=2>Resumption Timeout (sec)</td>
      <td>Only the .hls format supports recording resumption after push interruption, and the timeout period for resumption can be set between 0 and 1800 seconds.</td>
      </tr><tr>
      <td colspan=2>Storage Period (days)</td>
      <td>You can select <b>Permanent</b> to save a recording file permanently or <b>Custom</b> to specify a storage period (up to 1,500 days). Setting the period to `0` means to save recording files permanently.</td>
      </tr><tr>
      <td colspan=2>VOD Subapplication/Category</td>
      <td>By default, streams are recorded to the primary application in VOD, but you can also record them to a specified category of a specified writable <a href="https://console.cloud.tencent.com/vod/app-manage">subapplication</a>.</td>
      </tr><tr>
      <td rowspan=2 width="12%">Advanced Configuration</td>
      <td>Storage Policy</td> 
      <td><ul style=margin:0><li>Select STANDARD (default) if the recording files need to be played back for business purposes. </li><li>Select STANDARD_IA (cold storage) if the recording files will not be accessed frequently or will be stored for a long period of time.</li></ul></td>
      </tr><tr>
      <td>VOD Task Flow</td>
      <td>Click <b>Select</b> to bind a task flow created under the VOD subapplication. You can also click a task flow to go to the VOD console, where you can modify the task flow or create new ones. The bound task flow will be executed on recording files upon generation, for which you will be charged <a href="https://tcloud-doc.isd.com/document/product/266/2838">VOD fees</a>.</td>
      </tr>
      </tbody></table>

>! Notes:
>- If you select **STANDARD** for **Storage Policy** and cold storage is enabled for the selected application/category, streams will be recorded to STANDARD storage first before the configured cold storage policy is executed on the recording files. You can go to [Cold Storage](https://console.cloud.tencent.com/vod/inactivation) to view your cold storage policies.
>- If you select **STANDARD_IA** and cold storage is enabled for the selected application/category, streams will be recorded to STANDARD_IA storage first, and the system will then determine whether to execute the cold storage policy.

4. Click **Save**.

[](id:conect)
## Binding Domain Name
1. Log in to the CSS console and select **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
    - To **bind a domain name to an existing recording template**, click **Bind Domain Name** in the upper left.
    ![](https://main.qcloudimg.com/raw/bcb6c5da46a3455f94d441134e49825a.png)
    - You can also click **Bind Domain Name** in the dialog box that pops up **upon successful [template creation](#C_record)**. 
    ![](https://main.qcloudimg.com/raw/7f26a83d95d0f08ceda1b10e93e30389.png)
2. In the pop-up window, select a **recording template** and a **push domain name** and then click **Confirm**.
![](https://main.qcloudimg.com/raw/a9411818457b4e708fd624f970d92ab6.png)

>? You can click **Add** to bind multiple push domain names to a template.

[](id:unite)
## Unbinding Domain Name
1. Log in to the CSS console and select **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Select a recording template with bound domain names, find the target domain name, and click **Unbind**.
   ![](https://main.qcloudimg.com/raw/f7071a4b4f9297124b460ffebcba64d3.png)
3. In the pop-up, click **Confirm**.
    ![](https://main.qcloudimg.com/raw/a666387f882584860eaf2c229c2b4769.png)

>? 
>- Unbinding the recording template will not affect ongoing live streams.
>- To make the unbinding take effect, interrupt ongoing live streams and push them again. The new live streams will not generate recording files.


[](id:change)
## Modifying Template
1. Go to **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Select the target recording template and click **Edit** on the right to modify the template information.
3. After modification, click **Save**.

![](![img](https://main.qcloudimg.com/raw/68f4dd1a6452a3e97e7ff4dea6493d7b.png)

[](id:delete)
## Deleting Template
1. Log in to the CSS console and select **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)**.
2. Select the target recording template, and click **Delete** in the upper right.
3. In the pop-up window, click **Confirm**.
![](https://main.qcloudimg.com/raw/c7c3e300488ba332b84bfd61da0fb999.png)

>! 
>- If the template has been bound with domain names, you need to [unbind](#unite) the template before deleting it.
>- In the console, you can manage recording templates by domain name, and cannot cancel rules created by APIs. If you have bound the recording configuration with a specified stream through the recording management APIs and want to unbind them, you need to call the [DeleteLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30843) API. 


## Related Operations
For more information about **binding a domain name with** and **unbinding a domain name from** a recording template, see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224).


## FAQs
[](id:que1)
#### How are videos generated by live recording named?
Recording files generated by the callback of a recording template created in the console are named in the following format by default:
`{StreamID}*{StartYear}-{StartMonth}-{StartDay}-{StartHour}-{StartMinute}-{StartSecond}*{EndYear}-{EndMonth}-{EndDay}-{EndHour}-{EndMinute}-{EndSecond} `

**Description:**

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
