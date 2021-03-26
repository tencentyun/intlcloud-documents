<span id="que1"></span>
### How does LVB recording work?
![img](https://main.qcloudimg.com/raw/8fb1f0b9bcc3ab299b99d6c75859c13f.png)

When you enable the recording for a live stream, the audio/video data is relayed to the recording system. Every frame pushed from the host's mobile phone is written into the recording file by the recording system.

If an LVB push is interrupted, the access layer will immediately notify the recording server to record the file being written, store it into the VOD system, and generate an index. Then, you can find the new recording file in the VOD system. If you have configured recording event notification on a server, the recording system will send the **index ID** and **online playback address** to the server.

However, an error will occur in the processes of transferring and processing a large file on the cloud. To ensure success, the maximum recording length of a file is 120 minutes, and you can specify a shorter segment by using the `RecordInterval` parameter.

<span id="que2"></span>
### Why is LVB recording not available? 
The playback feature of LVB recording relies on Tencent Cloud's **VOD service**. If you want to use this feature, you need to [activate VOD](https://console.cloud.tencent.com/vod) first in the Tencent Cloud console. 

<span id="que3"></span>
### How soon will the recording file be ready after the live streaming is over? 
You may get the recording file in about 5 minutes after the live streaming is over. An event callback will be triggered when the recording ends, which provides accurate recording completion time. For more information, please see [Callback Configuration](https://intl.cloud.tencent.com/document/product/267/31074).

<span id="que4"></span>
### Can I migrate an LVB video?
You can use the download address of the video to migrate it. 

<span id="que5"></span>
### How do I set the video storage period?
LVB currently has no limit on the video storage period. You can manage video files through the console and RESTful APIs. 

<span id="que6"></span>
### How many recording files are generated in an LVB recording process?

- **Recoding in MP4, FLV, or AAC format:** the recording length of a file can be 5–120 minutes. You can specify a shorter segment by using the `RecordInterval` parameter of the [CreateLiveRecordTemplate API](https://intl.cloud.tencent.com/document/product/267/30845).
	- If the duration of a live stream is very short and the push ends before the recording module starts, the system will not be able to generate a recording file.
	- If the duration of a live stream is not long (shorter than `RecordInterval`), and the push is not interrupted during the live stream, only one recording file is generated.
	- If the duration of a live stream is very long (longer than `RecordInterval`), the video will be segmented based on the length of time specified by `RecordInterval`, to avoid the time uncertainty of the flow of the file with a longer duration in a distributed system.
	- If the push is interrupted during a live stream (SDK will re-push later), a new segment will be generated every time the interruption occurs.

- **Recording in HLS format:** there is no upper limit. After the resuming timeout period (which can be set to 0–1800s) elapses, a new file will be created to continue recording.

<span id="que7"></span>
### How do I know which files belong to a certain live stream?

Actually, Tencent Cloud as PaaS does not know how you defined one live stream. If one of your live streams lasted for 20 minutes, during which a push interruption caused by network switching occurred, and the live stream was stopped and restarted once manually. For common mobile live streaming, we generally define the period between the two time points as shown below as one live stream.

Therefore, the time information sent from the application client is important. If you want to define that all the files recorded during this period belong to this live stream, you just need to retrieve the recording notification you received by using LVB codes and time information (each recording notification event comes with the stream ID, start time, and end time).

<span id="que8"></span>
### How do I splice segments?
Tencent Cloud supports splicing video fragments with a TencentCloud API. For more information on how to use this API, please see [Edit Media](https://intl.cloud.tencent.com/zh/document/product/266/34126). 

<span id="que9"></span>
### How do I troubleshoot when only one recording template is set but two recording streams exist? 
In general, this might be because there are two recording tasks under the current push domain name. We recommend you troubleshoot in the following ways:

1. Check the recording configuration in the console. Make sure that only one format is selected as the recording file type.
   - If you use the new console, go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click **Manage** on the right of the desired push domain name, select **Template Configuration**, and view the "Recording Format" of the bound template in the **Recording Configuration** tab.
   - If you use the legacy console, go to **[LVB Code Access](https://console.cloud.tencent.com/live/livecodemanage)** > **Access Configuration** to view the recording configuration.	
2. You can use one of the following methods to record: [create a recording task](https://intl.cloud.tencent.com/zh/document/product/267/37309) or [create a recording template](https://intl.cloud.tencent.com/document/product/267/34223). If you create both a recording template and a recording task for the same live stream, it will be recorded repeatedly. Please check whether a recording task has been enabled in the console and another recording task has been enabled by [CreateLiveRecord](https://intl.cloud.tencent.com/zh/document/product/267/37309) (API 3.0).

> ! 
> - If you enabled LVB recording in the legacy console but want to disable it in the new console, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). 
> - If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.






