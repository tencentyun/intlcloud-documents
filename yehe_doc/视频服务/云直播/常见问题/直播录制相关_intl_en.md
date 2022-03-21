<span id="que1"></span>
### How does live recording work?
![img](https://main.qcloudimg.com/raw/9c9d31c6ffec97d2b8b4042b7a673cbc.jpg)

When you enable the recording for a live stream, the audio/video data is relayed to the recording system. Every frame pushed from the host’s mobile phone is written into the recording file by the recording system.

If a live push is interrupted, the access layer will immediately notify the recording server to record the file being written, store it into the VOD system and generate an index. Then, you can find the new recording file in the VOD system. If you have configured recording event notification on a server, the recording system will send the **index ID** and **online playback URL** to the server.

However, an error will occur in the processes of transferring and processing a large file on the cloud. To ensure success, the maximum recording length of a file is 120 minutes, and you can specify a shorter segment using the `RecordInterval` parameter.

<span id="que2"></span>
### Why is live recording not available? 
Live recording and playback is built on Tencent Cloud's **VOD** service. To use this feature, you need to [activate VOD](https://console.cloud.tencent.com/vod) in the Tencent Cloud console.

<span id="que3"></span>
### How soon will the recording file be ready after the live streaming is over? 
You may get the recording file in about 5 minutes after the live streaming is over. An event callback will be triggered when the recording ends, which provides accurate recording completion time. For more information, please see [Callback Configuration](https://intl.cloud.tencent.com/document/product/267/31074).

<span id="que4"></span>
### After live recording is completed, how do I get the recording files?
The generated recording files are automatically stored in the VOD system. After you have activated VOD, you can get the recording files in the following ways:
- [VOD console](https://intl.cloud.tencent.com/document/product/267/31563#vod-console)
- [Recording event notification](https://intl.cloud.tencent.com/document/product/267/31563#recording-event-notification)
- [VOD APIs](https://intl.cloud.tencent.com/document/product/267/31563#vod-api-query)

<span id="que5"></span>
### Can I migrate a CSS video?
You can use the download address of the video to migrate it. 

<span id="que6"></span>
### How do I set the video storage period?
CSS currently has no limit on the video storage period. You can manage video files through the console and RSETful APIs. 

<span id="que7"></span>
### How many recording files are generated in an live recording process?
- **Recording a file in MP4, FLV or AAC format**: the maximum recording length of a single file ranges from 5 to 20 minutes. You can specify a shorter segment using the `RecordIntervall` parameter of the [CreateLiveRecordTemplate API](https://intl.cloud.tencent.com/document/product/267/30845).
	- If the duration of a live stream is so short that the push ends before recording is enabled, no recording file will be generated.
	- If the duration of a live stream is not long (shorter than `RecordInterval`), and the push is not interrupted during the live stream, only one recording file is generated.
	- If the duration of a live stream is very long (longer than `RecordInterval`), the video will be segmented based on the length of time specified by `RecordInterval`, to avoid the time uncertainty of the flow of the file with a longer duration in a distributed system.
	- If the push is interrupted during a live stream (SDK will re-push later), a new segment will be generated every time the interruption occurs.

- **Recording a file in HLS format**: there is no upper limit. If a file exceeds the recording resumption timeout period, a new file will be created to continue recording. You can set the recording resumption timeout period to 0-1800 seconds.

<span id="que9"></span>
### How do I splice segments?
You can splice segments by using the TencentCloud APIs. 

<span id="que10"></span>
### How do I troubleshoot when only one recording template is set but two recording streams exist? 
In general, this might be because there are two recording tasks under the current push domain name. We recommend troubleshooting in the following ways:

1. Check the recording configuration in the console. Make sure that only one format is selected as the recording file type.
   - If you use the new console, go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click **Manage** on the right of the desired push domain name, select **Template Configuration**, and view the "Recording Format" of the associated template in the **Recording Configuration** section.
2. You can use one of the following methods to record: [create a recording task](https://intl.cloud.tencent.com/document/product/267/30847) or [create a recording template](https://intl.cloud.tencent.com/document/product/267/34223). If you create both recording templates and recording tasks for the same live stream, it will be recorded repeatedly. Check whether a recording task has been enabled in the console and another recording task has been enabled by [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/30847) (API v3.0).

> ! If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).






