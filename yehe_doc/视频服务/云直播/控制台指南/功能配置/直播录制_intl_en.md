CSS supports recording live streams and storing recording files in VOD for download and preview. This document describes how to create, bind, unbind, modify, and delete recording templates.
You can create a recording template in two ways:

- In the CSS console: For detailed directions, see [Creating a Recording Template](#C_record).
- Through an API: For the API parameters and examples, see [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845).

## Notes
- Recording files are saved in [VOD](https://console.cloud.tencent.com/vod/overview) by default. Please activate VOD first. For more information, see [Getting Started with VOD](https://intl.cloud.tencent.com/document/product/266/8757).
- After enabling the recording feature, please make sure that your VOD service is in normal status. If it is not activated or is suspended due to overdue payments, live recording will fail. No recording files will be generated. Nor will fees be incurred.
- A recording file is available in about 5 minutes after recording ends. For example, if you start recording a live stream at 12:00 and stop at 12:30, you can get the recorded video at around 12:35.
- Because only FLV, .MP4, and HLS formats are supported, you can only use the H.264 video codec and the AAC audio codec.
- After creating a recording template, you can bind it with push domain names. For detailed directions, see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224). The binding takes effect in about 5-10 minutes.
- For the naming rules of generated recording files, see [VodFileName](https://intl.cloud.tencent.com/document/product/267/30767#RecordParam).
- Binding, unbinding, or modifying a template affects only new live streams and not ongoing ones. To make the change apply to ongoing live streams, you need to stop them and push them again.
- Mixed-stream recording does not support mixing streams inside the Chinese mainland with those outside. It will cause an error and playback will fail.



## Prerequisites
- You have activated CSS and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have activated the [VOD service](https://intl.cloud.tencent.com/document/product/266/8757#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5.BC.80.E9.80.9A.E4.BA.91.E7.82.B9.E6.92.AD).

[](id:C_record)
## Creating a Recording Template
1. Log in to the CSS console and select **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record) on the left sidebar.
2. Click **Create Recording Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/ca30bd94a2f81ecead5c1684b8007744.png)

<table>
   <thead><tr><th width="20%" colspan=2>Item</th><th>Description</th></tr></thead>
   <tbody><tr>
   <tr>
   <td colspan=2>Template Name</td>
   <td>The template name, which can contain letters, digits, underscores (_), and hyphens (-).</td>
   </tr><tr>
   <td colspan=2>Template Description</td>
   <td>The template description, which can contain letters, digits, underscores (_), and hyphens (-).</td>
   </tr><tr>   
   <td rowspan=3 width="10%">Recording Content</td>
   <td width="30%">Original stream</td> 
   <td>Record videos before transcoding, watermarking, and stream mixing.</ul></td>
   </tr><tr>
   <td>Watermarked stream</td>
   <td>Record videos after they are watermarked according to the specified watermark template.</td>
   </tr><tr>
   <td>Transcoded stream</td>
   <td> Record transcoded streams. You can select an existing transcoding template or click the name of a template to modify its configuration. If you select this, streams will be watermarked and transcoded as specified in the selected template before recording. If the template is deleted, streams will be recorded after they are watermarked.</td>
   </tr><tr>
   <td colspan=2>Recording Format</td>
   <td>Videos can be outputted in formats of HLS, MP4, FLV, and AAC (for audio-only recording).</td>
   </tr>
   </tbody></table>
>! 
>- If you select **Original stream**, you cannot record the audio of WebRTC streams.
>- You cannot record transcoded streams if you use the time shifting feature. If a recording template has time shifting configured, original streams will be recorded.
>- If an audio-only transcoding template is selected, the recording format must be an audio format as well.
>- To record transcoded streams, the system will initiate transcoding tasks, which will incur transcoding fees. If you use the same transcoding template for playback, the transcoding will be charged only once.
3. Select the recording content and formats and complete the following settings:
![](https://qcloudimg.tencent-cloud.cn/raw/0a835b00a6864bc29411da9d8088a626.png)

<table>
   <thead><tr><th width="27%" colspan=2>Item</th><th>Description</th></tr></thead>
   <tbody><tr>
      <tr>
      <td colspan=2>Max Recording Time Per File</td>
      <td><ul style="margin-bottom:0px">
          <li>There is no upper limit on the length of a recording file in HLS format. If a live stream is interrupted and the timeout period for resumption elapses, a new recording file will be generated to continue recording.</li>
          <li>The value range for the maximum length of a recording file in MP4, FLV, or AAC format is 1-120 minutes.</li>
          </ul></td>
      </tr><tr>
      <td colspan=2>Resumption Timeout</td>
      <td>Only the HLS format supports recording resumption after push interruption, and the value range for the timeout period for resumption is 1-1800 seconds.</td>
      </tr><tr>
      <td colspan=2>Storage Period (days)</td>
      <td>You can select <b>Permanent</b> to save a recording file permanently or <b>Custom</b> to specify a storage period (up to 1,500 days). If you set the period to 0, recording files will be saved permanently.</td>
      </tr><tr>
      <td colspan=2>VOD Subapplication/Category</td>
      <td>By default, streams are recorded to the primary application in VOD, but you can also record them to a specified category of a specified writable <a href="https://console.cloud.tencent.com/vod/app-manage">subapplication</a>.</td>
      </tr><tr>
      <td rowspan=3 width="12%">Advanced Configuration</td>
      <td>Storage Policy</td> 
      <td><ul style=margin:0><li>Select STANDARD (default) if the recording files need to be played back for business purposes. </li><li>Select STANDARD_IA (cold storage) if the recording files will not be accessed frequently or will be stored for a long period of time.</li></ul></td>
      </tr><tr>
      <td>VOD Task Flow</td>
      <td>Click <b>Select</b> to bind a task flow created under the specified VOD subapplication. In the pop-up window, you can click the name of a task flow to modify its configuration. The selected task flow will be executed on recording files upon generation, which will incur <a href="https://intl.cloud.tencent.com/document/product/266/2838">VOD fees</a>.</td>
       </tr><tr>
       <td>Upload while recording</td> 
      <td>Currently, only the FLV format supports upload while recording. This feature makes it possible to finish uploading a video as soon as recording ends. It extends the maximum recording time per file to 12 hours and makes FLV recording more disaster tolerant. Online playback of the recording files may stutter, but local playback is unaffected.</td>
      </tr>
      </tbody></table>

>! For **Storage Policy**:
>- If you select **STANDARD** and cold storage is enabled for the selected application/category, streams will be recorded to STANDARD storage first before the configured cold storage policy is executed on the recording files. You can go to [Cold Storage](https://console.cloud.tencent.com/vod/inactivation) to view your cold storage policies.
>- If you select **STANDARD_IA** and cold storage is enabled for the selected application/category, streams will be recorded to STANDARD_IA storage first, and the system will then determine whether to execute the cold storage policy.
4. Click **Save**.

[](id:conect)
## Binding a Domain Name
1. Log in to the CSS console and select **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record) on the left sidebar.
    - **Bind a domain to an existing transcoding template**: Click **Bind Domain Name** in the top left.
    ![](https://main.qcloudimg.com/raw/bcb6c5da46a3455f94d441134e49825a.png)
    - **Bind a domain after creating a template**: After [creating a template](#C_record), click **Bind Domain Name** in the dialog box that pops up.
    ![](https://qcloudimg.tencent-cloud.cn/raw/b45ec9863fe4c6f16fe5551605ce46d9.png)
2. In the pop-up window, select a **recording template** and a **push domain name** and then click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/9abc1af79841e877d4e194d0d5741efc.png)

>? You can click **Add** to bind multiple push domain names to a template.

[](id:unite)
## Unbinding a Domain Name
1. Log in to the CSS console and select **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record) on the left sidebar.
2. Select a recording template bound with domain names, find the target domain name, and click **Unbind**.
   ![](https://main.qcloudimg.com/raw/f7071a4b4f9297124b460ffebcba64d3.png)
3. In the pop-up window, click **Confirm**.
    ![](https://main.qcloudimg.com/raw/a666387f882584860eaf2c229c2b4769.png)

>? 
>- Unbinding the recording template will not affect ongoing live streams.
>- For the unbinding to take effect for ongoing streams, stop the streams and push them again, after which no recording files will be generated.


[](id:change)
## Modifying a Template
1. Go to **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record).
2. Select the target recording template, click **Edit** on the right, modify the settings, and click **Save**.
![](![img](https://main.qcloudimg.com/raw/68f4dd1a6452a3e97e7ff4dea6493d7b.png)

[](id:delete)
## Deleting a Template
1. Log in to the CSS console and select **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record) on the left sidebar.
2. Select the target recording template, and click **Delete** in the upper right.
3. In the pop-up window, click **Confirm**.
![](https://main.qcloudimg.com/raw/c7c3e300488ba332b84bfd61da0fb999.png)

>! 
>- If domain names are bound to a template, you need to [unbind](#unite) them before you can delete the template.
>- In the console, recording templates are managed at the domain level. To unbind recording rules created and bound by APIs, call [DeleteLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30843). 


## Related Operations
For more information about **binding a domain name with** and **unbinding a domain name from** a recording template, see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/34224).


## FAQs
[](id:que1)
#### How are recording files named?
If a recording template is created in the console, the names of its recording files (the names returned by the recording callback) are in the following format:
`{StreamID}*{StartYear}-{StartMonth}-{StartDay}-{StartHour}-{StartMinute}-{StartSecond}*{EndYear}-{EndMonth}-{EndDay}-{EndHour}-{EndMinute}-{EndSecond} `

**Fields:**

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
