# Relay to CDN

This document describes how to publish (relay) audio/video streams in TRTC to CDNs so that viewers can watch the streams using standard live streaming players.

## Publishing the Local User’s Stream to CDNs

![](https://qcloudimg.tencent-cloud.cn/raw/f1df9ddcf6fbf206cb6e6b29af88ff31.png)
### Description

You can use the **startPublishMediaStream** API of `TRTCCloud` to publish the audio/video streams of local users to live streaming CDNs (known in TRTC as "relay to CDN").
The TRTC server will send the audio/video data directly to the CDN server. Because the data is not transcoded, the cost is relatively low.
However, if there are multiple users publishing audio/video streams in a room, there will be a CDN stream for each user. Multiple players are needed to play the streams, and they may not play in sync.

### Directions
Follow the steps below to publish the local user’s stream to CDNs.
1. Create a `TRTCPublishTarget` object and set `mode` in the object to `TRTCPublishBigStreamToCdn` or `TRTCPublishSubStreamToCdn`. The former is used to publish the user’s primary stream (usually the camera), and the latter is used to publish the user’s substream (usually the screen).
2. Set `cdnUrlList` in the `TRTCPublishTarget` object to one or multiple CDN addresses (which usually start with `rtmp://`). If you publish to the Tencent Cloud CDN, set `isInternalLine` to `true`; otherwise, set it to `false`.
3. Because the data is not transcoded, leave `TRTCStreamEncoderParam` and `TRTCStreamMixingConfig` empty.
4. Call `startPublishMediaStream`. If the `taskId` parameter returned by the `onStartPublishMediaStream` callback is not empty, the local API call is successful.
5. To stop publishing, call `stopPublishMediaStream`, passing in the `taskId` returned by `onStartPublishMediaStream`.

### Sample code

The code below publishes the local user’s stream to a live streaming CDN.

<dx-codeblock>
::: Java Java
```
TRTCCloudDef.TRTCPublishTarget target = new TRTCCloudDef.TRTCPublishTarget();
target.mode = TRTC_PublishBigStream_ToCdn;

TRTCCloudDef.TRTCPublishCdnUrl cdnUrl= new TRTCCloudDef.TRTCPublishCdnUrl();
cdnUrl.rtmpUrl = "rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = true;
target.cdnUrlList.add(cdnUrl);

mTRTCCloud.startPublishMediaStream(target, null, null);
```
:::
::: ObjC ObjC
```
TRTCPublishTarget* target = [[TRTCPublishTarget alloc] init];
target.mode = TRTCPublishBigStreamToCdn;

TRTCPublishCdnUrl* cdnUrl = [[TRTCPublishCdnUrl alloc] init];
cdnUrl.rtmpUrl = @"rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = YES;

NSMutableArray* cdnUrlList = [NSMutableArray new];
[cdnUrlList addObject:cdnUrl];
target.cdnUrlList = cdnUrlList;

[_trtcCloud startPublishMediaStream:target encoderParam:nil mixingConfig:nil];
```
:::
::: C++ C++
```
TRTCPublishTarget target;
target.mode = TRTCPublishMode::TRTCPublishBigStreamToCdn;

TRTCPublishCdnUrl* cdn_url_list = new TRTCPublishCdnUrl[1];
cdn_url_list[0].rtmpUrl = "rtmp://tencent/live/bestnews";
cdn_url_list[0].isInternalLine = true;

target.cdnUrlList = cdn_url_list;
target.cdnUrlListSize = 1;

trtc->startPublishMediaStream(&target, nullptr, nullptr);
delete[] cdn_url_list;
```
:::
</dx-codeblock>


## Publishing Mixed Streams to CDNs

![](https://qcloudimg.tencent-cloud.cn/raw/fa00298505bb8284bb5224b65cff4c6a.png)

### Description
You can call **startPublishMediaStream** to mix the streams of multiple users in a TRTC room into one stream and publish the stream to a CDN. The `TRTCStreamEncoderParam` and `TRTCStreamMixingConfig` parameters of the API allow you to determine the details of stream mixing and transcoding.

The streams will be decoded on the cloud first, mixed, and then re-encoded according to the stream mixing parameters (`TRTCStreamMixingConfig`) and transcoding parameters (`TRTCStreamEncoderParam`) you specify. Afterward, they will be published to CDNs. In this mode, additional [transcoding fees](https://intl.cloud.tencent.com/document/product/647/38929) are charged.

### Directions
Follow the steps below to mix the streams of multiple users in a room and publish the mixed stream to CDNs.
1 Create a `TRTCPublishTarget` object and set `mode` in the object to `TRTCPublishMixStreamToCdn`.
2. Set `cdnUrlList` in the `TRTCPublishTarget` object to one or multiple CDN addresses (which usually start with `rtmp://`). If you publish to the Tencent Cloud CDN, set `isInternalLine` to `true`; otherwise, set it to `false`.
3. Set the encoding parameters (`TRTCStreamEncoderParam`):
**Video encoding parameters:** Specify the resolution, frame rate (15 fps is recommended), bitrate, and GOP (3 seconds is recommended). Bitrate and resolution work in correlation with each other. The table below lists some recommended resolution and bitrate settings.
**Audio encoding parameters:** Specify the codec, bitrate, sample rate, and sound channels according to the `AudioQuality` value you pass in when calling `startLocalAudio`.

|videoEncodedWidth | videoEncodedHeight | videoEncodedFPS |  videoEncodedGOP |  videoEncodedKbps |
|:-------:|:-----:|:-------:|:------:|:------:|
| 640   | 360    | 15 | 3 |  800 Kbps |
| 960   | 540    | 15 | 3 | 1200 Kbps |
| 1280 | 720   | 15 | 3 | 1500 Kbps |
| 1920 | 1080   | 15 | 3 | 2500 Kbps |

| TRTCAudioQuality | audioEncodedSampleRate | audioEncodedChannelNum | audioEncodedKbps | audioEncodedCodecType |
|---------|---------|---------|---------|---------|
| TRTCAudioQualitySpeech | 48000 | 1 | 50 | 0 |  
| TRTCAudioQualityDefault | 48000 | 1 | 50 | 0 |  
| TRTCAudioQualityMusic | 48000 | 2 | 60 | 2 |  

4. Set the parameters for audio mixing and video layout (`TRTCStreamMixingConfig`):
**Audio mixing parameters (`audioMixUserList`)**: You can leave this parameter empty to mix all audios in a room, or you can set it to the IDs of users whose audios you want to mix.
**Video layout parameters (`videoLayoutList`)**: Video layout is determined by an array. Each `TRTCVideoLayout` element in the array determines the position, dimensions, and background color of a video window. If you specify **fixedVideoUser**, the window defined by the `TRTCVideoLayout` element will display the video of a specific user. If you set `fixedVideoUser` to null, the TRTC server will determine whose video to display in the window.

> **Example 1: Mix four users’ streams and use an image as the background.**
>- `layout1` specifies the position (upper half of the canvas) and dimensions (640 x 480) of the camera video of user `jerry`.
>- Because no user IDs are specified for `layout2`, `layout3`, and `layout4`, TRTC will display the videos of the other three users in the windows based on its own rule.
![](https://qcloudimg.tencent-cloud.cn/raw/6530f7a07ef88f22ec9798d41f646b63.png) <br>

> **Example 2: Mix the camera video and screen of one user plus the camera videos of three other users.**
>- `layout1` specifies the position (left) and dimensions (1280 x 720) of user `jerry`’s screen. The rendering mode used is aspect fit (`Fit`), and the background color is black.
>- `layout2` specifies the position (top right) and dimensions (300 x 200) of user `jerry`’s camera video. The rendering mode used is aspect fill (`Fill`).
>- Because no user IDs are specified for `layout3`, `layout4`, and `layout5`, TRTC will display the videos of the other three users in the windows based on its own rule.
![](https://qcloudimg.tencent-cloud.cn/raw/0cd5b07fb3e03e6a742f9c396c6ea241.png)

5. Call `startPublishMediaStream`. If the `taskId` parameter returned by the `onStartPublishMediaStream` callback is not empty, the local API call is successful.
6. To change the stream mixing parameters (for example, the video layout), call `updatePublishMediaStream`, passing in the `taskId` returned in step 6 as well as the new `TRTCStreamMixingConfig` parameters. We recommend you do not change `TRTCStreamEncoderParam` during relay because doing so will affect the stability of CDN playback.
7. To stop publishing, call `stopPublishMediaStream`, passing in the `taskId` returned by `onStartPublishMediaStream`.

### Sample code
The code below mixes the streams of multiple users in a room and publishes the result to a CDN.

<dx-codeblock>
::: Java Java
```
TRTCCloudDef.TRTCPublishTarget target = new TRTCCloudDef.TRTCPublishTarget();
target.mode = TRTC_PublishMixedStream_ToCdn;

TRTCCloudDef.TRTCPublishCdnUrl cdnUrl= new TRTCCloudDef.TRTCPublishCdnUrl();
cdnUrl.rtmpUrl = "rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = true;
target.cdnUrlList.add(cdnUrl);


TRTCCloudDef.TRTCStreamEncoderParam encoderParam 
    = new TRTCCloudDef.TRTCStreamEncoderParam();
encoderParam.videoEncodedWidth = 1280;
encoderParam.videoEncodedHeight = 720;
encoderParam.videoEncodedFPS = 15;
encoderParam.videoEncodedGOP = 3;
encoderParam.videoEncodedKbps = 1000;
encoderParam.audioEncodedSampleRate = 48000;
encoderParam.audioEncodedChannelNum = 1;
encoderParam.audioEncodedKbps = 50;
encoderParam.audioEncodedCodecType = 0;

TRTCCloudDef.TRTCStreamMixingConfig mixingConfig =
      new TRTCCloudDef.TRTCStreamMixingConfig();
TRTCCloudDef.TRTCVideoLayout layout1 = new TRTCCloudDef.TRTCVideoLayout();
layout1.zOrder = 0;
layout1.x = 0;
layout1.y = 0;
layout1.width = 720;
layout1.height = 1280;
layout1.fixedVideoStreamType = TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SUB;
layout1.fixedVideoUser.intRoomId = 1234;    
layout1.fixedVideoUser.userId = "mike"; 

TRTCCloudDef.TRTCVideoLayout layout2 = new TRTCCloudDef.TRTCVideoLayout();
layout2.zOrder = 0;
layout2.x = 1300;
layout2.y = 0;
layout2.width = 300;
layout2.height = 200;
layout2.fixedVideoStreamType = TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG;
layout2.fixedVideoUser.intRoomId = 1234;    
layout2.fixedVideoUser.userId = "mike"; 

TRTCCloudDef.TRTCVideoLayout layout3 = new TRTCCloudDef.TRTCVideoLayout();
layout3.zOrder = 0;
layout3.x = 1300;
layout3.y = 220;
layout3.width = 300;
layout3.height = 200;
layout3.fixedVideoStreamType = TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SUB;
layout3.fixedVideoUser = null;

mixingConfig.videoLayoutList.add(layout1);
mixingConfig.videoLayoutList.add(layout2);
mixingConfig.videoLayoutList.add(layout3);
mixingConfig.audioMixUserList = null;

mTRTCCloud.startPublishMediaStream(target, encoderParam, mixingConfig);
```
:::
::: ObjC ObjC
```
TRTCPublishTarget* target = [[TRTCPublishTarget alloc] init];
target.mode = TRTCPublishMixStreamToCdn;

TRTCPublishCdnUrl* cdnUrl = [[TRTCPublishCdnUrl alloc] init];
cdnUrl.rtmpUrl = @"rtmp://tencent/live/bestnews";
cdnUrl.isInternalLine = YES;

NSMutableArray* cdnUrlList = [NSMutableArray new];
[cdnUrlList addObject:cdnUrl];
target.cdnUrlList = cdnUrlList;

TRTCStreamEncoderParam* encoderParam = [[TRTCStreamEncoderParam alloc] init];
encoderParam.videoEncodedWidth = 1280;
encoderParam.videoEncodedHeight = 720;
encoderParam.videoEncodedFPS = 15;
encoderParam.videoEncodedGOP = 3;
encoderParam.videoEncodedKbps = 1000;
encoderParam.audioEncodedSampleRate = 48000;
encoderParam.audioEncodedChannelNum = 1;
encoderParam.audioEncodedKbps = 50;
encoderParam.audioEncodedCodecType = 0;

TRTCStreamMixingConfig* config = [[TRTCStreamMixingConfig alloc] init];
NSMutableArray* videoLayoutList = [NSMutableArray new];
TRTCVideoLayout* layout1 = [[TRTCVideoLayout alloc] init];
layout1.zOrder = 0;
layout1.rect = CGRectMake(0, 0, 720, 1280);
layout1.fixedVideoStreamType = TRTCVideoStreamTypeSub;
layout1.fixedVideoUser.intRoomId = 1234;
layout1.fixedVideoUser.userId = @"mike";  

TRTCVideoLayout* layout2 = [[TRTCVideoLayout alloc] init];
layout2.zOrder = 0;
layout2.rect = CGRectMake(1300, 0, 300, 200);
layout2.fixedVideoStreamType = TRTCVideoStreamTypeBig;
layout2.fixedVideoUser.intRoomId = 1234;
layout2.fixedVideoUser.userId = @"mike"; 

TRTCVideoLayout* layout3 = [[TRTCVideoLayout alloc] init];
layout3.zOrder = 0;
layout3.rect = CGRectMake(1300, 220, 300, 200);
layout3.fixedVideoStreamType = TRTCVideoStreamTypeSub;
layout3.fixedVideoUser = nil;

[videoLayoutList addObject:layout1];
[videoLayoutList addObject:layout2];
[videoLayoutList addObject:layout3];
config.videoLayoutList = videoLayoutList;
config.audioMixUserList = nil;

[_trtcCloud startPublishMediaStream:target encoderParam:encoderParam mixingConfig:config];
```
:::
::: C++ C++
```
TRTCPublishTarget target;
target.mode = TRTCPublishMode::TRTCPublishMixStreamToCdn;

TRTCPublishCdnUrl* cdn_url = new TRTCPublishCdnUrl[1];
cdn_url[0].rtmpUrl = "rtmp://tencent/live/bestnews";
cdn_url[0].isInternalLine = true;
target.cdnUrlList = cdn_url;
target.cdnUrlListSize = 1;

TRTCStreamEncoderParam encoder_param;
encoder_param.videoEncodedWidth = 1280;
encoder_param.videoEncodedHeight = 720;
encoder_param.videoEncodedFPS = 15;
encoder_param.videoEncodedGOP = 3;
encoder_param.videoEncodedKbps = 1000;
encoder_param.audioEncodedSampleRate = 48000;
encoder_param.audioEncodedChannelNum = 1;
encoder_param.audioEncodedKbps = 50;
encoder_param.audioEncodedCodecType = 0;

TRTCStreamMixingConfig config;
TRTCVideoLayout* video_layout_list = new TRTCVideoLayout[3];

TRTCUser* fixedVideoUser0 = new TRTCUser();
fixedVideoUser0->intRoomId = 1234;
fixedVideoUser0->userId = "mike"; 
video_layout_list[0].zOrder = 0;
video_layout_list[0].rect.left = 0;
video_layout_list[0].rect.top = 0;
video_layout_list[0].rect.right = 720;
video_layout_list[0].rect.bottom = 1280;
video_layout_list[0].fixedVideoStreamType =
      TRTCVideoStreamType::TRTCVideoStreamTypeSub;
video_layout_list[0].fixedVideoUser = fixedVideoUser0;  

TRTCUser* fixedVideoUser1 = new TRTCUser();
fixedVideoUser1->intRoomId = 1234;
fixedVideoUser1->userId = "mike"; 
video_layout_list[1].zOrder = 0;
video_layout_list[1].rect.left = 1300;
video_layout_list[1].rect.top = 0;
video_layout_list[1].rect.right = 300;
video_layout_list[1].rect.bottom = 200;
video_layout_list[1].fixedVideoStreamType =
      TRTCVideoStreamType::TRTCVideoStreamTypeBig;
video_layout_list[1].fixedVideoUser = fixedVideoUser1;

video_layout_list[2].zOrder = 0;
video_layout_list[2].rect.left = 1300;
video_layout_list[2].rect.top = 220;
video_layout_list[2].rect.right = 300;
video_layout_list[2].rect.bottom = 200;
video_layout_list[2].fixedVideoStreamType =
      TRTCVideoStreamType::TRTCVideoStreamTypeSub;
video_layout_list[2].fixedVideoUser = nullptr;

config.videoLayoutList = video_layout_list;
config.videoLayoutListSize = 3;
config.audioMixUserList = nullptr;

trtc->startPublishMediaStream(&target, &encoder_param, &config);
delete fixedVideoUser0;
delete fixedVideoUser1;
delete[] video_layout_list;
```
:::
</dx-codeblock>

# FAQs

1. Can I listen for the status of CDN streams? What should I do if an error occurs?
You can listen for the `onCdnStreamStateChanged` callback event to get the latest status of a relay to CDN task. For details, see the [API documentation]().

2. How do I switch from publishing a single stream to publishing mixed streams? Do I need to stop publishing first and create a new relay task?
To switch from publishing a single stream to publishing mixed streams, just call `updatePublishMediaStream`, passing in the `taskid` of the current task. Note that, in order to ensure the stability of the publishing process, you cannot switch from publishing a single stream to mixing and publishing only audios or only videos. By default, both audio and video data are published when you publish a single stream. If you switch to publishing mixed streams, you must also publish both audios and videos.

3. How to mix only videos (without audio)?
Do not set the audio parameters in `TRTCStreamEncodeParam` and leave `audioMixUserList` of `TRTCStreamMixingConfig` empty.

4. Can I add watermarks to mixed streams?
Yes, you can use `watermarkList` of `TRTCStreamMixingConfig` to set watermarks. For details, see the [API documentation]().

5. In online learning scenarios, can I mix the screen shared by the teacher?
Yes, you can. We recommend you publish the screen as the substream and mix the teacher’s camera video and screen. When specifying the stream mixing parameters, set `fixedVideoStreamType` of `TRTCVideoLayout` to `TRTCVideoStreamTypeSub`.

6. When a preset layout is used, how are audios mixed?
When a preset layout is used, TRTC will mix the audios of up to 16 users in the room.

## Billing
### Cost calculation
Relay to CDN fees are charged based on the peak bandwidth used each month. If you mix streams, the MCU cluster will decode and re-encode the streams in the cloud, so an additional transcoding fee will be charged. Transcoding fees vary with the resolutions of the streams transcoded and the transcoding duration. For details, see [Billing of MixTranscoding and Relay to CDN](https://intl.cloud.tencent.com/document/product/647/47631).

### Cost control
If you use client-side APIs, stream mixing stops at the backend when either of the following conditions is met.
- The anchor who called `startPublishMediaStream` to mix streams left the room.
- The anchor called `stopPublishMediaStream` to stop mixing the streams.

In all other cases, TRTC will continue to mix streams in the cloud. Therefore, to reduce costs, when you no longer want to mix streams, please stop it using either of the above methods.
