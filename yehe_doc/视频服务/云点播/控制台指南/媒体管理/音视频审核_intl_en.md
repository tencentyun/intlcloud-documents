## Overview
The **Audio/Video Moderation** page displays audio/video moderation results, including the results of moderation tasks you initiated in **Video Management** and configured in the task flow.

## Directions

1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. By default, you will enter the **Media Assets > Video Management > Uploaded** page.
![](https://qcloudimg.tencent-cloud.cn/raw/aefccb09bebcd2aa3e79b0c8f58e94c5.png)

	- Query by time period: Audio/Video moderation results for today, yesterday, past 7 days, and any time period within the past 7 days can be queried in the audio/video moderation list.
	- Prefix search: You can search for moderation results by `FileId` or video name prefix.
	- Filter: You can sort video files by time in ascending or descending order and filter them by moderation status, intelligent moderation result, or human verification result.
	- Delete: Select the target video files and click **Delete** above the list to delete them in batches. Alternatively, click **Delete** in the row of a single file to delete it.
	
>?You need to initiate an [audio/video moderation](https://intl.cloud.tencent.com/document/product/266/33892) task in **Video Management** to view audio/video moderation results.

2. Click **View Result** in the row of the video file to go to the moderation result page.
![](https://qcloudimg.tencent-cloud.cn/raw/fcf31a23f67809fbec7ded67a01f7be9.png)
	- Content display: This page displays the task ID, video filename, source video file URL, intelligent moderation result, human verification result, and the details of the intelligent moderation result.
	- Copy video information: You can copy the task ID, video filename, and source video file URL.
	- Confirm moderation result:
		- Click **Confirm Pass**, which indicates that you confirm that there is no indication of a violation in the video and the result of human verification result is "Passed".
		- Click **Confirm Violation**, which indicates that you confirm that there is indication of a violation in the video and the result of human verification result is "Violated".
		- Click **Moderate Again** to select another moderation template and initiate a moderation task again. Or, click **Moderate Again** in the row of the target video file on the **Audio/Video Moderation** page.
	- Moderation details: Result of video moderation by VOD. The internal player only supports **previewing videos in MP4 format**. The moderation result details are displayed in the form of tags, and the moderation result and segment confidence are displayed based on the specific moderation template to help you easily [adjust the confidence threshold](https://intl.cloud.tencent.com/document/product/266/14059).
		

