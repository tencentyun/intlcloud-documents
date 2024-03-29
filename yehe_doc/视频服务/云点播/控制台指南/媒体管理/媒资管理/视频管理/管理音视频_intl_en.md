This document describes how to manage audios/videos in the VOD console, including editing basic audio/video information, publishing audios/videos, previewing audios/videos in Player, and generating web player code.

## More Features
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Go to **Media Assets > Video Management > Uploaded**.
4. Click **More** to change the status or storage class of audio/video files or retrieve archived files.

### Changing audio/video status
You can control access to a media file by changing its status.
![](https://qcloudimg.tencent-cloud.cn/raw/8f124e1147f2dead3aed420404912429.jpg)

- **Playback Prohibited**: After the playback of an audio/video is prohibited, error 403 will be returned when resources of the selected asset (including the source file, transcoding result, and screenshots) are requested. You can still play the file in the VOD console.
- **Unblocked**: Click this to unblock an audio/video file and allow users to access the file normally.
>? It takes about 5-10 minutes for the playback prohibiting/unblocking action to fully take effect.

### Changing the storage class
You can change the storage class of a media file on this page. Currently, the following storage classes are supported:

| Storage Class   | STANDARD | STANDARD_IA | ARCHIVE  | DEEP_ARCHIVE   |
| ------ | ---- | ---- | ----- | -------- |
| Default in VOD  | Yes    | No    | No     | No        |
| Storage costs   | High    | Medium    | Low     | Very low       |
| Access performance   | High    | Low    | Not supported | Not supported    |
| Data retrieval fees | No | No | Yes | Yes|
| Supported regions   | All   | All   | All    | Beijing, Shanghai, and Chongqing |
| Minimum billable duration | None | 30 days | 90 days | 180 days |

#### Notes:
1. For files uploaded to VOD (whether using an API, from the SDK, or from the console), the default storage class is STANDARD.
2. For details about storage costs, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/266/14666).
3. Access performance refers to metrics such as **time to first frame (TTFF)** and **stutter rate**. We recommend you do not change the storage class of files that are **frequently accessed**. ARCHIVE and DEEP ARCHIVE files cannot be directly accessed (played or processed). You need to retrieve them first.
4. You can retrieve files from ARCHIVE or DEEP ARCHIVE files to STANDARD. The costs vary depending on the original storage class and retrieval mode.
5. DEEP ARCHIVE is currently available only in Beijing, Shanghai, and Chongqing.
6. **There are minimum storage durations for STANDARD_IA, ARCHIVE, and DEEP ARCHIVE files. Storage fees for the minimum storage duration will be charged even if a file is stored for shorter than the period.**
>?
>- Minimum storage duration for STANDARD_IA files is 30 days. Storage fees for 30 days are charged even if the file is stored for a shorter period.
>- Minimum storage duration for ARCHIVE files is 90 days. Storage fees for 90 days are charged even if the file is stored for a shorter period.
>- Minimum storage duration for DEEP ARCHIVE files is 180 days. Storage fees for 180 days are charged even if the file is stored for a shorter period.
>- If a file is deleted before the minimum storage period elapses, the storage fee will be billed the following day for daily billed users and the following month for monthly billed users.

#### Use limits:
To move a file from ARCHIVE or DEEP ARCHIVE to another storage class, use the data retrieval feature.
>? You will fail to move a file from ARCHIVE or DEEP ARCHIVE to another storage class using the **Change Storage Class** feature.

