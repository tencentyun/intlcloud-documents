## Operation Scenarios
The "Video Audit" page displays video audit results, including the results of audit tasks you initiated in "Media Assets" and configured in the task flow.

## Directions

1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and click **Video Audit** on the left sidebar to enter the "Video Audit" page.
![](https://main.qcloudimg.com/raw/226920768d74a5acccbc1393493c1a59.png)
	- Query by time period: video audit results for today, yesterday, last 7 days, and any time period within the last 7 days can be queried in the video audit list.
	- Prefix search: you can search for audit results by `FileId` or video name prefix.
	- Filter: you can sort video files by time in ascending or descending order and filter them by audit status, intelligent audit result, or human verification result.
	- Delete: select the target video files and click **Delete** above the list to delete them in batches. Or, click **Delete** in the row of a single file to delete it directly.
	
>You need to initiate [video audit](https://intl.cloud.tencent.com/document/product/266/33892) in "Media Assets" to get the video audit result.

2. Click **View Result** in the row of the desired video file to enter the "Audit Result" page.
![](https://main.qcloudimg.com/raw/bb204c5235cd38be81c26dd862c55e9e.png)
	- Content display: this page displays the task ID, video filename, source video file URL, intelligent audit result, human verification result, and the details of the intelligent audit result.
	- Copy video information: you can copy the task ID, video filename, and source video file URL.
	- Confirm audit result:
		- Click **Confirm Pass**, which indicates that you confirm that there is no indication of violation in the video and the result of human verification result is "pass".
		- Click **Confirm Violation**, which indicates that you confirm that there is indication of violation in the video and the result of human verification result is "violation".
		- Click **Reaudit** to select another audit template and initiate an audit task again. Or, click **Reaudit** in the row of the target video file on the "Video Audit" page.
	- Audit details: result of video audit by VOD. The internal player only supports **previewing videos in MP4 format**. The audit result details are displayed in the form of tags, and the audit result and segment confidence are displayed based on the specific audit template to help you easily [adjust the confidence threshold](https://intl.cloud.tencent.com/document/product/266/14059#yz).
		




