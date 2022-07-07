[](id:que1)
### How does live recording work?
![img](https://main.qcloudimg.com/raw/9c9d31c6ffec97d2b8b4042b7a673cbc.jpg)

After you enable recording for a live stream, each audio/video frame published from the host’s mobile phone will be relayed to the recording system and written into a recording file.

When a live stream is interrupted, the access layer will immediately request the recording server to end the writing process, save the generated files to VOD, and generate an index for the file. You can then find the recording file in VOD. If you have configured the recording callback, the recording system will send the **index ID** and **playback URL** to the server you specified.

If a file is too large, errors may occur while the file is being transferred and processed in the cloud. As a result, to ensure the success of recording, we have capped the duration of a single recording file at 120 minutes. You can record shorter video segments by setting the `RecordInterval` parameter to a smaller value.

[](id:que2)
### Why can't I use the live recording feature? 
The live recording feature relies on Tencent Cloud's **VOD service**. To use this feature, you need to [activate VOD](https://console.cloud.tencent.com/vod) first. For more information, see [Recording and Replay](https://intl.cloud.tencent.com/document/product/1071/41868).

[](id:que3)
### When will the recording file be ready after a live stream ends? 
The recording file is ready when you receive the recording callback ( about 5 minutes after a live stream ends). For more information, see [Live Stream Callback](https://intl.cloud.tencent.com/document/product/267/31074).

[](id:que4)
### How do I get recording files?
Recording files are saved to VOD, so you need to activate VOD first. You can get recording files in the following ways:
- [VOD console](https://intl.cloud.tencent.com/document/product/267/31563)
- [Recording event notification](https://intl.cloud.tencent.com/document/product/267/31563)
- [Query by VOD API](https://intl.cloud.tencent.com/document/product/267/31563)

[](id:que5)
### Can I migrate my videos?
To migrate your videos, you need to get the download addresses and download your videos. 

[](id:que6)
### How do I set the video storage period?
CSS does not set a limit on the video storage period. You can manage your video files in the console or via RESTful APIs. 

[](id:que7)
### How many recording files are generated for a live stream?
- **Recording in MP4, FLV, or AAC format**: A single recording file can be 1 to 120 minutes long. You can specify a shorter maximum duration by setting the `RecordInterval` parameter of the [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) API.
  - If a live stream is so short that it ends before the recording module is started, no recording files will be generated.
  - If a live stream is shorter than `RecordInterval` and is not interrupted, only one recording file will be generated.
  - If a live stream lasts longer than `RecordInterval`, the stream will be recorded into multiple files. This is to reduce the uncertainty of a file’s transfer time in a distributed system.
  - If a live stream is interrupted and resumed, a new recording file will be generated each time an interruption occurs.
- **Recording in HLS format**: There is no upper limit on the duration of recording files. However, if a live stream is interrupted and the timeout period for breakpoint resumption (which can be set to 0-1800s) elapses, a new recording file will be generated.

[](id:que8)
### How do I know which live stream a recording file belongs to?

It depends on how you define a live stream. Assume that a host streamed for 20 minutes, but the stream was interrupted twice, once due to network change and once manually by the host. Does this count as one or three live streams?

In most mobile live streaming scenarios, we consider the period from when a host starts live streaming to when they end it as one live stream.

If you use the above standard, to determine which live stream a recording file belongs to, just search for recording notifications by live stream code and time. Each recording notification carries information including **stream ID**, **start time**, and **end time**.

[](id:que9)
### How do I splice the recording files of a live stream?
You can use a cloud API to splice recording files. 

[](id:que10)
### Why are there two recording channels when I have configured only one recording template? 
This is usually because two recording tasks are initiated for the push domain. Check the following:

1. Check in the console whether you have selected two recording formats.
   - If you use the new console, select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar, find your push domain, click **Manage** on the right to enter the details page, and select **Template Configuration** to view your recording configuration.
   - If you use the legacy console, go to **[Live Stream Code Access](https://console.cloud.tencent.com/live/livecodemanage)** > **Access Configuration** to view the recording configuration.  
2. Make sure you haven’t called the 3.0 API [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) or 2.0 API Live_Tape_Start to start a recording task at the same time. You can either call the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API or [create a recording template](https://intl.cloud.tencent.com/document/product/267/34223) in the console to start recording. If you create a recording task and configure a recording template for a live stream at the same time, it will be recorded twice.

> ! 
>- If you enabled live recording in the legacy console and want to disable it in the new console, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). 
>- If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

[](id:que11)
### How do I record audio only?	
If you record the streams of a specific room, add the following parameter to the end of your push URL:
- **Audio only**: `record_type=audio`
- **Video**: `record_type=video`

If you want both video and audio-only files, you can record videos first and then transcode the video files to audio files in VOD.

[](id:que12)
### How do I save my videos permanently?
Set the storage period in your recording template to 0. For details, see [Live Recording](https://intl.cloud.tencent.com/document/product/267/34223).

[](id:que13)
### Can CSS automatically remove the beginning and end of a recording file?
No, because the player is not able to identify the beginning and end of a video. Instead, you can use the following methods:
- Trim the recorded videos. For details, see [EditMedia](https://intl.cloud.tencent.com/document/product/266/34126).
- Adjust the playback progress.

[](id:que14)
### How can I recover my live streaming content if I forget to record it?
Tencent Cloud does not record your content without your request, so you cannot recover the content. This is the case with most cloud service providers.



