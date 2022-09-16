This document describes how to change the fields displayed in the audio/video list and export the list from the VOD console.

## Customizing the Audio/Video List


1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Go to **Media Assets > Video/Audio Management > Uploaded**
4. Click ![](https://main.qcloudimg.com/raw/f4d3608e1d8319051883e90226a86f50.png) in the top right of the list, select the fields you want to display, and click **Confirm**. You can select up to 14 fields. **Video Name/ID** and **Operation** are selected by default.
![](https://qcloudimg.tencent-cloud.cn/raw/473896085055dc9a382e363cec4db9dc.png)



## Exporting the Audio/Video List

1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Go to **Media Assets > Video/Audio Management > Uploaded**
4. Click ![](https://main.qcloudimg.com/raw/e530c6f8adeb603d98e1bc7e0ae8e255.png) in the top right of the list, select an export format and the export data, and click **Confirm**. **Export All File Info** is selected by default.
![](https://qcloudimg.tencent-cloud.cn/raw/c390702b9e17fb783cae7e8047873e22.png)
5. You can choose to export the information of selected files or all files in CSV or JSON Lines format.
 1. A CSV (Character Separated Values) file is a plain text file that stores table information. Below is an example of an exported CSV file:
 ![](https://qcloudimg.tencent-cloud.cn/raw/858c2dac0136337f560d52833921ff00.png)
<table>
   <tr>
      <th width="120px" style="text-align:center">File Format</td>
      <th width="0px" style="text-align:center">Fields (In Specified Order)</td>
   </tr>
   <tr>
      <td>CSV</td>
      <td>Media file name, creation time, last updated time, expiration time, category ID, category name, category path, thumbnail URL, source, storage, labels, live recording file (VID), file URL, file ID, file size, duration</td>
   </tr>
</table>
 5. The JSON Lines format is used to store structured data that can be processed one record at a time. An exported JSON Lines file contains the following fields:
 <table>
   <tr>
      <th width="120px" style="text-align:center">File Format</td>
      <th width="0px" style="text-align:center">Field</td>
      <th width="0px"  style="text-align:center">Description</td>
   </tr>
   <tr>
      <td rowspan='12'>JSON Lines</td>
      <td>BasicInfo</td>
      <td>Basic information such as file name, category, playback URL, and thumbnail</td>
   </tr>
   <tr>
      <td>MetaData</td>
      <td>Metadata, such as size, duration, video stream information, and audio stream information</td>
   </tr>
   <tr>
      <td>TranscodeInfo</td>
      <td>Transcoding output information, including the URLs, specifications, bitrates, and resolutions of the files generated</td>
   </tr>
   <tr>
      <td>AnimatedGraphicsInfo</td>
      <td>The output information of animated image generation</td>
   </tr>
   <tr>
      <td>SampleSnapshotInfo</td>
      <td>Sampled screenshot information</td>
   </tr>
   <tr>
      <td>ImageSpriteInfo</td>
      <td>Image sprite information</td>
   </tr>
   <tr>
      <td>SnapshotByTimeOffsetInfo</td>
      <td>Time point screenshot information</td>
   </tr>
   <tr>
      <td>KeyFrameDescInfo</td>
      <td>Video keyframe descriptions</td>
   </tr>
   <tr>
      <td>AdaptiveDynamicStreamingInfo</td>
      <td>Adaptive bitrate streaming information</td>
   </tr>
   <tr>
      <td>SubtitleInfo</td>
      <td>Subtitle information</td>
   </tr>
   <tr>
      <td>FileId</td>
      <td>The unique ID of a media file</td>
   </tr>
</table>
