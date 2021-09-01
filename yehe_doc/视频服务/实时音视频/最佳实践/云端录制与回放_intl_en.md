
## Use Cases
In application scenarios such as video interview, remote loss assessment, financial audiovisual recording, online education, live show streaming, and online healthcare, the entire video call or interactive live streaming process needs to be recorded and retained for future needs like evidence gathering, quality control, audit, storage, and playback.
Tencent Cloud TRTC provides a complete set of on-cloud recording features based on [LVB](https://intl.cloud.tencent.com/document/product/267) through relayed push during the entire live streaming process. Recording files can be stored on the [VOD](https://intl.cloud.tencent.com/document/product/266) platform for easy playback.



## How It Works
Tencent Cloud converts audio/video data in TRTC to the standard streaming media format by using the relayed push system and then transfers it to the on-cloud recording system which stores the audio/video streams in the specified format:

<span id="directRecord"></span>
- **Multi-channel audio/video streams recorded into multiple files**
In this scheme, each audio/video channel is recorded into an independent file. If you need to save the original files for further composing, you can select this scheme.

<span id="mixRecord"></span>
- **Multi-channel audio/video streams recorded into one file**
In this scheme, multiple audio/video channels are first mixed by [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) and then recorded in order to generate only one file for one call (or live stream).

## Directions
<span id="open"></span>
### Step 1. Activate the recording service
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc) and select **Application Management** on the left sidebar.
2. Click **Feature Configuration** in the row of the target application to enter the feature configuration page. If there are no applications, you can click **Create Application**, enter the application name, and click **OK** to create one.
3. Click <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png"  style="margin:0;"> on the right of **Enable Automatic Relayed Live Streaming** to enable relayed live streaming.
 > **Enabling relayed live streaming does not incur additional fees**: on-cloud recording in TRTC is implemented by reusing the recording system of LVB and can be enabled only after relayed live streaming is enabled. As LVB is billed based on the watch traffic, if you only activate the LVB service but do not configure a playback domain name, relayed live streaming cannot be watched, and no additional fees will be incurred.
 > 
4. Click <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png"  style="margin:0;"> on the right of **Enable Automatic On-Cloud Recording**.
<span id="Step5"></span>
5. On the pop-up recording configuration page, set the following parameters as needed:
 <table>
<tr>
<th>Parameter</th>
<th>Parameter Description</th>
<th>Recommended Value</th>
</tr>
<tr>
<td>File Type</td>
<td>The following file types are supported: <ul><li><b>HLS</b>: this file type is supported by most browsers for online playback and is suitable for video playback scenarios. If it is selected, resumable recording will be supported, and the maximum length of a single file will be unlimited.</li><li><b>FLV</b>: this file type is not supported by browsers for online playback but is simple and has a high fault tolerance. If you do not need to store recording files on the VOD platform, you can select this file type and download recording files immediately after recording is completed and delete the source files.</li><li><b>MP4</b>: this file type is supported by web browsers for online playback but has a low fault tolerance. Any packet loss during a video call will affect the playback quality of the recording file.</li><li><b>AAC</b>: you can select this file type if you only need to record audio.</li></td>
<td>HLS</td>
</tr>
<tr>
<td nowrap="nowrap">Maximum Length of Single File (in Minutes)</td>
<td>You can set the maximum length of a single file based on your actual business needs, and files exceeding this limit will be automatically split by the system. The value ranges from 5 to 120 minutes.<br>If **File Type** is set to **HLS**, the maximum length of a single file will be unlimited, i.e., this parameter will not take effect.</td>
<td>Custom</td>
</tr>
<tr>
<td>File Retention Duration (in Days)</td>
<td>You can set the number of days during which a video file will be stored on the VOD platform based on your actual business needs. The value ranges from 0 to 1,080 days, and 0 indicates permanent storage.</td>
<td>Custom</td>
</tr>
<tr>
<td>Recording Resumption Timeout Period (in Seconds)</td>
<td>Only when **File Type** is set to **HLS** can this parameter take effect.<br>By default, if a call (or live stream) is interrupted due to network jitter or other problems, the recording file will be split into multiple files. If you want to generate only one playback link for one call (or live stream), you can set this parameter as needed. If the interruption duration does not exceed the specified recording resumption timeout period, only one file will be generated for one call (or live stream). The value ranges from 1 to 300 seconds, and 0 indicates that recording resumption is disabled. </td>
<td>Custom</td>
</tr>
<tr>
<td>Recording Callback Address</td>
<td>Please enter the address for your server to receive recording file callback, which must be an HTTP or HTTPS address. When a new recording file is generated, Tencent Cloud will send a notification to your server at this address.</td>
<td>Custom</td>
</tr></table>

