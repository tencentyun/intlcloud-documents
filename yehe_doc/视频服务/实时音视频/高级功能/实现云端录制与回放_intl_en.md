## Use Cases
In application scenarios such as remote education, showroom streaming, video conferencing, remote loss assessment, financial transaction recording, and online healthcare, it is often necessary to record an entire video call or live streaming session and save the recording files for purposes such as evidence gathering, quality control, auditing, archiving, and playback.

With TRTC’s on-cloud recording feature, you can record the audio/video streams of each user in a room into separate files.
![](https://main.qcloudimg.com/raw/7820cdafe40fabc38653bc53795412d2.png)

You can also mix the audio/video streams in a room into one stream through [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) and then record the mixed stream into a single file.
![](https://main.qcloudimg.com/raw/2f92f978c2ca76d001891e645905e8f9.png)

## Directions
[ ](id:open)
### Enabling the recording feature
1. Log in to the TRTC console and click [Application Management](https://console.cloud.tencent.com/trtc/app) on the left sidebar.
2. Find your application and click **Function Configuration** on the right. If you haven’t created an application yet, click **Create Application**, enter an application name, and click **Confirm** to create one.
3. Click <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png"> next to **Enable On-Cloud Recording**. The configuration page for on-cloud recording appears.


[ ](id:recordType)

### Selecting a recording mode

TRTC supports recording in two modes: **Global Auto-Recording** and **Specified User Recording**.
![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

- **Global Auto-Recording**
  The upstream audio/video streams of all users in all TRTC rooms are automatically recorded. The recording starts and stops automatically. Because no human intervention is needed, this mode is simple and easy to use. For detailed instructions, see [Scheme 1: Global Auto-Recording](#autoRecord).

- **Specified User Recording**
  You can specify users whose streams you want to record. This is achieved using either the client-side SDK API or server-side RESTful API for on-cloud recording and requires additional development efforts. For detailed instructions, see [Scheme 2: specified user recording (SDK API)](#recordSDKAPI) and [Scheme 3: specified user recording (RESTful API)](#recordRESTAPI).


[ ](id:fileFormat)

### Selecting a file format

TRTC can record streams in four formats, namely HLS, MP4, FLV, and AAC. Their differences and application scenarios are listed in the table below.

<table>
<tr><th>Item</th><th>Description</th></tr>
<tr>
<td>File format</td>
<td>Four file formats are supported: <ul style="margin:0"><li><b>HLS</b>: Files in this format can be played back on most browsers and are ideal for scenarios in which videos need to be replayed multiple times. When this format is selected, recording can resume from breakpoints, and no upper limit is set on the recording length of a file.</li><li><b>FLV</b>: Files in this format cannot be played back on browsers, but the format is simple and fault tolerant. You can use this format if you do not need to save recording files in VOD. Just download the files immediately after recording and delete the original files.</li><li><b>MP4</b>: Files in this format can be played back on browsers, but the format is not fault tolerant. Any packet loss during a video call may affect the playback quality of the recording file.</li><li><b>AAC</b>: Select this format if you want to record audio only.</li></td>
</tr>
<tr>
<td nowrap="nowrap">Maximum file length (min)</td>
<td><ul style="margin:0"><li/>You can set a maximum length for recording files based on your needs. The system will automatically segment files that exceed the limit. The value range is 1-120 (minutes).<li/>When <b>HLS</b> is selected for <b>File Type</b>, no limit is set on the length of recording files, and this parameter will be ignored.</td>
</tr>
<tr>
<td>File retention duration (day)</td>
<td>You can set for how many days you want VOD to save your recording files. The value range is 0-1500 (days). Files that expire will be deleted and cannot be retrieved. `0` indicates to save files indefinitely.</td>
</tr>
<tr>
<td>Resumption timeout (second)</td>
<td><ul style="margin:0"><li/>By default, if a call/live streaming session is interrupted due to network jitter or other reasons, the call will be recorded into multiple files.<li/>You can set this parameter if you want to generate only one playback link for each call/live streaming session. If recording is cut off for a period not longer than the specified time, only one file will be generated, which you can get only after the timeout period elapses. <li/>Value range: 0-1800 (seconds). `0` indicates to disable the resumption feature.</ul></td>
</tr>
</table>


>? HLS allows a maximum resumption timeout period of 30 minutes, making it possible to generate only one playback link for each lecture. What’s more, files in HLS format can be played back on most browsers, making the format ideal for video playback in online education scenarios.

[ ](id:storageLocation)

### Selecting a storage location

In TRTC, recording files are stored in Tencent Cloud’s VOD platform by default. If more than one of your businesses share a Tencent Cloud VOD account, you may want to separate their recording files, which you can achieve through VOD’s subapplication feature.

- **What are VOD primary applications and subapplications?**
  Primary applications and subapplications offer a way to separate your resources in VOD. A primary application is essentially your VOD account. Multiple subapplications can be created under a primary application, each of which functions as a sub-account of the VOD account. The resources of subapplications are managed separately and assigned their own storage space.

- **How do I enable the subapplication feature in VOD?**
  You can create subapplications in the [VOD console](https://console.cloud.tencent.com/vod) as instructed in [Subapplication System](https://intl.cloud.tencent.com/document/product/266/33987).

[ ](id:recordCallback)

### Configuring the recording callback
- **Recording callback address:**
  To receive [notifications about the generation of new recording files](#callback) in real time, set the **Recording Callback Address** to an HTTP or HTTPS address on your server. When a new recording file is generated, Tencent Cloud will send a notification to your server via this address.
![](https://main.qcloudimg.com/raw/9b9beab813d929a7a364eb2d8ab045ba.png)
	
- **Recording callback key:**
The callback key is used to generate a signature for authentication, which is needed to receive recording callbacks. The key must consist of no more than 32 uppercase and lowercase letters and digits. For details, see [Common callback parameters](https://intl.cloud.tencent.com/document/product/267/38082).


>? For details about how to receive and interpret recording callbacks, please refer to the [Receiving recording files](https://intl.cloud.tencent.com/document/product/647/35426) section below.



[ ](id:startAndStop)

## Recording Schemes

TRTC offers three on-cloud recording schemes, namely [global auto-recording](#autoRecord), [specified user recording (SDK API)](#recordSDKAPI), and [specified user recording (RESTful API)](#recordRESTAPI). We will explain the following for each of the scheme.

- How do I select the scheme in the console?
- How do I start a recording task?
- How do I end a recording task?
- How do I mix multiple image streams in a room into one stream?
- How is a recording file named?
- What platforms support the scheme?


[](id:autoRecord)

### Scheme 1: Global auto-recording

- **Selecting the scheme in the console**
  To use this recording scheme, set **[On-Cloud Recording Mode](#recordType)** to **Global Auto-Recording** in the console.

- **Starting a recording task**
  The audio/video streams of each user in a TRTC room are recorded automatically, with no need for human intervention.

- **Ending a recording task**
  A task stops automatically when an anchor stops sending audio/video data. However, if you have set the **Resumption Timeout** parameter when [choosing the format for recording files](#fileFormat), you will not receive the recording file until the timeout period elapses.

- **Mixing streams**
  In the global auto-recording mode, you can mix streams by using either the server-side RESTful API or the client-side SDK API. These two methods for mixing streams should not be used at the same time.
  - [Stream mixing via the server-side RESTful API](#recordRESTAPI): The stream mixing API must be called on your server. This method works regardless of the platform the SDK runs on.
  - [Stream mixing via the client-side API](#recordSDKAPI): The stream mixing API can be called from the client. This method works on iOS, Android, Windows, macOS and Electron but does not work on WeChat Mini Program or browsers.

- **Naming of recording files**
  - If an anchor has set [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) during room entry, recording files will be named `userDefineRecordId_streamType__start time_end time` (`streamType` has two valid values: `main`, which indicates the primary stream, and `aux`, which indicates the substream.)
  - If an anchor has set [streamId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167), but not [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) during room entry, recording files will be named `streamId_start time_end time`.
  - If an anchor has set neither [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) nor [streamId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) during room entry, recording files will be named `sdkappid_roomid_userid_streamType_start time_end time` (`streamType` has two valid values: `main`, which indicates the primary stream, and `aux`, which indicates the substream.)

- **Supported platforms**
  Recording operations are initiated by your server and are not affected by the platform on which the SDK runs.

[](id:recordSDKAPI)

### Scheme 2: Specified user recording (SDK API)

You can call APIs of the TRTC SDK to enable On-Cloud MixTranscoding, on-cloud recording, and CDN live streaming.

| On-Cloud Capability | Enabling | Disabling |
| :------- | :------- | :------- |
| On-cloud recording | Specify the `userDefineRecordId` field in `TRTCParams` during room entry.    | The recording stops automatically when the anchor exits the room.                                           |
| On-Cloud MixTranscoding | Call the SDK API [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) to start On-Cloud MixTranscoding. | The mixing stops automatically when the anchor who starts it exits the room. The anchor can also stop it manually by calling [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93), with the parameter set to `null/nil`. |
| CDN live streaming | Specify the `streamId` field in `TRTCParams` during room entry.             | The relaying stops automatically when the anchor exits the room.                                           |

![](https://main.qcloudimg.com/raw/7daf8430ca74adeec019c10fc384a48e.gif)

- **Selecting the scheme in the console**
  To use this recording scheme, set [On-Cloud Recording Mode](#recordType) to **Specified User Recording** in the console.

- **Starting a recording task**
  If an anchor has set [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) in the room entry parameter [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCParams) during room entry, the audio/video data sent by the anchor will be recorded on the cloud. The streams of anchors who have not set the parameter are not recorded.
<dx-codeblock>
::: Objective-C Objective-C
// Sample code: Select the user rexchang for specified user recording, the ID of the recording file being `1001_rexchang`
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // SDKAppID in TRTC, which is generated after the creation of an application
param.roomId   = 1001;           // Room ID
param.userId   = @"rexchang";    // User ID
param.userSig  = @"xxxxxxxx";    // Login signature
params.role     = TRTCRoleAnchor; // Role: anchor
param.userDefineRecordId = @"1001_rexchang";  // Recording ID. Specify the user whose stream is to be recorded
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // Please use the `LIVE` mode
:::
</dx-codeblock>

- **Ending a recording task**
  The task stops automatically after the anchor who has set [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) during room entry stops sending audio/video. However, if you have set the **Resumption Timeout** parameter when [choosing the format for recording files](#fileFormat), you will not receive the recording file until the timeout period elapses.

- **Mixing streams**
  You can call the SDK API [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) to mix the audio/video streams of other users in a room into the current user's audio/video streams.
>! Make sure that the `setMixTranscodingConfig` API is called by just one anchor (preferably the anchor who created the room) in a TRTC room. Calling of the API by multiple anchors may cause errors.

- **Naming of recording files**
  Recording files are named `userDefineRecordId_start time_end time`.

- **Supported platforms**
  Recording tasks can be initiated on [iOS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), [Android](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520), [Windows](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc), [macOS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), and [Electron](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html), and [web](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createClient), but not on WeChat Mini Program currently.

[](id:recordRESTAPI)

### Scheme 3: Specified user recording (RESTful API)

TRTC's server provides a pair of RESTful APIs ([StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) and [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)) for the implementation of On-Cloud MixTranscoding, on-cloud recording, and CDN live streaming.

| On-Cloud Capability | Enabling  | Disabling |
| :------- | :------- | :------- |
| On-cloud recording | Specify `OutputParams.RecordId` when calling [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) to enable recording. | The recording stops automatically. It can also be manually stopped via the calling of [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760). |
| On-Cloud MixTranscoding | Specify `LayoutParams` when calling [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) to select a layout template and set other layout parameters. | Stream mixing stops automatically when the last user exits the room. It can also be manually stopped by calling [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760). |
| CDN live streaming | Specify `OutputParams.StreamId` when calling [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761). | The relaying stops automatically. It can also be manually stopped by calling [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760). |

>? The two RESTful APIs work via TRTC’s core stream mixing MCU and send mixed streams to the recording system and live streaming CDNs, hence the name `Start/StopMCUMixTranscode`. In addition to stream mixing, the APIs can also be used to enable on-cloud recording and CDN live streaming.

![](https://main.qcloudimg.com/raw/65ef546c0e424af77f7d20f23aa1d363.gif)

- **Selecting the scheme in the console**
  To use this recording scheme, set [On-Cloud Recording Mode](#recordType) to **Specified User Recording** in the console.

- **Starting a recording task**
  Call [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) from your server, with `OutputParams.RecordId` set to enable stream mixing and recording.
```
// Sample code: Start an On-Cloud MixTranscoding and on-cloud recording task through the RESTful API
https://trtc.tencentcloudapi.com/?Action=StartMCUMixTranscode
&SdkAppId=1400000123
&RoomId=1001
&OutputParams.RecordId=1400000123_room1001
&OutputParams.RecordAudioOnly=0
&EncodeParams.VideoWidth=1280
&EncodeParams.VideoHeight=720
&EncodeParams.VideoBitrate=1560
&EncodeParams.VideoFramerate=15
&EncodeParams.VideoGop=3
&EncodeParams.BackgroundColor=0
&EncodeParams.AudioSampleRate=48000
&EncodeParams.AudioBitrate=64
&EncodeParams.AudioChannels=2
&LayoutParams.Template=1
&<Common Request Parameters>
```

>! 
>- The RESTful API works only when at least one user has entered the room (`enterRoom`).
>- The RESTful API cannot be used to record single streams. If you want to record single streams, choose [Scheme 1](#autoRecord) or [Scheme 2](#recordSDKAPI).

- **Ending a recording task**
  Stream mixing and recording tasks stop automatically. You can also stop them manually by calling [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760).

- **Mixing streams**
  Set `LayoutParams` when calling [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) to enable On-Cloud MixTranscoding. The API can be called multiple times during live streaming, meaning that you can modify the `LayoutParams` parameter to change the layout of video images. Make sure you use the same `OutputParams.RecordId` and `OutputParams.StreamId` for each call; otherwise the recording will be interrupted and multiple recording files will be generated.



- **Naming of recording files**
  Recording files are named `OutputParams.RecordId_start time_ end time`, in which `OutputParams.RecordId` is set when [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) is called.

- **Supported platforms**
  Recording operations are initiated by your server and are not affected by the platform on which the SDK runs.

[](id:search)
## Searching for Recording Files

When recording is enabled, files recorded in TRTC are saved in Tencent Cloud’s VOD platform. You can search for files in the VOD console or use a RESTful API on your server for scheduled filtering.

#### Searching for files in the VOD console
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/) and click **Media Assets** on the left sidebar.
2. Click the search box above the list, select **Name Prefix**, enter a keyword (for example, `1400000123_1001_rexchang_main`), and click <img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;"> to show the files whose names match.
3. You can also filter files by creation time.

#### Searching for files via RESTful API
You can use the [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) API to query files in VOD. You can also use the request parameter `Text` for fuzzy searches or the `StreamId` parameter for exact searches.
RESTful request sample code:
```
https://vod.tencentcloudapi.com/?Action=SearchMedia
&StreamId=stream1001
&Sort.Field=CreateTime
&Sort.Order=Desc
&<Common Request Parameters>
```

[](id:callback)

## Receiving Recording Files

In addition to [searching for recording files](#search), you can configure a callback address to have Tencent Cloud push notifications to your server when new recording files are generated.
When the last user exits the room, Tencent Cloud will stop recording and save the recording file in VOD. This normally takes about 30-120 seconds. If you have set a resumption timeout period (for example, 300 seconds), then the process will take 300 seconds longer. After saving the file, Tencent Cloud will send a notification to your server via the [specified (HTTP/HTTPS) callback address](#recordCallback).

Tencent Cloud sends information about both the recording itself and recording-related events to your server via the specified callback address. Below is an example of a callback message:
![](https://main.qcloudimg.com/raw/483dba536acd022f93af3ca5ff6cd74a.png)
The fields in the table below can help you determine which call/live streaming session a callback is about.

<table>
<tr>
<th>No.</th><th>Field</th><th>Description</th>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/b75fdd3c8a2c0b1562ee4cb5a4ef65d1.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>event_type</td>
<td>Event type. `100` indicates that a recording file is generated.</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/2a495b157f03a8905e372a2516ea3a8f.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_id</td>
<td>Stream ID for CDN live streaming, which you can set by specifying the <a href="https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167">streamId</a> field in `TRTCParams` during room entry (recommended), or when calling the `startPublishing` API of `TRTCCloud`.</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1cf7ec54371a5e95e2ea00bdda4d1a64.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userid</td>
<td>Base64-encoded user ID</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/66d50d985be81cae9698fae3ffa40f40.png" style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userdefinerecordid</td>
<td>A custom field. You can set this field by specifying the <a href="https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce">userDefineRecordId</a> field in `TRTCParams`.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/d1cb894a93a1d69cd4215c54064eca5d.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>video_url</td>
<td>Playback address of the recording file, which can be used for <a href="#play">VOD playback</a>.</td>
</tr></table>

>? For information about other fields in the callback, see [Recording Event Notification](https://intl.cloud.tencent.com/document/product/267/38082).


[](id:delete)
## Deleting Recording Files

You can use the [DeleteMedia](https://intl.cloud.tencent.com/document/product/266/37571) to delete a file from VOD.
RESTful request sample code:
```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<Common Request Parameters>
```

[](id:play)
## Replaying Recording Files

In application scenarios such as online education, to make the best of teaching resources, it is often necessary to replay recording files multiple times.

#### Select the file format (HLS)
Select HLS as the [file format](#fileFormat).
HLS supports a maximum timeout period of 30 minutes for breakpoint resumption, making it possible to generate only one playback link for each live streaming session/lecture. What’s more, files in HLS format can be played back on most browsers, making it an ideal format for replay.

#### Get the playback address (video_url)
After [receiving a recording file callback](#callback), you can get the playback address of the file by looking for the **video_url** field in the callback message.

#### Integrate the VOD player
Integrate the VOD player. For detailed instructions, see the following documents.
- [iOS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html)
- [Android](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html)
- [Web](https://intl.cloud.tencent.com/document/product/266/33977)

>! We recommend you use [TRTC Professional](https://intl.cloud.tencent.com/document/product/647/34615), which integrates [Superplayer](https://intl.cloud.tencent.com/document/product/266/7836), MLVB features, and more. This integrated edition adds less to the size of your application package than two independent SDKs do because many underlying modules are shared among the services. It also allows you to avoid duplicate symbol issues.


## Billing
The on-cloud recording and playback feature is powered by cloud services including on-cloud recording and VOD’s storage, video processing, and playback services. It also relies on the player capabilities of the mobile SDKs.

### Cloud service fees
Cloud service fees include the fees incurred for recording videos on the cloud and playing back recording files.

>? The prices used in the examples of this document are for reference only. In case of any inconsistencies, the prices specified in [Billing of On-Cloud Recording](https://intl.cloud.tencent.com/document/product/647/38385), [Pricing - Cloud Streaming Services](https://buy.intl.cloud.tencent.com/pricing/css), and [Pricing - Video on Demand](https://buy.cloud.tencent.com/price/vod) shall apply.


- **Recording fee: The computing cost of transcoding or remuxing**
Because server computing resources are needed to transcode or remux audio/video streams during recording, a recording fee is charged based on the computing resources used for recording.
>!
>- For Tencent Cloud accounts that created their first TRTC applications on or after July 1, 2020, on-cloud recording fees are charged as described in [Billing of On-Cloud Recording](https://intl.cloud.tencent.com/document/product/647/45176).
>- Tencent Cloud accounts that created applications before July 1, 2020 will continue to be charged the **live recording** fee for the use of the recording service.
>
The **live recording** fee is calculated based on the peak number of concurrent recording channels. The higher the number, the higher the fee. For details, see [CSS > Live Recording](https://intl.cloud.tencent.com/document/product/267/39605).
> Assume that you have 1,000 anchors, and during peak times, it’s necessary to record the audio/video streams of 500 anchors at the same time. If the service is priced 5.2941 USD per channel per month, then you will be charged `500 channels x 5.2941 USD/channel/month = 2,647.05 USD/month`.
> If you select two [file formats](https://intl.cloud.tencent.com/document/product/647/35426), both the recording and storage fees will double. If you select three, they will triple. To reduce cost, you are advised to select only one file format.

- **Transcoding fee: Charged for using On-Cloud MixTranscoding**
Because stream mixing involves encoding and decoding, an additional transcoding fee will be charged if you enable On-Cloud MixTranscoding. The fee varies with the resolution used and the transcoding duration. The higher resolution used for anchors, and the longer co-anchoring (the most common application scenario for On-Cloud MixTranscoding) lasts, the higher the cost. For more information, see [Live Transcoding](https://intl.cloud.tencent.com/document/product/267/39604).
> Assume that you called [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) to set the bitrate (`videoBitrate`) for anchors to 1,500 Kbps and resolution to 720p, and the anchor co-anchored with a viewer for 1 hour, during which [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) was enabled. The transcoding fee incurred would be `0.0057 USD/min x 60 min = 0.342 USD`.

- **Storage fee: Charged for storing files with VOD**
Because storage requires disk resources, if you save recording files in VOD, a storage fee will be charged based on the disk resources used. The longer you save a file, the higher the cost. To reduce cost, you are advised to keep the storage duration as short as possible or store recording files on your own server. Storage fees are charged in the [daily pay-as-you-go mode](https://intl.cloud.tencent.com/document/product/266/14666).
> Assume that you called [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) to set the bitrate (`videoBitrate`) of an anchor to 1000 Kbps and recorded the anchor's stream (one file format) for an hour. The size of the recording file generated would be approximately `(1,000/8) KBps x 3,600s = 450,000 KB = 0.45 GB`. If you store the file with VOD, the storage fee per day would be `0.45 GB x 0.0009 USD/GB/day = 0.000405 USD`.

- **Playback fee**: Charged for playing back a file**
Playing back a recording file relies on VOD’s CDN playback feature and consumes CDN traffic. By default, a video acceleration fee is charged based on the traffic consumed by playback. The larger audience you serve, the higher the cost. Playback fees are charged in the [daily pay-as-you-go mode](https://intl.cloud.tencent.com/document/product/266/14666).
> Assume that you recorded a 1 GB file on the cloud and played it back to 1,000 users from beginning to end. The traffic consumed amounted to 1 TB, and according to VOD’s tiered pricing system, you would be charged `1,000 x 1 GB x 0.0794 USD/GB = 79.4 USD`.
> If you download files from Tencent Cloud to your server, a relatively small amount of traffic will also be consumed, which is billed on a monthly basis.

### Player license
TRTC Professional offers powerful player capabilities that allow you to play recording files and streams relayed to CDNs. If you use our mobile SDK and its version is 10.1 or later, please get a license to use the player capabilities.
>! You don’t need a license for playback within TRTC.


## FAQs
#### How do I record streams on the server side?
Server-side recording relies on the Linux SDK, which is not commercially available yet. If you have questions about the SDK or want to use it, please contact colleenyu@tencent.com.
