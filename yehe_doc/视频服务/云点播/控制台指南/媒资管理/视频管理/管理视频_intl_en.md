
This document describes how to manage videos in the VOD console, including editing basic video information, previewing videos in superplayer, and generating web player code.

## More Features
Log in to the [VOD console](https://console.cloud.tencent.com/vod/media) and click **More**. You can get more service capabilities of VOD, such as changing video status, changing storage class, and data retrieval.
### Video Status
You can control the availability of video access by changing its status.
![](https://qcloudimg.tencent-cloud.cn/raw/5ab3bd41d73c1980f2e80fd779a31596.png)

- **Playback Prohibited**: after a video’s playback is prohibited, error 403 will be returned for scenarios accessing the URL of various resources of the video, such as source file, transcoding output files, and screenshots, except for the video’s preview in the VOD console.
- **Unblocked**: you can unblock a video with playback prohibited so as to allow users to access the video normally.
>?It takes about 5-10 minutes for the prohibiting/unblocking to take effect across the entire network.

### Changing Storage Class
You can directly change the video storage class as needed. The following storage classes are currently supported and their characteristics are shown in the table below.

| Storage Class   | STANDARD | STANDARD_IA | ARCHIVE  | DEEP ARCHIVE   |
| ------ | ---- | ---- | ----- | -------- |
| VOD default | Yes | No | No | No | No |
| Storage cost | High | Medium | Low | Very low |
| Access performance | High | Low | Access not supported | Access not supported |
| Data retrieval fees | No | No | Yes | Yes|
| Supported regions | All | All | All | Beijing, Shanghai, Chongqing |
| Minimum billable duration | None | 30 days | 90 days | 180 days |

#### Notes:
1. The default storage class is STANDARD for VOD files uploaded through various upload methods (API/SDK/console).
2. For details about storage costs, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/266/14666).
2. The access of a video will affect metrics such as **first frame broadcasting time** and **stutter rate** when users are watching videos. Therefore, we recommend you not change the storage class **for frequently accessed online business**. ARCHIVE and DEEP ARCHIVE files are not allowed to be accessed directly, for playback, initiating video processing, etc. You need to retrieve a video before you can access it.
4. You can retrieve ARCHIVE and DEEP ARCHIVE files as STANDARD files. The costs incurred vary depending on the source storage class and retrieval mode.
5. DEEP ARCHIVE is currently available only in Beijing, Shanghai, and Chongqing.
6. **STANDARD_IA, ARCHIVE, or DEEP ARCHIVE files must be stored for at least a minimum storage duration, and will still be billed for the minimum storage duration if deleted early.**
>?
>- Minimum storage duration for STANDARD_IA files: 30 days
>- Minimum storage duration for ARCHIVE files: 90 days
>- Minimum storage duration for DEEP ARCHIVE files: 180 days
>- Minimum storage duration for daily billing and monthly billing users: billed the next day and month respectively.

#### Use limits:
Data retrievals are required for changing ARCHIVE or DEEP ARCHIVE files to other storage classes.
>?For videos with use limits, changing its storage class will not take effect.

### Data retrieval capability
You can use data retrievals to change ARCHIVE or DEEP ARCHIVE files to STANDARD files. There are multiple modes for changing storage classes and data retrievals of ARCHIVE or DEEP ARCHIVE files to STANDARD files. These modes can achieve the same results, but differ in speeds and costs, such as data retrieval fees. For details, please see [Purchase Guide - Data Retrievals](https://intl.cloud.tencent.com/document/product/266/14666).

| Restoration Mode| Retrieval from ARCHIVE | Retrieval from DEEP ARCHIVE |
| ---- | -------- | ---------- |
| Expedited | 5 minutes      |  Not supported        |
| Standard | 5 hours      | 24 hours       |
| Bulk | 12 hours     | 48 hours       |

>?
>- The unique `FileId` of a media file can correspond to many stored files, such as the original file, transcoded files, screenshot files, etc. The actual restoration completion time points of such files may vary. Instead of considering the restoration completion status of each file, VOD sees the media files under the same `FileId` as a whole and takes the maximum possible time to estimate the restoration time. Before restoration, these media files are still marked as not restored and access is not allowed, even if sometimes all files under the same `FileId` have actually been restored.
>- As the time point at which the media file is marked as restored will be later than the time when it is actually restored, the restored copies of the media file will be available for a shorter period of time than expected. To ensure that the restored copy has sufficient available time, you’re advised to add an additional 1 day of validity to DEEP ARCHIVE files.

## Editing Basic Info
1. Log in to the VOD console and select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**. The **Uploaded** page is displayed.
2. Find the target video and click **Manage** to enter the **Basic Info** page. You will find the video’s basic information here, including list of standard transcoding source and output files, and list of adaptive bitrate streaming output files:
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
<td>Video Cover</td>
<td ><ul><li>Click </b>Edit</b> on the right of the video thumbnail to select images in </b>Image Management</b>, or to upload a local image.<br><li>Only JPG, PNG, and static GIF images are supported.<br><li>The image can be up to 1 MB in size and 1920 x 1080 in dimensions.<br><li>The filename should not contain Chinese characters.</ul></td>
</tr>
<tr>
<td>Video Name</td>
<td><ul> <li>You can rename the video.<br><li>The video name can contain up to 20 characters and cannot contain double quotation marks ("), single quotation marks ('), less-than signs (<), and greater-than signs (>).</ul></td>
</tr>
<tr>
<td>Category</td>
<td><ul><li>You can modify the video category. <br><li>Click </b>Edit</b>, select a category, and click </b>Confirm</b>.</ul></td>
</tr>
<tr>
<td>Tag</td>
<td><ul><li>You can set tags for the video. <br><li>Set a tag of up to 16 characters (only letters and digits are supported) and then press Enter.</ul></td>
</tr>
<tr>
<td>Overview</td>
<td><ul><li>You can add a brief description to the video.<br><li>The description is up to 128 characters.</ul></td>
</tr>
<tr>
<td>Storage Type</td>
<td><ul><li>You can modify the storage class.<br><li>Click </b>Storage Type</b> to modify. Switching between STANDARD and STANDARD_IA is supported.</ul></td>
</tr>
</tbody></table>
	
	- **Standard Transcoding List**: lists the source and output video files.
		- You can copy the URL of a video file and preview it.
		- You can also delete an output video file or share it via QR code.
	- **Adaptive Bitrate Streaming List**
	You can copy the URL of a video file, preview it, and view its details.
	
## Screenshot Information

1. Log in to the VOD console and select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**. The **Uploaded** page is displayed.
2. Find the target video and click **Manage** to enter the **Basic Info** page.
3. Select the **Screenshot Info** tab. It displays a list of original videos and screenshot files of the processed videos, including generated animated images, image sprites, sampled screenshots, and point-in-time screenshots.

>?Only the latest 100 entries of screenshot information are displayed. To get the information of all screenshots, click the download icon in the top-right corner.


## Superplayer Preview
>!Superplayer only supports previewing adaptive bitrate streaming videos. If you want to quickly generate videos for the superplayer, please see [Superplayer Guide](https://intl.cloud.tencent.com/document/product/266/38098).

After transcoding a video to an adaptive bitrate streaming file, you can preview it in superplayer. VOD supports preview on both the **web player** and **client player**.

### Parameter Info
**Playback Configuration**: displays all the configurations of the superplayer. It comes with two configurations: `default` and `basicDrmPreset`. To configure your own parameter, you must first [enable key hotlink protection](https://console.cloud.tencent.com/vod/distribute-play/domain) for the primary distribution domain name via the Operation tab.
![](https://qcloudimg.tencent-cloud.cn/raw/e46e31631d7a92cbe12cb0d015364951.png)


### Configuration Item
**Configuration Item**: shows the selected playback configuration items.
- **Adaptive bitrate streaming template for playback**: specifies an adaptive bitrate streaming template for your current player to preview videos transcoded by the template.
- **Image sprite template for thumbnail preview**: specify an image sprite template for the player to preview image sprites generated by the template.
![](https://qcloudimg.tencent-cloud.cn/raw/762dee1c8d7a1515a0f7e7eebf889465.png)

### Playback control
Playback configuration (for domain name with key hotlink protection enabled): you can set the parameters of **playback URL expiration time**, **preview duration**, and **maximum number of playback IPs**.
- Playback URL Validity: specify the expiration time of the video URL.
- Preview duration: specify the preview duration of a video, which must be more than 30 seconds. If it is left empty, there will be no limit on playback duration.
- Maximum number of playback IPs: specify the maximum number of IPs allowed for playback.

### Video preview
#### Web player

You can click a video to preview it on the web player. You can also copy the code and embed it into a webpage.
![](https://main.qcloudimg.com/raw/36f46c83781ffa90bcf6d432dcbfa079.png)

#### Client player
1. Download the Video Cloud Toolkit App.
<img src="https://main.qcloudimg.com/raw/4f8138e11bdc92b1286263f1d1f683c4.png" width="400">
2. Use the Video Cloud Toolkit to scan the QR code or enter the `appID` and `fileID` to preview the video on the client device.



## Web Player Code Generation
1. Log in to the VOD console and select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**. The **Uploaded** page is displayed.
2. Find the target video and click **Manage** to enter the **Basic Info** page.
3. Select the **Web Player Code Generation** tab to manage your player information and web player code.
	- Click **Modify** in the **Parameter Settings** section, and the **Modify Player** dialog box will pop up. Select a configured player from the drop-down list (for more information on player settings, please see [Web Player Management](https://intl.cloud.tencent.com/document/product/266/14056)), and click **Confirm**.
	- In the **Web Player Code** section, you can choose an appropriate video resolution from the **Video Dimension** drop-down list, enable or disable auto playback, and set **HTML** or **IFRAME** as the code type.
4. Click **Copy Code** to copy the generated web player code.



