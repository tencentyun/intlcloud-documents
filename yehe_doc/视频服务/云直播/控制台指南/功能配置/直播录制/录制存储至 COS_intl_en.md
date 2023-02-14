With CSS, you can record a live stream and save the recording file to VOD or COS. This document shows you how to record to Cloud Object Storage (COS).

## Notes

1. To record to COS, you need to activate COS first. We recommend you buy a storage package in advance to avoid service suspension caused by overdue payments. For details, see [COS > Getting Started](https://intl.cloud.tencent.com/document/product/436/32955).
2. After enabling the recording feature, please make sure that your COS service is in normal status. If COS is not activated or is suspended due to overdue payments, live recording will fail. No recording files will be generated. Nor will fees be incurred.
3. A recording file is available about five minutes after recording ends. For example, if you start recording a live stream at 12:00 and stop at 12:30, you can get the recorded video at around 12:35.
4. After creating a recording template, you need to bind it to a push domain. For detailed directions, see “Recording Configuration”. The template takes effect 5-10 minutes after binding.
5. Mixed-stream recording does not support mixing streams inside the Chinese mainland with streams outside. Doing so will cause an error and playback of the recording file will fail.
6. CSS needs permissions to store recording files in COS. Before you use the record-to-COS feature, make sure you have granted the necessary permission. If recording to COS fails due to insufficient permissions, the video cannot be recovered. For how to grant the permission, see “Authorizing CSS to Store Recording Files in COS”.
7. If you don’t specify a recording template when initiating a recording task, the recording file will be saved to VOD.
 

## Prerequisites

- You have activated CSS and added a [push domain](https://intl.cloud.tencent.com/document/product/267/35970).
- You have activated [COS](https://intl.cloud.tencent.com/document/product/436/32955).

## Creating a Recording Template

1. Log in to the CSS console and select **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record) on the left sidebar.
2. Select **Save to COS**.
3. Click **Create template** and complete the following settings:
![](https://qcloudimg.tencent-cloud.cn/raw/5b4be3ce104a74e1092053be5ffcda8a.png)

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
   <td>Record videos before transcoding, watermarking, and stream mixing. For WebRTC streams, please select other content types, because audio will be missing from the recording files.</ul></td>
   </tr><tr>
   <td>Watermarked stream</td>
   <td>Record videos after they are watermarked according to the specified watermark template.</td>
   </tr><tr>
   <td>Transcoded stream</td>
   <td>Record videos after they are transcoded according to the specified transcoding template. You can select an existing transcoding template or click the name of a template to modify its configuration. If the template configured is deleted, original streams will be recorded.</td>
   </tr><tr>
   <td colspan=2>Recording Format</td>
   <td>Videos can be outputted in formats of HLS, MP4, FLV, and AAC (for audio-only recording).</td>
   </tr>
   </tbody></table>

>! 
>- If you select **Original stream**, you cannot record the audio of WebRTC streams.
>- You cannot record transcoded streams if you use the time shifting feature. If time shifting is enabled for a stream, the original stream will be recorded.
>- If an audio-only transcoding template is selected, the recording format must also be an audio format.
>- To record a transcoded live stream, you need to configure a transcoding task for the stream in advance. This will incur transcoding fees. Transcoding fees will be charged only once for playback of the same transcoded stream (same transcoding template).

3. Select the recording content and formats and complete the following settings:
 ![](https://qcloudimg.tencent-cloud.cn/raw/ef25f0451d1625570046b88c7a7eba55.png)

<table>
<thead><tr><th width="27%" colspan=2>Item</th><th>Description</th></tr></thead>
<tbody><tr>
<tr>
<td colspan=2>Max Recording Time Per File</td>
<td><ul style="margin-bottom:0px">
<li>There is no upper limit on the length of a recording file in HLS format. If a live stream is interrupted and the timeout period for resumption elapses, a new recording file will be generated to continue recording.</li>
<li>The value range for the maximum length of a recording file in FLV format is 1-720 minutes.</li>
<li>The value range for the maximum length of a recording file in MP4 or AAC format is 1-120 minutes.</li>
</ul></td>
</tr><tr>
<td colspan=2>Resumption Timeout</td>
<td>Only the HLS format supports recording resumption after push interruption, and the value range for the timeout period for resumption is 1-1800 seconds.</td>
</tr><tr>
<td colspan=2>Storage Period (days)</td>
<td>You can select <b>Permanent</b> to save a recording file permanently or <b>Custom</b> to specify a storage period (up to 1,500 days). If you set the period to 0, recording files will be saved permanently.</td>
</tr><tr>
<td colspan=2>Storage path</td>
<td><ul style="margin-bottom:0px">
<li>Select a bucket you created in <b>COS</b>. Make sure you have granted CSS access to this bucket.</li>
<li><b>Region</b> shows the region information of the selected COS bucket. It cannot be modified.</li>
</ul></td>
</tr><tr>      
<td colspan=2>Backup storage path</td>      
<td>In case of failure to save recording files to the primary storage path due to network jitter, the backup path will be used. After the primary path recovers, the recording files saved in the backup path will be automatically uploaded to the primary path. The backup and primary paths must be in different regions.</td>
</tr><tr>      
<td colspan=2>Folder</td>      
<td><ul style="margin-bottom:0px">
 <li>The default storage folder is {RecordSource}/{Domain}/{AppName}/{StreamID}/{RecordId}/{StartYear}-{StartMonth}-{StartDay}-{StartHour}-{StartMinute}-{StartSecond}.</li>
 <li>{RecordSource} indicates the content type. If the original stream is recorded, this is "origin". If a transcoded stream is recorded, this is the transcoding template ID.</li>  
<li>{StartYear} indicates the starting year.</li> 
<li>{StartMonth} indicates the starting month.</li>
<li>{StartDay} indicates the starting day.</li>
<li>{StartMinute} indicates the starting minute.</li>
<li>{StartSecond} indicates the starting second.</li>
<li>{Domain} indicates the push domain.</li>
<li>{AppName} indicates the push path.</li>
<li>{StreamID} indicates the stream ID.</li>
<li>{RecordId} indicates the recording task ID, which is returned by the CreateRecordTask API.</li>
<li> "/" indicates folder levels. "-" is an ordinary character.</li>
</ul></td>
</tr>
</tbody></table>

4. Click **Save**.
>? Streams are uploaded while being recorded, which is why the filename does not contain fields that indicate the end time.

[](id:conect)

## Binding a Domain Name

1. Log in to the CSS console, select **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record) on the left sidebar, and click **Save to COS**
   - **Bind a domain to an existing template**: Click **Bind Domain Name** in the top left.
     ![](https://main.qcloudimg.com/raw/d32d938925b1aec96c0e6cfc418eb697.png)
   - **Bind a domain after creating a template**: After [creating a template](#C_record), click **Bind Domain Name** in the dialog box that pops up.
     ![](https://main.qcloudimg.com/raw/4de2cb134a48920fc5527217704e7f76.png)
2. In the pop-up window, select a **recording template** and a **push domain** and then click **Confirm**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/ed874330b279d76e3fe80de2310b12b5.png)

>? You can click **Add** to bind multiple push domains to a template.

[](id:unite)

## Unbinding a Domain Name

1. Log in to the CSS console, select **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record) on the left sidebar, and click **Save to COS**
2. Select a recording template bound with domain names, find the target domain name, and click **Unbind**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d2f0024b98c330addc479e2d51c8810e.png)
3. In the pop-up window, click **Confirm**.
   ![](https://main.qcloudimg.com/raw/690daf43f9b1d5f57b6033720c19860a.png)

>? 
>- Unbinding the recording template will not affect ongoing live streams.
>- To cancel recording for ongoing streams, stop the streams and push them again.

## Modifying a Template

1. Go to **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record) and select **Save to COS**.
2. Select the target recording template and click **Edit** on the right to modify the template information.
3. Click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/eba64793c4ade862606eb5dfaedf6a46.png)

## Deleting a Template

1. Log in to the CSS console, select **Feature Configuration** > [Live Recording](https://console.cloud.tencent.com/live/config/record) on the left sidebar, and click **Save to COS**

2. Select the target recording template, and click **Delete** in the upper right.

3. In the pop-up window, click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/45006e452f7418e894e534d23b0ebc78.png)

>! 
>- If domain names are bound to a template, you need to [unbind](#unite) them before you can delete the template.
>- In the console, recording templates are managed at the domain level. To unbind recording rules bound to streams by APIs, call [DeleteLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30843). 

## More

You can also **unbind** and **bind** domains and recording templates on the **Domain Management** page. For details, see “Recording Configuration”.