### Data Retrieval
You can use the data retrieval feature to move files from ARCHIVE or DEEP ARCHIVE to STANDARD. Multiple retrieval modes are supported, which differ in speed and cost. For details about data retrieval fees, see [Data Retrieval](https://intl.cloud.tencent.com/document/product/266/14666).

| Retrieval Mode| From ARCHIVE | From DEEP ARCHIVE |
| ---- | -------- | ---------- |
| Expedited | 5 minutes      | Not supported        |
| Standard | 5 hours      | 24 hours       |
| Bulk | 12 hours     | 48 hours       |

>?
>- A media asset (FileId) may be stored as multiple files, including the original file, transcoding results, and screenshots. The time it takes to retrieve these files may vary. VOD does not keep track of the retrieval progress of each file. Instead, it estimates the time it may take for all the files to be retrieved and denies access to the asset before the time elapses (even if all the files have already been retrieved).
>- Because a media asset may not be marked as retrieved even when it has actually been retrieved, the actual accessible period of the asset may be shorter than expected. Given this, we recommend you set the validity period of assets retrieved from DEEP_ARCHIVE one day longer than you actually need.

## Editing Basic Information
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Go to **Media Assets > Video Management > Uploaded**.
4. Find the target video and click **Manage**. The **Basic Info** page shows a media file’s basic information, standard transcoding list, and adaptive bitrate streaming list.
	- **Basic Info**
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Thumbnail</td>
<td ><ul><li>You can click the edit icon next to the thumbnail image to select an existing image in “Image Management” or upload a local image to use as the thumbnail.<br><li>Only JPG, PNG, and static GIF images are supported.<br><li>The image can be up to 1 MB in size and 1920 x 1080 in dimensions.<br><li>The filename cannot contain Chinese characters.</ul></td>
</tr>
<tr>
<td>Name</td>
<td><ul> <li>You can rename a media file.<br><li>The name can contain up to 20 characters. Double quotation marks ("), single quotation marks ('), less-than signs (<), and greater-than signs (>) are not supported.</ul></td>
</tr>
<tr>
<td>Category</td>
<td><ul><li>You can modify the category of a media file. <br><li>Click the edit icon, select a category, and click **Confirm**.</ul></td>
</tr>
<tr>
<td>Label</td>
<td><ul><li>You can add labels to a media file. <br><li>Each label can be up to 16 characters long and can contain letters and numbers. Press Enter to add multiple labels.</ul></td>
</tr>
<tr>
<td>Description</td>
<td><ul><li>You can add a brief description to a media file.<br><li>The description can be up to 128 characters long.</ul></td>
</tr>
<tr>
<td>Storage Type</td>
<td><ul><li>You can modify the storage class of a media file.<br><li>Click **Storage Type** to move a file from STANDARD to STANDARD_IA or the other way around.</ul></td>
</tr>
</tbody></table>

- **Standard Transcoding List**: The source file and transcoding outputs.
	- You can copy the URL of a file or preview the file.
	- You can also delete a transcoding output file or generate a QR code for sharing.
- **Adaptive Bitrate Streaming List**
	You can copy the URL of a media file, preview the file, and view its details.

## Screenshot Information
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Go to **Media Assets > Video Management > Uploaded**.
4. Find the target media file and click **Manage** to enter the **Basic Info** page.
![](https://qcloudimg.tencent-cloud.cn/raw/179441cd170d27637468e95b932f9799.jpg)
5. Select the **Screenshot Info** tab. This page shows screenshots of the source video as well as processed videos, including animated images, image sprites, sampled screenshots, and time point screenshots.

>? Only the latest 100 entries are displayed. To get the information of all screenshots, click the download icon in the top-right corner.

## Publishing Video
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Go to **Media Assets > Video Management > Uploaded**.
4. Find the target media file and click **Manage** to enter the **Basic Info** page.
![](https://qcloudimg.tencent-cloud.cn/raw/179441cd170d27637468e95b932f9799.jpg)
5. Click **Publish Video** to enter the video publishing page, which displays the source and output video files.


## Player Preview

After transcoding a video to an adaptive bitstream, you can preview it in the player. VOD supports preview in both the **web player** and **client player**.

### Parameter Info
**Playback Configuration**: Displays all the configurations of the player. It comes with two configurations: `default` and `basicDrmPreset`. **To configure your own parameter, you must first [enable key hotlink protection](https://console.cloud.tencent.com/vod/distribute-play/domain) for the primary distribution domain name via the Operation tab.**
![](https://qcloudimg.tencent-cloud.cn/raw/673da72a81f8834f68e8a5e487e1edf3.jpg)


### Configuration items
**Configuration Item**: Shows the configuration items for the selected player configuration.
- If there is an adaptive bitrate stream and image sprite thumbnails for the media asset (file ID), you can preview it using a web player or client player.
- If there isn’t an adaptive bitrate stream or image sprite thumbnails for the media asset (file ID), you will see the following messages:
![](https://qcloudimg.tencent-cloud.cn/raw/762dee1c8d7a1515a0f7e7eebf889465.png)

### Playback control
For a player configuration for which key hotlink protection is enabled, you can set parameters including **playback URL expiration time**, **preview duration**, and **max playback IPs**.
- Playback URL expiration time: The expiration time of the playback URL.
- Preview duration: The preview duration of a video, which must be longer than 30 seconds. If it is left empty, there will be no limit on playback duration.
- Max playback IPs: The maximum number of IP addresses allowed to play the file.

### Video preview
#### Web player

You can click a video to preview it on the web player. You can also copy the code and embed it into a webpage.
![](https://main.qcloudimg.com/raw/36f46c83781ffa90bcf6d432dcbfa079.png)

#### Client player
1. Download the Video Cloud Toolkit App. 
<img src="https://main.qcloudimg.com/raw/4f8138e11bdc92b1286263f1d1f683c4.png" width="400">
2. Use the app to scan the QR code or enter the `appID` and `fileID` manually to preview the video on a client player.



## Web Player Code Generation
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Go to **Media Assets > Video Management > Uploaded**.
4. Find the target media file and click **Manage** to enter the **Basic Info** page.
![](https://qcloudimg.tencent-cloud.cn/raw/179441cd170d27637468e95b932f9799.jpg)
5. Select the **Web Player Code Generation** tab to manage your player information and web player code.
	- Click **Modify** in the **Parameter Settings** area. In the window that pops up, select a player from the drop-down list (for information on player configuration, see [Web Player Management](https://intl.cloud.tencent.com/document/product/266/14056)), and click **Confirm**.
	- In the **Web Player Code** area, choose a video resolution from the **Video Dimension** drop-down list, enable or disable auto playback, and select a code type (**HTML** or **IFRAME**).
6. Click **Copy Code** to copy the generated web player code.
