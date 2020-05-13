
This document describes how to manage videos in the VOD Console, including editing basic video information, publishing videos, previewing videos in superplayer, and generating web player code.

## Basic Information Editing
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and click **Media Assets** on the left sidebar to enter the "Uploaded" page by default.
2. Click **Manage** in the row of the desired video file to enter the "Basic Info" page by default which displays the basic video information, list of standard transcoding output files, and list of adaptive bitrate streaming output files:
	- **Basic information**
	Click **Edit** in the top-right corner to edit the following fields of basic video information:
	<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Video cover</td>
<td ><ul><li>Click **Change Image** to select and upload a local image. <br><li>Only JPG, PNG, and static GIF images are supported. <br><li>The image can be up to 1 MB in size and 1920 * 1080 px in dimensions. <br><li>The filename cannot contain Chinese characters. </ul></td>
</tr>
<tr>
<td>Video name</td>
<td><ul> <li>You can rename the video.<br><li>The name can contain up to 20 characters and cannot contain double quotation marks ("), single quotation marks ('), less-than signs (<), or greater-than signs (>). </ul></td>
</tr>
<tr>
<td>Category</td>
<td><ul><li>You can modify the video category. <br><li>Click **Modify Category**, select a category, and click **OK**.</ul></td>
</tr>
<tr>
<td>Tag</td>
<td><ul><li>You can set a tag for the video. <br><li>Set a tag of up to 16 letters and digits and press Enter.</ul></td>
</tr>
<tr>
<td>Overview</td>
<td><ul><li>You can add a brief description to the video. <br><li>The description can contain up to 128 characters.</ul></td>
</tr>
</tbody></table>
	- **List of standard transcoding output files**: it lists the source and output video files.
		- You can copy the URL of a video file and preview it.
		- You can also delete an output video file and share it through QR code.
	- **List of adaptive bitrate streaming output files**
	You can copy the URL of a video file, preview it, and view its details.
	


## Video Release
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and click **Media Assets** on the left sidebar to enter the "Uploaded" page by default.
2. Click **Manage** in the row of the desired video file to enter the "Basic Info" page by default.
3. Click **Video Release** to enter the "Video Release" page which displays the source and output video files.
	
	
## Superplayer Preview
>Superplayer only supports preview of videos processed with adaptive bitrate streaming.

After transcoding a video to adaptive bitstream, you can preview it in superplayer. VOD supports preview in **web player** and **terminal player**.

### Web player

Click **Preview** to preview the video directly on the web.
<!--![](https://main.qcloudimg.com/raw/552486ddf1dd389b3130f1c8618b246d.png)-->

### Terminal player
1. Download the Video Cloud Toolkit app.

<img src="https://main.qcloudimg.com/raw/4f8138e11bdc92b1286263f1d1f683c4.png" width="400">

2. Use the Video Cloud Toolkit to scan the QR code or enter the `appID` and `fileID` to preview the video on the terminal device.



## Web Player Code Generation
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and click **Media Assets** on the left sidebar to enter the "Uploaded" page by default.
2. Click **Manage** in the row of the desired video file to enter the "Basic Info" page by default.
3. Click **Web Player Code Generation** to enter the "Web Player Code Generation" page where you can manage player information and web player code.
	- In the "Parameter Settings" section, click **Modify** and the "Modify Player" dialog box will pop up. Select a configured player in the player drop-down list (for more information on player settings, please see [Web Player Management](https://intl.cloud.tencent.com/document/product/266/14056)), and click **OK**.
	- In the **Web Player Code** section, you can choose the appropriate video resolution in the "Video Resolution" drop-down list, enable or disable autoplay as needed, and set **HTML** or **IFRAME** for code type.
4. Click **Copy Code** to copy the generated web player code.