6. Click **Save** to save the settings.

> **Suggestions on file format**:
- Lecture or live stream playback: HLS is recommended.
HLS supports a maximum of 5-minute timeout period for recording resumption so as to generate only one playback link for one live stream (or lecture). In addition, it is supported by most browsers for online playback and is therefore ideal for video playback scenarios.
- Custom storage and archiving: FLV is recommended.
As an HLS file consists of a series of small .ts files, it is inconvenient to migrate it during service operation. Therefore, if you need to store recording files on your self-built servers, please choose the simple and highly tolerant FLV format.

<span id="start"></span>
### Step 2. Enable on-cloud recording

TRTC on-cloud recording is an automated process alongside audio/video data: when a user enters a room ([enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)), audio/video data can be upstreamed. At this time, the TRTC on-cloud system will relay the data to the LVB system where the recording module will write the data to a disk file.
Therefore, you only need to set the current `streamId` when a user enters the room (enterRoom) to enable the on-cloud recording feature, which will start writing the user's audio/video data to the disk file during data upstreaming. You can set the `streamId` in `TRTCParams` when invoking the `enterRoom` function in `TRTCCloud`.
This document uses `Objective-C` code for iOS as an example:

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // `SDKAppID` in TRTC, which can be obtained after an application is created
param.roomId   = 1001;           // Room ID
param.userId   = @"rexchang";    // Username
param.userSig  = @"xxxxxxxx";    // Login signature
param.role     = TRTCRoleAnchor; // Role: anchor
param.streamId = @"stream1001";  // Stream ID
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
```

The name of an on-cloud recording file is prefixed with `streamId` and contains the recording start time and end time, which is in the format of `streamId_recording start time (yyyy-MM-dd-HH24-mm-ss)_end time (yyyy-MM-dd-HH24-mm-ss)`.
For example, the `streamId` when a user enters a room is set to `stream1001`, and if the user upstreams audio/video data from 12:12:12 to 13:13:13 on February 16, the file generated in the cloud will be named `stream1001_2020-02-16-12-12-12_2020-02-16-13-13-13`.

> If `streamId` is not specified, Tencent Cloud will generate one by default according to the following calculation rules:
>- For applications created on or after January 9, 2020 and applications that were created before this data but have never been used, the rule `streamId = urlencode(SDKAppID_roomId_userId_stream type)` applies, i.e., the `streamId` is a URL-encoded value calculated based on `SDKAppID_roomId_userId_stream type`.
>- For applications that were created before January 9, 2020 and have been used, the rule `streamId = bizid_MD5(roomId_userId_stream type)` applies.
>
>Both `SDKAppID` and `bizid` can be found in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app). The stream type of camera image is `main`, while that of screen sharing is `aux`.

<span id="mix"></span>
### Step 3. Control the mix scheme for multi-channel video image
By default, an independent file will be generated for each anchor in a TRTC room. For example, if there are three users, "userA", "userB", and "userC" in a room, three independent files ("fileA", "fileB", and "fileC") will be recorded in the cloud by default.
In scenarios such as multi-person conferences and online education, you may want to record video images and audios of all users in only one file for one conference (or lecture). In this case, you can use [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) when enabling recording to mix video images and audios of "userA", "userB", and "userC" in the same room to one channel (A + B + C). For more information on the recording process, please see [How It Works](#mixRecord).

For example, there is only one anchor "userA" in the room "1001", and after a while, another user "userB" enters the same room and co-anchors with the anchor "userA". Then, the anchor "userA" will receive the `onUserVideoAvailable` and `onUserAudioAvailable` callbacks from "userB" through `TRTCCloudDelegate`. You can call the stream mixing command through [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) in these callbacks to mix the streams of "userA" and "userB" in the cloud.

This document uses the Objective-C code for iOS as an example to describe how to mix streams in order to display one big video image and two small ones at the same time with the small ones on top.

``` Objective-C
TRTCTranscodingConfig *config = [[TRTCTranscodingConfig alloc] init];
// Set the resolution to 720x1280, bitrate to 1,500 Kbps, and frame rate to 20 FPS
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
// Use the preset layout mode
config.mode = TRTCTranscodingConfigMode_Template_PresetLayout;
config.mixUsers = [NSMutableArray new];

// Camera image position of anchor
TRTCMixUser* local = [TRTCMixUser new];
local.userId = @"PLACE_HOLDER_LOCAL_MAIN"; 
local.zOrder = 0;   // `zOrder` value of 0 indicates that the anchor's video image is at the bottom
local.rect   = CGRectMake(0, 0, videoWidth, videoHeight);
local.roomID = nil; // `roomID` needs to be specified for a remote user but not the local user
[config.mixUsers addObject:local];
		
