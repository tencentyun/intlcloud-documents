## Use Cases
In application scenarios such as remote education, show live streaming, video conferencing, remote loss assessment, financial audiovisual recording, and online healthcare, the entire video call or interactive live streaming process needs to be recorded and retained for future needs like evidence gathering, quality control, audit, storage, and playback.

The on-cloud recording feature of TRTC can record the audio and video streams of each user in the room into a separate file:
![](https://main.qcloudimg.com/raw/b96dd835182d3546f8d13abb290e619e.gif)

Multiple audio/video streams can also be first mixed by [On-cloud Stream Mix](https://intl.cloud.tencent.com/document/product/647/34618), and then the mixed audio/video streams can be recorded as a file:
![](https://main.qcloudimg.com/raw/be3fe2b57b07fb9cabe62e108f5cbe69.gif)

## Console Guide

<span id="open"></span>
### Activating recording service
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc) and select **Application Management** on the left sidebar.
2. Click **Feature Configuration** in the row of the target application to enter the feature configuration page. If there are no applications, you can click **Create Application**, enter the application name, and click **OK** to create one.
3. Click <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png"  style="margin:0;"> on the right of **Enable On-cloud Recording** and the on-cloud recording settings page will pop up:

<span id="recordType"></span>
### Selecting recording mode
The on-cloud recording service of TRTC supports two recording modes: "global auto-recording" and "recording by user":
![](https://main.qcloudimg.com/raw/cfa54cf045cd8d6ed266c5022ac4eb1e.png)

- **Global auto-recording**
The audio and video upstreams of each user in each TRTC room will be automatically recorded. The start and stop of the recording task are automatic, so you don't need to care about it. This option is relatively simple and easy to use. For specific usage, please see [Scheme 1. Global auto-recording](#autoRecord).

- **Recording by user**
You can specify to record certain users' audio and video streams, which requires you to control through the client SDK API or server RESTful API and requires additional development efforts. For specific usage, please see [Scheme 2. Recording by user (SDK API)](#recordSDKAPI) and [Scheme 3. Recording by user (RESTful API)](#recordRESTAPI).

<span id="fileFormat"></span>
### Selecting file format
On-cloud recording supports four different file formats: HLS, MP4, FLV, and AAC. The differences and applicable scenarios of the four formats are listed in the table below. You can choose an appropriate one according to your business needs:

<table>
<tr>
<th>Parameter</th>
<th>Parameter Description</th>
</tr>
<tr>
<td>File Type</td>
<td>The following file types are supported: <ul><li><b>HLS</b>: this file type is supported by most browsers for online playback and is suitable for video playback scenarios. If it is selected, resumable recording will be supported, and the maximum length of a single file will be unlimited.</li><li><b>FLV</b>: this file type is not supported by browsers for online playback but is simple and has a high fault tolerance. If you do not need to store recording files on the VOD platform, you can select this file type and download recording files immediately after recording is completed and delete the source files.</li><li><b>MP4</b>: this file type is supported by web browsers for online playback but has a low fault tolerance. Any packet loss during a video call will affect the playback quality of the recording file.</li><li><b>AAC</b>: you can select this file type if you only need to record audio.</li></td>
</tr>
<tr>
<td nowrap="nowrap">Maximum Length of Single File (in Minutes)</td>
<td>You can set the maximum length of a single video file based on your actual business needs, and files exceeding this limit will be automatically split by the system. The value ranges from 5 to 120 minutes.<br>If **File Type** is set to **HLS**, the maximum length of a single file will be unlimited, i.e., this parameter will not take effect.</td>
</tr>
<tr>
<td>File retention duration (in days)</td>
<td>You can set the number of days during which a video file will be stored on the VOD platform based on your actual business needs. The value ranges from 0 to 1,800 days, the file will be irreversibly deleted automatically by the VOD platform upon expiration, and 0 indicates permanent storage.</td>
</tr>
<tr>
<td>Recording Resumption Timeout Period (in Seconds)</td>
<td>Only when **File Type** is set to **HLS** can this parameter take effect.<br>By default, if a call (or live stream) is interrupted due to network jitter or other problems, the recording file will be split into multiple files. If you want to generate only one playback link for one call (or live stream), you can set this parameter as needed. If the interruption duration does not exceed the specified recording resumption timeout period, only one file will be generated for one call (or live stream). The value ranges from 1 to 300 seconds, and 0 indicates that recording resumption is disabled. </td>
</tr>
</table>

>? 
- The HLS format is recommended for online education businesses for easy course playback.
HLS supports a maximum of 5-minute timeout period for recording resumption so as to generate only one playback link for one lecture. In addition, it is supported by most browsers for online playback and is therefore ideal for video playback scenarios.
- If you need to store recording files on your own, the FLV format is recommended.
As an HLS file consists of a series of small .ts files, it is inconvenient to migrate it across servers. Therefore, if you need to store recording files on your self-built servers, please choose the simple and highly tolerant FLV format.

<span id="storageLocation"></span>
### Selecting storage location
An on-cloud recording file in TRTC will be stored in the Tencent Cloud VOD service by default. If multiple businesses in your project share the same Tencent Cloud VOD account, you may need recording file isolation. You can distinguish TRTC recording files from those in other businesses through the "subapplication" capability of VOD.

- **What are VOD primary application and subapplication?**
Primary application and subapplication are a way of resource division in VOD. A primary application is equivalent to a root account of VOD, and multiple subapplications can be created under the primary application, each of which is equivalent to a sub-account under the root account and has independent resource management features and storage space isolated from other subapplications.

- **How do I enable a VOD subapplication?**
You can add new subapplications in the [VOD Console](https://console.cloud.tencent.com/vod) as instructed in [How do I enable a VOD subapplication?](https://intl.cloud.tencent.com/document/product/266/33987).

<span id="recordCallback"></span>
### Setting recording callback
If you need to receive [storage notifications](#callback) for new files in real time, you can enter the address for your server to receive recording file callback, which must be an HTTP or HTTPS address. When a new recording file is generated, Tencent Cloud will send a notification to your server at this address.

![](https://main.qcloudimg.com/raw/34588c52d3a93690874fdb760c771a84.png)

For detailed recording callback receipt and interpretation, please see [Receiving recording file](#callback) below.

<span id="startAndStop"></span>
## Recording Control Schemes
TRTC provides three on-cloud recording control schemes, namely, "global auto-recording", "recording by user (controlled by SDK API)", and "recording by user (controlled by RESTful API)", each of which will be described in the following aspects:
- How do I select a scheme in the console?
- How do I start a recording task?
- How do I end a recording task?
- How do I mix multiple channels of video image in the room into one channel?
- How is a recording file named?
- What platforms are supported by the scheme?

<span id="autoRecord"></span>
### Scheme 1. Global auto-recording
- **Settings in the console**
To use this recording scheme, please select "Global Auto-Recording" when [selecting the recording mode](#recordType).

- **Start of recording task**
The audio and video streams of each user in the TRTC room will be automatically recorded into files with no additional operations required.

- **End of recording task**
The task will stop automatically. After an anchor stops upstreaming audio/video, on-cloud recording of the anchor will stop automatically. If you set the "recording timeout" when [selecting the file format](#fileFormat), you need to wait for the recording timeout period to elapse before you can receive the recording file.

- **Mix of multi-channel video image**
There are two schemes for on-cloud stream mix in the global auto-recording mode, namely, "server RESTful API scheme" and "client SDK API scheme". Do not mix the two schemes:
 + [Server RESTful API stream mix scheme](https://intl.cloud.tencent.com/document/product/647/34618#restapi): your server needs to initiate API calls, which are not subject to the client platform version.
 + [Client SDK API stream mix scheme](https://intl.cloud.tencent.com/document/product/647/34618#sdkapi): stream mix can be initiated directly on the client. Currently, it supports iOS, Android, Windows, macOS, and Electron but not WeChat Mini Program and Web Browser.


- **Naming of recording file**
 + If the anchor specifies the [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) parameter during room entry, the recording file will be named as `userDefineRecordId_start time_end time`;
 + If the anchor specifies the [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) parameter but not the [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) parameter during room entry, the recording file will be named as `streamId_start time_end time`;
 + If the anchor specifies neither the [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) parameter nor the [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) parameter during room entry, the recording file will be named as `sdkappid_roomid_userid_start time_end time`.
 
- **Supported platforms**
The operation is controlled by your server but not subject to the client platform.

<span id="recordSDKAPI"></span>
### Scheme 2. Recording by user (SDK API)

![](https://main.qcloudimg.com/raw/83b8e1790265a58bede293934802d000.gif)

- **Settings in the console**
To use this recording scheme, please select "Specified User Recording" when [selecting the recording mode](#recordType).

- **Start of recording task**
If the anchor specifies the [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) field in the room entry parameter [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams) during room entry, the upstreamed audio/video data of the anchor will be recorded in the cloud; otherwise, no recording tasks will be triggered.

```Objective-C
// Sample code: specifying to record the audio/video streams of user rexchang with the file ID as 1001_rexchang
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // `SDKAppID` in TRTC, which can be obtained after an application is created
param.roomId   = 1001;           // Room ID
param.userId   = @"rexchang";    // Username
param.userSig  = @"xxxxxxxx";    // Login signature
param.role     = TRTCRoleAnchor; // Role: anchor
param.userDefineRecordId = @"1001_rexchang";  // Recording ID, i.e., specifying to enable recording for this user
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // Please use the `LIVE` mode
```

- **End of recording task**
The task will stop automatically. After the anchor who specifies the [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) parameter during room entry stops upstreaming audio/video, on-cloud recording will stop automatically. If you set the "recording timeout" when [selecting the file format](#fileFormat), you need to wait for the recording timeout period to elapse before you can receive the recording file.

- **Mix of multi-channel video image**
You can call the SDK API [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) to mix the audio/video streams of other users in the room with the current user's audio/video streams. For more information, please see [On-cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88).

- **Naming of recording file**
The recording file will be named as `userDefineRecordId_start time_end time`.

- **Supported platforms**
Recording controls can be initiated on [iOS](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), [Android](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520), [Windows](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc), [macOS](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), and [Electron](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html) but not Web Browser and WeChat Mini Program.

<span id="recordRESTAPI"></span>
### Scheme 3. Recording by user (RESTful API)

![](https://main.qcloudimg.com/raw/f0d7c94b98e4e7839c2e360f1aeea718.gif)

>? TRTC's server provides a pair of RESTful APIs ([StartMCUMixTranscode](https://cloud.tencent.com/document/product/647/44270) and [StopMCUMixTranscode](https://cloud.tencent.com/document/product/647/44269)) to implement three features of on-cloud stream mix, on-cloud recording, and relayed live streaming:
>- On-cloud stream mix: the video image layout during stream mix can be controlled through the `LayoutParams` parameter.
>- On-cloud recording: on-cloud recording can be enabled/disabled through the `OutputParams.RecordId` parameter.
>- Relayed live streaming: CDN live watching can be enabled/disabled through the `OutputParams.StreamId` parameter.

- **Settings in the console**
To use this recording scheme, please select "Specified User Recording" when [selecting the recording mode](#recordType).

- **Start of recording task**
Call [StartMCUMixTranscode](https://cloud.tencent.com/document/product/647/44270) from your server and specify the `OutputParams.RecordId` parameter to start stream mix and recording.

```
// Sample code: starting on-cloud stream mix and on-cloud recording tasks through RESTful API
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

- **End of recording task**
The task will stop automatically. You can also call [StopMCUMixTranscode](https://cloud.tencent.com/document/product/647/44269) halfway to stop the stream mix or recording task.

- **Mix of multi-channel video image**
Call [StartMCUMixTranscode](https://cloud.tencent.com/document/product/647/44270) from your server and specify the `LayoutParams` parameter. For more information, please see [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88).

- **Naming of recording file**
A recording file will be named by the `OutputParams.RecordId` parameter specified when [StartMCUMixTranscode](https://cloud.tencent.com/document/product/647/44270) is called, and the naming format is `OutputParams.RecordId_start time_ end time`.

- **Supported platforms**
The operation is controlled by your server but not subject to the client platform.

<span id="search"></span>
## Finding Recording File
After recording is enabled, files recorded in TRTC can be found in Tencent Cloud VOD. You can directly search for files in the VOD Console or use a RESTful API on your backend server for scheduled filtering:

**Method 1. Search for files in the VOD Console**
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/) and select **Media Assets** on the left sidebar.
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
## Receive Recording File
In addition to [searching for recording files](#search), you can make Tencent Cloud proactively push messages of new recording files to your server by configuring a callback address.
After the last channel of audio/video stream exits a room, Tencent Cloud will end recording and transfer the recording file to the VOD platform for storage, which will take about 30 seconds to 2 minutes by default (if you set the recording resumption timeout period to 300 seconds, then the actual waiting time will be 300 seconds plus the default waiting time). After the transfer and storage are completed, Tencent Cloud will send a notification to your server at the callback address (HTTP/HTTPS) configured in [Setting recording callback](#recordCallback).

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
<td>Message type. If its value is 100, the callback message indicates generation of a recording file.</td>
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
## Deleting Recording File
VOD provides a series of RESTful APIs for audio/video file management. You can use the `DeleteMedia` API to delete a specified file.
Sample RESTful request:
```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<Common request parameters>
```

<span id="play"></span>
## Playing back Recording File
In scenarios such as online education, recording files usually need to be played back for multiple times in order to make full use of the teaching resources.

**Select the file format (HLS)**
Select HLS as the file format when [selecting the file format](#fileFormat).
HLS supports a maximum of 5-minute timeout period for recording resumption so as to generate only one playback link for one live stream (or lecture). In addition, HLS is supported by most browsers for online playback and is therefore ideal for video playback scenarios.

**Get the VOD address (video_url)**
When [receiving a recording file](#callback), you can get the **video_url** field in the callback message, which is the VOD address of this file in Tencent Cloud.

**Integrate a VOD player**
Integrate a VOD player based on the used platform. For detailed directions, please see:
- [iOS](http://doc.qcloudtrtc.com/group__TXVodPlayer__ios.html)
- [Android](http://doc.qcloudtrtc.com/group__TXVodPlayer__android.html)

>! We recommend you use the [Pro Edition](https://intl.cloud.tencent.com/document/product/647/34615) of the TRTC SDK, which is integrated with various features such as superplayer (Player+) and MLVB. Thanks to the highly reusable underlying modules, integration with the Pro Edition has a smaller size than integration with two independent SDKs and can also avoid the problem of symbol duplicate.
