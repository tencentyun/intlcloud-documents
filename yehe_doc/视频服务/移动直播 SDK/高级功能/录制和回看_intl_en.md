## Feature Overview
The recording and playback features allow you to record live streams and play them to users on demand.

Your application may have a relatively small number of hosts at the early stage. Playback can enrich the content your application provides to audience at this stage. Even after your hosts grow to a considerable scale, having a library of high-quality content is still essential. Videos of past streams also make up an important part of a host’s profile.

## Enabling Recording
The recording and playback features are built on Tencent Cloud's **VOD service**. Therefore, to use the recording feature, you need to activate [VOD](https://console.cloud.tencent.com/vod) in the console. After that, you can find recorded videos in [Video Management](http://console.cloud.tencent.com/vod/media) of the VOD console.

Follow the steps below to enable the recording feature.
>? 
>- You can record live streams using an API. For more information, see [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309).
>- Recorded videos are automatically stored in the VOD platform. Therefore, to use the recording feature, you need to activate VOD and purchase storage and traffic packages to store and play back recorded videos. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/266/8757).

#### Directions
In the CSS console, go to **Feature Configuration** > **[Live Recording](https://console.cloud.tencent.com/live/config/record)** and click **Create Recording Template**. After configuration, click **Save**. For detailed instructions, please see the "Creating a Recording Template" section in [CSS Recording](https://intl.cloud.tencent.com/document/product/267/34223).
![](https://qcloudimg.tencent-cloud.cn/raw/87d63f524398a0af69f520002412a2ef.png)

<table>
<tr><th colspan=2 width=25%>Item</th><th>Description</th></tr><tr>
<td colspan=2>Max Recording Time Per File</td>
<td><ul style="margin:0"><li>There is no upper limit on the recording time of a file in HLS format. If a live stream is interrupted and the timeout period for resumption elapses, a new recording file will be generated to continue recording.</li><li>The allowed duration of a file recorded in MP4, FLV, or AAC format is 1-120 minutes. </li></ul></td>
</tr><tr>
<td colspan=2>Resumption Timeout</td>
<td>Only the HLS format supports recording resumption after interruption, and the timeout period for resumption can be set between 0 and 1800 seconds.</td>
<td></td>
</tr><tr>
<td colspan=2>Storage Period (day)</td>
<td>You can select <b>Permanent</b> to save a recording file permanently or <b>Custom</b> to specify a storage period (up to 1,500 days). Setting the period to `0` means to save recording files permanently.</td>
</tr><tr>
<td colspan=2>VOD Subapplication/Category</td>
<td>By default, streams are recorded to the primary application in VOD. You can also record them to a category of a writable <a href="https://console.cloud.tencent.com/vod/enable-subapp">subapplication</a>.</td>
<td></td>
</tr>
<tr>
<td rowspan=2>Advanced Configuration</td>
<td>Storage Policy</td>
<td>Select STANDARD_IA (cold storage) if the recording files will not be accessed frequently or will be stored for a long period of time, and select STANDARD (default) if the recording files need to be played back for business purposes.
<ul style="margin:0">
<li>If you select <b>Standard</b> and cold storage is enabled for the selected application/category, streams will be recorded to standard storage first before the configured cold storage policy is executed on the recording files. You can view your cold storage policies in the <a href="https://console.cloud.tencent.com/vod/inactivation">console</a>.</li>
<li>If you select <b>STANDARD_IA</b> and cold storage is enabled for the selected application/category, streams will be recorded to STANDARD_IA storage first, and the system will then determine whether to execute the cold storage policy.</li>
</ul>
</td>
</tr><tr>
<td>VOD Task Flow</td>
<td>Click <b>Select</b> to bind a task flow created under the VOD subapplication. You can also click a task flow to go to the VOD console, where you can modify the task flow or create new ones. The bound task flow will be executed on recording files upon generation, for which you will be charged <a href="https://intl.cloud.tencent.com/document/product/266/2838">VOD fees</a>.</td>
</tr></table>




#### Binding domain name
After creating a recording template, in the CSS console, select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click a publishing domain to go to the details page, select **Template Configuration**, click **Edit** in the **Recording Configuration** section to bind the domain name to the template created, and click **save**. For detailed directions, please see [Binding a Template with Domain Names](https://intl.cloud.tencent.com/document/product/267/34224).
![](https://qcloudimg.tencent-cloud.cn/raw/46e8692bfae204432c56a5d6f72522c5.png)

## Getting Files
Playback URLs are generated for new recording files. You can use them to enable various additional features for your application based on your business needs.

For example, you can add the playback URLs of a host’s past live streams to his or her profile. You can also select high-quality content from past live streams and recommend it to your users in a playback list.

There are two methods to get recording files.

### Method 1: listening for notifications

Register a callback URL on your server and provide it when [configuring callbacks](https://intl.cloud.tencent.com/document/product/267/31074) with Tencent Cloud. Tencent Cloud will notify you of the generation of new recording files via the URL.

In the CSS console, select **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)**, click **Create Callback Template**, fill in the callback information, and click **Save**. For detailed directions, see [Creating a Callback Template](https://intl.cloud.tencent.com/document/product/267/31074#Callback).
![](https://qcloudimg.tencent-cloud.cn/raw/db3107a8981479b82f2f1d611e21e770.png)

**Binding a domain name to the template**
After creating a callback template, select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click a publishing domain name to go to the details page, select **Template Configuration**, click **Edit** in the **Callback Configuration** section to bind the domain name to the template created, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/1e15650eb0d482e255b1bc554c9ae307.png)
Below is a typical notification message. It indicates that a new FLV recording file with the ID `9192487266581821586` has been generated, and the playback URL is `http://200025724.vod.myqcloud.com/200025724_ac92b781a22c4a3e937c9e61c2624af7.f0.flv`.
```json
{
    "channel_id": "2121_15919131751",
    "end_time": 1473125627,
    "event_type": 100,
    "file_format": "flv",
    "file_id": "9192487266581821586",
    "file_size": 9749353,
    "sign": "fef79a097458ed80b5f5574cbc13e1fd",
    "start_time": 1473135647,
    "stream_id": "2121_15919131751",
    "t": 1473126233,
    "video_id": "200025724_ac92b781a22c4a3e937c9e61c2624af7",
    "video_url": "http://200025724.vod.myqcloud.com/200025724_ac92b781a22c4a3e937c9e61c2624af7.f0.flv"
}
```

### Method 2: querying in the console or via an API
Recording files are saved automatically in the VOD system after generation. You can view recording files in the VOD console or query files using a VOD API. For details, please see [Obtaining Recording Files](https://intl.cloud.tencent.com/document/product/267/31563).

## FAQs
[](id:que1)
### 1. How does live recording work?
![](https://main.qcloudimg.com/raw/334a262df93cd5eafcca740033894446.png)
After you enable recording for a live stream, each audio/video frame published from the host’s mobile phone will be relayed to the recording system and written into a recording file.

When a live stream is interrupted, the access layer will immediately ask the recording server to wrap up the writing process, save the file generated to the VOD system, and generate an index for the file. You can then find the recording file in the VOD system. If you have configured recording callback, the recording system will send the **index ID** and **playback URL** to the server you specified.

If a file is too large, errors may occur while the file is being transferred and processed in the cloud. As a result, to ensure the success of recording, we have capped the duration of a single recording file at 120 minutes. You can record shorter video segments by setting the `RecordInterval` parameter to a smaller value.

[](id:que2)
### 2. How many recording files does a live stream generate?
- **Recording in MP4, FLV, or AAC format**: the duration of a single file ranges from 1 to 120 minutes. You can specify a shorter segment using the `RecordInterval` parameter of the [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) API.
  - If a live stream is so short that it ends before the recording module is started, no recording files will be generated.
  - If a live stream lasts shorter than `RecordInterval` and is not interrupted, only one recording file will be generated.
  - If a live stream lasts longer than `RecordInterval`, the stream will be segmented based on the duration specified by `RecordInterval`. The purpose of this is to reduce the uncertainty of a file’s transfer time in a distributed system.
  - If a live stream is interrupted and resumed, a new video segment will be generated each time an interruption occurs.
- **Recording in HLS format:** There is no upper limit on the duration of recording files. If a live stream is interrupted and the timeout period for breakpoint resumption (which can be set to 0-1800s) elapses, a new recording file will be generated to continue recording.

[](id:que3)
### 3. How do I know which live stream a recording file belongs to?
Tencent Cloud as a PaaS provider does not really know how you define a live stream. Assume that a host streamed for 20 minutes, but the process was interrupted twice, once due to network change and once manually by the host. Is it one live stream or three?

In most mobile live streaming scenarios, we consider the period between the two time points below as a live stream.
![](https://main.qcloudimg.com/raw/e91b79fed8b397a4fc7e67bd9b302d1a.png)

If you use the above standard, the time information provided by your application is important. To determine which live stream a recording file belongs to, just search for the recording notification received by live stream code and time. Each recording notification carries information including stream ID, start time, and end time.

[](id:que4)
### 4. How to splice video segments?
You can splice video segments using a cloud API.