// Video image position of co-anchor
TRTCMixUser* remote1 = [TRTCMixUser new];
remote1.userId = @"PLACE_HOLDER_REMOTE"; 
remote1.zOrder = 1;
remote1.rect   = CGRectMake(400, 800, 180, 240); // For reference only
remote1.roomID = 97392; // `roomID` needs to be specified for a remote user but not the local user
[config.mixUsers addObject:remote1];

// Video image position of co-anchor
TRTCMixUser* remote2 = [TRTCMixUser new];
remote2.userId = @"PLACE_HOLDER_REMOTE"; 
remote2.zOrder = 1;
remote2.rect   = CGRectMake(400, 500, 180, 240); // For reference only
remote2.roomID = 97392; // `roomID` needs to be specified for a remote user but not the local user
[config.mixUsers addObject:remote2];
		
// Initiate the On-Cloud MixTranscoding service
[_trtc setMixTranscodingConfig:config];
```

<span id="search"></span>
### Step 4. Search for a recording file
After recording is enabled, files recorded in TRTC can be found in Tencent Cloud VOD. You can directly search for files in the VOD Console or use a RESTful API on your backend server for scheduled filtering:

**Method 1. Search for files in the VOD Console**
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/) and select **Media Assets** on the left sidebar.
2. Click **Prefix Search** above the list, select **Prefix Search**, enter a keyword such as `1400000123_1001_rexchang_main` in the search box, and click <img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;">. Video files whose names match the prefix will be displayed.
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
### Step 5. Receive a recording file
In addition to [searching for recording files](#search), you can make Tencent Cloud proactively push messages of new recording files to your server by configuring a callback address.
After the last channel of audio/video stream exits a room, Tencent Cloud will end recording and transfer the recording file to the VOD platform for storage, which will take about 30 seconds to 2 minutes by default (if you set the recording resumption timeout period to 300 seconds, then the actual waiting time will be 300 seconds plus the default waiting time). After the transfer and storage are completed, Tencent Cloud will send a notification to your server at the callback address configured in [Enabling On-Cloud Recording > Step 5](#Step5).

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
<td>You can set this field by specifying the `streamId` field in `TRTCParams` during room entry.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1cf7ec54371a5e95e2ea00bdda4d1a64.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userid</td>
<td>Base64-encoded username.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/66d50d985be81cae9698fae3ffa40f40.png" style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userdefinerecordid</td>
<td>Custom field. You can set this field by specifying the `userDefineRecordId` field in `TRTCParams`.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/d1cb894a93a1d69cd4215c54064eca5d.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>video_url</td>
<td>Playback address of the recording file, which can be used for <a href="#play">VOD playback</a>.</td>
</tr></table>

<span id="restapi"></span>
### Step 6. Delete a recording file
VOD provides a series of RESTful APIs for audio/video file management. You can use the [DeleteMedia](https://intl.cloud.tencent.com/document/product/266/31764) API to delete a specified file.
Sample RESTful request:
```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<Common request parameters>
```

<span id="play"></span>
### Step 7. Play back a recording file
In scenarios such as online education, recording files usually need to be played back for multiple times in order to make full use of the teaching resources.

**Select the file format (HLS)**
Select HLS as the file format in [Enabling On-Cloud Recording > Step 5](#Step5).
HLS supports a maximum of 5-minute timeout period for recording resumption so as to generate only one playback link for one live stream (or lecture). In addition, HLS is supported by most browsers for online playback and is therefore ideal for video playback scenarios.

**Get the VOD address (video_url)**
When [receiving a recording file](#callback), you can get the **video_url** field in the callback message, which is the VOD address of this file in Tencent Cloud.

**Integrate a VOD player**
Integrate a VOD player based on the used platform. For detailed directions, please see:
- [iOS](http://doc.qcloudtrtc.com/group__TXVodPlayer__ios.html)
- [Android](http://doc.qcloudtrtc.com/group__TXVodPlayer__android.html)
- [Web browser](https://intl.cloud.tencent.com/document/product/266/14424)

> You are recommended to use the [Pro Edition](https://intl.cloud.tencent.com/document/product/647/34615) of the TRTC SDK, which is integrated with various features such as superplayer (Player+) and MLVB. Thanks to the highly reusable underlying modules, integration with the Pro Edition has a smaller size than integration with two independent SDKs and can also avoid the problem of symbol duplicate.
