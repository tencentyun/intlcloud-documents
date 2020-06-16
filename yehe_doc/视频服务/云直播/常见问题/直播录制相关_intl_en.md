<span id="que1"></span>
### How does LVB recording work?
![img](https://main.qcloudimg.com/raw/9c9d31c6ffec97d2b8b4042b7a673cbc.jpg)

When you enable the recording for an LVB stream, the audio/video data is relayed to the recording system. Every frame pushed from the host’s mobile phone is written into the recording file by the recording system.

If an LVB push is interrupted, the access layer will immediately notify the recording server to record the file being written, store it into the VOD system and generate an index. Then you can find the new recording file in the VOD system. If you have configured recording event notification on a server, the recording system will send the **index ID** and **online playback URL** to the server.

However, an error will occur in the processes of transferring and processing a large file on the cloud. To ensure success, the maximum recording length of a file is 120 minutes, and you can specify a shorter fragment using the `record_interval` parameter.

<span id="que2"></span>
### Why is the LVB recording not available? 
LVB recording and replay is built on Tencent Cloud's **VOD service**. To use this feature, you need to [activate VOD](https://console.cloud.tencent.com/vod) in the Tencent Cloud console.

<span id="que3"></span>
### How soon will the recording file be ready after the live streaming is over? 
You may get the recording file in about 5 minutes after the live streaming is over. An event callback will be triggered when the recording ends, which provides accurate recording completion time. For more information, please see [Callback Configuration](https://intl.cloud.tencent.com/document/product/267/31074).

<span id="que4"></span>
### After LVB recording is completed, how do I get the recording files?
The generated recording files are automatically stored in the VOD system. After you have activated VOD, you can get the recording files in the following ways:
- [VOD Console](https://intl.cloud.tencent.com/document/product/267/31563)
- [Recording Event Notification](https://intl.cloud.tencent.com/document/product/267/31563)
- [VOD APIs](https://intl.cloud.tencent.com/document/product/267/31563)

<span id="que5"></span>
### Can I migrate an LVB video?
You can use the download address of the video to migrate it. 

<span id="que6"></span>
### How do I set the video storage period?
LVB currently has no limit on the video storage period. You can manage video files through the console and RSET APIs. 

<span id="que7"></span>
### How many recording files are generated in an LVB recording process?
The maximum recording length of a file is 120 minutes. You can specify a shorter fragment using the `record_interval` parameter of the [`CreateLiveRecordTemplate` API](https://intl.cloud.tencent.com/document/product/267/30845). 

- If the duration of a live stream is too short (for example, shorter than 1 second), no recording file is generated.
- If the duration of a live stream is not long (shorter than `record_interval`), and the push is not interrupted during the live stream, only one recording file is generated.
- If the duration of a live stream is very long (longer than `record_interval`), the video will be fragmented based on the length of time specified by `record_interval`, to avoid the time uncertainty of the flow of the file with a longer duration in a distributed system.
- If the push is interrupted during a live stream (SDK will re-push later), a new fragment will be generated every time the interruption occurs.

<span id="que8"></span>
### How do I stitch fragments?
You can stitch fragments by using the Tencent Cloud APIs. 

