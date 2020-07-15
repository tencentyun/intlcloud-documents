## Application Scenarios
In application scenarios such as remote education, live show streaming, video conferencing, remote loss assessment, financial audiovisual recording, and online healthcare, the entire video call or interactive live streaming process needs to be recorded and retained for future needs like evidence gathering, quality control, audit, storage, and playback.

With TRTC on-cloud recording, an audio/video channel is recorded into an independent file for each user in a room:
![](https://main.qcloudimg.com/raw/7820cdafe40fabc38653bc53795412d2.png)

Or multiple audio/video channels are mixed by [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) and then recorded into one file:
![](https://main.qcloudimg.com/raw/2f92f978c2ca76d001891e645905e8f9.png)

## Console Guide

<span id="open"></span>
### Activating on-cloud recording service
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc) and select **Application Management** on the left sidebar.
2. Click **Feature Configuration** in the row of the target application to enter the feature configuration page. If there are no applications, you can click **Create Application**, enter the application name, and click **OK** to create one.
3. Click <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png"  style="margin:0;"> on the right of **Enable On-cloud Recording** to enter the on-cloud recording configuration page.

<span id="recordType"></span>
### Selecting an on-cloud recording mode
TRTC on-cloud recording has two modes: global auto-recording and specified user recording.
![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

- **Global auto-recording**
Upstream audio/video streams of every user in each TRTC room are automatically recorded. A recording task automatically starts and ends without manual intervention, making it easy to use. For more information, please see [Solution 1. Global auto-recording](#autoRecord).

- **Specified user recording**
You can record audio/video streams for specified users through SDK APIs on the client or RESTful APIs on the server, but this needs additional development. For more information, please see [Solution 2. Specified user recording (SDK APIs)](#recordSDKAPI) and [Solution 3. Specified user recording (RESTful APIs)](#recordRESTAPI).

<span id="fileFormat"></span>
### Selecting a file format
TRTC on-cloud recording supports HLS, MP4, FLV and AAC formats for you to choose as needed. Their differences and application scenarios are listed in the table below:

<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>File Type</td>
<td>The following file types are supported: <ul><li><b>HLS</b>: this file type is supported by most browsers for online playback and is suitable for video playback scenarios. If it is selected, resumable recording will be supported, and the maximum length of a single file will be unlimited.</li><li><b>FLV</b>: this file type is not supported by browsers for online playback but is simple and has a high fault tolerance. If you do not need to store recording files on the VOD platform, you can select this file type and download recording files immediately after recording is completed and delete the source files.</li><li><b>MP4</b>: this file type is supported by web browsers for online playback but has a low fault tolerance. Any packet loss during a video call will affect the playback quality of the recording file.</li><li><b>AAC</b>: you can select this file type if you only need to record audio.</li></td>
</tr>
<tr>
<td nowrap="nowrap">Maximum Length of Single File (in Minutes)</td>
<td>You can set the maximum length of a single file based on your actual business needs, and files exceeding this limit will be automatically split by the system. The value ranges from 5 to 120 minutes.<br>If **File Type** is set to **HLS**, the maximum length of a single file will be unlimited, i.e., this parameter will not take effect.</td>
</tr>
<tr>
<td>File Retention Duration (in Days)</td>
<td>You can set the number of days during which a video file will be stored on the VOD platform based on your actual business needs. The value ranges from 0 to 1,800 days, and 0 indicates permanent storage.</td>
</tr>
<tr>
<td>Recording Resumption Timeout Period (in Seconds)</td>
<td>Only when **File Type** is set to **HLS** can this parameter take effect.<br>By default, if a call (or live stream) is interrupted due to network jitter or other problems, the recording file will be split into multiple files. If you want to generate only one playback link for one call (or live stream), you can set this parameter as needed. If the interruption duration does not exceed the specified recording resumption timeout period, only one file will be generated for one call (or live stream). The value ranges from 1 to 300 seconds, and 0 indicates that recording resumption is disabled.</td>
</tr>
</table>

> 
- We recommend HLS for lecture playback in online education scenarios.
HLS supports a maximum of 5-minute timeout period for recording resumption so as to generate only one playback link for one lecture. In addition, it is supported by most browsers for online playback and is therefore ideal for video playback scenarios.
- We recommend FLV when you need to store recording files on self-built servers.
As an HLS file consists of a series of small .ts files, it is inconvenient to migrate it during service operation. Therefore, if you need to store recording files on your self-built servers, please choose the simple and highly tolerant FLV format.

<span id="storageLocation"></span>
### Selecting a storage location
Files recorded by TRTC on-cloud recording are stored on VOD by default. If multiple businesses in your project share the same VOD account, you may need to isolate recording files from each other. You can isolate TRTC recording files from those of other businesses through VOD "subapplications".

- **What are primary applications and subapplications in VOD?**
Primary applications and subapplications can divide VOD resources. A primary application is equivalent to a root account, and a subapplication to a sub-account under the root account. You can create multiple subapplications for one primary application, but each of them manages resources independently and has a storage space isolated from that of other subapplications.

- **How to enable VOD subapplications?**
Log in to the [VOD Console](https://console.cloud.tencent.com/vod), enable the subapplication feature, and create a subapplication as instructed in [Subapplication System](https://intl.cloud.tencent.com/document/product/266/33987).

<span id="recordCallback"></span>
### Configuring recording callback
If you want to receive a real-time [notification](#callback) whenever a recording file is generated, enter an address in the input box shown below for your server to receive the recoding file callback. The address should comply with the HTTP (or HTTPS) protocol. When a recording file is generated, Tencent Cloud will send a notification to your server via this address.



For details on how to receive a callback and understand its fields, please see [Receiving a Recoding File](#callback).

<span id="startAndStop"></span>
## On-cloud Recording Solutions
TRTC supports three on-cloud recording solutions: global auto-recording, specified user recording (SDK APIs), and specified user recording (RESTful APIs). They will be detailed from the following perspectives:
- How to configure and use a solution in the console?
- How to start a recording task?
- How to end a recording task?
- How to mix multiple image channels in a room into one?
- In which format will a recording file be named?
- Which platforms will support these solutions?

<span id="autoRecord"></span>
### Solution 1. Global auto-recording
- **Configure in the console**
Select **Global Auto-Recording** as the [on-cloud recording mode](#recordType) in the console.

- **Start a recording task**
Audio/video streams of every user in each TRTC room are automatically recorded without manual intervention.

- **End a recording task**
A recording task ends automatically. Once an anchor stops upstreaming audio/video streams, the on-cloud recording automatically stops. If you set the recording resumption timeout period when [selecting a file format](#fileFormat), you will not receive the recording file until the timeout period has elapsed.

- **Mix multiple image channels**
Global auto-recording supports two methods of On-Cloud MixTranscoding: mixing through RESTful APIs on the server or SDK APIs on the client. Do not use both methods at the same time:
 + [Mixing through RESTful APIs on the server](https://intl.cloud.tencent.com/document/product/647/34618#restapi): call APIs on your server, which is not subject to the client platform version.
 + [Mixing through SDK APIs on the client](https://intl.cloud.tencent.com/document/product/647/34618#sdkapi): the client starts a mixing. Currently, clients for iOS, Android, Windows, macOS, and Electron, etc. are supported, while WeChat Mini Programs and web browsers are not.


- **Name a recording file**
 + If the [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) parameter is specified when an anchor enters a room, the recording file is named `userDefineRecordId_start time_end time`.
 + If the [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) parameter (instead of [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)) is specified when an anchor enters a room, the recording file is named `streamId_start time_end time`.
 + If neither [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) nor [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) is specified when an anchor enters a room, the recording file is named `sdkappid_roomid_userid_start time_end time`.
 
- **Supported platforms**
They depend on your server rather than the client.

<span id="recordSDKAPI"></span>
### Solution 2. Specified user recording (SDK APIs)

![](https://main.qcloudimg.com/raw/e3d81ef76c64d2fb6631d98d22bfb0dc.png)

- **Configure in the console**
Select **Specified User Recording** as the [on-cloud recording mode](#recordType) in the console.

- **Start a recording task**
If the [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) field of the [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams) parameter is specified when an anchor enters a room, upstream audio/video data of the anchor can be recorded on cloud; otherwise, no recording task will be triggered by the anchor.

```Objective-C
// Sample code: record the audio/video streams of the specified "rexchang" user, and the file ID is "1001_rexchang"
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // `SDKAppID` in TRTC, which can be obtained after an application is created
param.roomId   = 1001;           // Room ID
param.userId   = @"rexchang";    // Username
param.userSig  = @"xxxxxxxx";    // Login signature
params.role     = TRTCRoleAnchor; // Role: anchor
param.userDefineRecordId = @"1001_rexchang";  // Recording ID, used to record only for this user
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // Please enable LIVE mode
```

- **End a recording task**
A recording task ends automatically. If the [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) parameter is specified when an anchor enters a room, once an anchor stops upstreaming audio/video streams, the on-cloud recording automatically stops. If you set the recording resumption timeout period when [selecting a file format](#fileFormat), you will not receive the recording file until the timeout period has elapsed.

- **Mix multiple image channels**
You can call the [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) SDK API to mix other users' images and audios in the same room into the current user's channel. For more information, please see [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88).

- **Name a recording file**
A recording file is named in the format of `userDefineRecordId_start time_end time`.

- **Supported platforms**
Currently, terminals for [iOS](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), [Android](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520), [Windows](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc), [macOS](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), and [Electron](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html), etc., are supported, while WeChat Mini Programs and web browsers are not.

<span id="recordRESTAPI"></span>
### Solution 3. Specified user recording (RESTful APIs)

![](https://main.qcloudimg.com/raw/71b4b6705cee61000660c13c2a0fe595.png)

> TRTC provides the `StartMCUMixTranscode` and `StopMCUMixTranscode` RESTful APIs for the server to implement on-cloud mixing and transcoding, on-cloud recording and relayed live streaming:
>- On-cloud mixing and transcoding: the `LayoutParams` parameter controls the image layout in mixing.
>- On-cloud recording: the `OutputParams.RecordId` parameter enables/disables on-cloud recording.
>- Relayed live streaming: the `OutputParams.StreamId` parameter enables/disables CDN relayed live streaming.

- **Configure in the console**
Select **Specified User Recording** as the [on-cloud recording mode](#recordType) in the console.

- **Start a recording task**
Call the `StartMCUMixTranscode` API and specify the `OutputParams.RecordId` parameter on your server to start mixing and recording.

```
// Sample code: start on-cloud mixing and transcoding and on-cloud recording tasks through the RESTful APIs
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
&<Common request parameters>
```

- **End a recording task**
A recording task ends automatically. You can call the `StopMCUMixTranscode` API to manually end a mixing or recording task in progress.

- **Mix multiple image channels**
Call the `StartMCUMixTranscode` API and specify the `LayoutParams` parameter on your server to mix. For more information, please see [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88).

- **Name a recording file**
A recording file is named with the `OutputParams.RecordId` parameter specified when `StartMCUMixTranscode` is called. The name is in the format of `OutputParams.RecordId_start time_end time`.

- **Supported platforms**
They depend on your server rather than the client.

<span id="search"></span>
## Searching for a Recording File
After recording is enabled, files recorded in TRTC can be found in Tencent Cloud VOD. You can directly search for files in the VOD Console or use a RESTful API on your backend server for scheduled filtering:

**Method 1. Search for files in the VOD Console**
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/) and click **Media Assets** on the left sidebar.
2. Click **Search by prefix** above the list, select **Search by prefix**, enter a keyword such as `1400000123_1001_rexchang_main` in the search box, and click <img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;">. Video files whose names match the prefix will be displayed.
3. You can filter out target files by creation time.

**Method 2. Search for files through a VOD RESTful API**
VOD provides a series of RESTful APIs for audio/video file management. You can use the [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179) RESTful API to query files in VOD. You can perform fuzzy match by using the parameter `Text` in the request parameter or perform exact search by specifying the `StreamId` parameter.
Sample RESTful request:
```
https://vod.tencentcloudapi.com/?Action=SearchMedia
&StreamId=stream1001
&Sort.Field=CreateTime
&Sort.Order=Desc
&<Common request parameters>
```

<span id="callback"></span>
## Receiving a Recording File
In addition to [searching for recording files](#search), you can make Tencent Cloud proactively push messages of new recording files to your server by configuring a callback address.
After the last channel of audio/video stream exits a room, Tencent Cloud will end recording and transfer the recording file to the VOD platform for storage, which will take about 30 seconds to 2 minutes by default (if you set the recording resumption timeout period to 300 seconds, then the actual waiting time will be 300 seconds plus the default waiting time). After the transfer and storage are completed, Tencent Cloud will send a notification to your server at the callback (HTTP/HTTPS) address configured in [Configuring recording callback](#recordCallback).

Tencent Cloud will push the recording and recording-related events to your server at the specified callback address. Below is a sample callback message:
![](https://main.qcloudimg.com/raw/1a89e7058f7c806f6f867217821d1a9c.png)
You can determine which call (or live stream) corresponds to the current callback based on the fields in the following table:

<table>
<tr>
<th>No.</th>
<th>Field Name</th>
<th>Description</th>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/b75fdd3c8a2c0b1562ee4cb5a4ef65d1.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>event_type</td>
<td>Message type. If its value is 100, the callback message indicates the generation of a recording file.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/2a495b157f03a8905e372a2516ea3a8f.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_id</td>
<td>You can set this field by specifying the <a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167">streamId</a> field in `TRTCParams` during room entry.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1cf7ec54371a5e95e2ea00bdda4d1a64.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userid</td>
<td>Base64-encoded username.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/66d50d985be81cae9698fae3ffa40f40.png" style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userdefinerecordid</td>
<td>Custom field. You can set this field by specifying the <a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce">userDefineRecordId</a> field in `TRTCParams`.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/d1cb894a93a1d69cd4215c54064eca5d.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>video_url</td>
<td>Playback address of the recording file, which can be used for <a href="#play">VOD playback</a>.</td>
</tr></table>

<span id="delete"></span>
## Deleting a Recording File
VOD provides a series of RESTful APIs for audio/video file management. You can use the `DeleteMedia` API to delete a specified file.
Sample RESTful request:
```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<Common request parameters>
```

<span id="play"></span>
## Playing Back a Recording File
In scenarios such as online education, recording files usually need to be played back for multiple times in order to make full use of the teaching resources.

**Select the file format (HLS)**
Select HLS as the [file format](#fileFormat).
HLS supports a maximum of 5-minute timeout period for recording resumption so as to generate only one playback link for one live stream (or lecture). In addition, HLS is supported by most browsers for online playback and is therefore ideal for video playback scenarios.

**Get the VOD address (video_url)**
When [receiving a recording file](#callback), you can get the **video_url** field in the callback message, which is the VOD address of this file in Tencent Cloud.

**Integrate a VOD player**
Integrate a VOD player based on the used platform. For detailed directions, please see:
- [iOS](http://doc.qcloudtrtc.com/group__TXVodPlayer__ios.html)
- [Android](http://doc.qcloudtrtc.com/group__TXVodPlayer__android.html)

> We recommend that you use the [professional edition](https://intl.cloud.tencent.com/document/product/647/34615) of the TRTC SDK, which is integrated with various features such as superplayer (Player+) and MLVB. Thanks to the highly reusable underlying modules, integration with the professional edition has a smaller size than integration with two independent SDKs and can also avoid the problem of symbol duplicate.
