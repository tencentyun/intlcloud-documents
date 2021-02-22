## Use Cases

In use cases such as [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and [on-cloud recording and playback](https://intl.cloud.tencent.com/document/product/647/35426), it is often necessary to mix multiple audio/video streams in a TRTC room into one, which can be achieved by using the On-cloud MixTranscoding cluster of the MCU on the Tencent Cloud server. The MCU cluster mixes multiple audio/video streams as required and distributes the generated video stream to the LVB CDN and on-cloud recording system.

You can control On-cloud MixTranscoding in the following methods:

- Method 1: use the RESTful APIs [StartMCUMixTranscode](https://intl.cloud.tencent.com/zh/document/product/647/37761) and [StopMCUMixTranscode](https://intl.cloud.tencent.com/zh/document/product/647/37760) on the server. These APIs also support enabling CDN relayed live streaming and on-cloud recording.
- Method 2: use the [setMixTranscodingConfig](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) API of the TRTC SDK on the client. The following diagram illustrates how it works: 
![](https://main.qcloudimg.com/raw/fd3017e7eb263b538fba858a362eab13.png)

>! Method 2 is supported only for SDKs for iOS, Android, Windows, macOS, and Electron.

## How It Works

On-cloud MixTranscoding involves three processes: decoding, mixing, and encoding:

- **Decoding**: MCU needs to decode multiple audio/video streams, including video decoding and audio decoding.
- **Mixing**: MCU needs to mix multiple image channels and implement a specific layout scheme according to the mixtranscoding command from the SDK. It also needs to mix the multiple decoded audio signals.
- **Encoding**: MCU needs to encode the mixed video and audio and mix them into one audio/video stream before sending it to downstream systems (such as LVB and recording).

![](https://main.qcloudimg.com/raw/a5ce0215228eca3375ce47133df0be95.png)

<span id="restapi"></span>

## Method 1. Mixing Through RESTful APIs on the Server

### Starting On-cloud MixTranscoding

The RESTful API [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) can be called by your server to start On-cloud MixTranscoding. For this API, you need to pay attention to the following details:

#### 1. Configuring the video image layout mode

Through the [LayoutParams](https://intl.cloud.tencent.com/document/product/647/36760#LayoutParams) parameter in `StartMCUMixTranscode`, you can set the following layout modes:
![](https://main.qcloudimg.com/raw/be0205b5f624679302e57ca5aa1b133f.png)

**Float layout template (LayoutParams.Template = 0)**

- The video of the first user to enter the room is played back in full screen, while videos of other users are played back in small images floating above the first user's video and arranged horizontally from the bottom-left corner.
- Small images float above the big image. There can be up to 4 small images per row and up to 4 rows in total.
- Up to 1 big image and 15 small images are supported.
- If a user only sends audio, the user will still occupy a position for displaying an image.

**9-grid template (LayoutParams.Template = 1)**

- Video images are in the same size for all users, dividing the screen into several equal parts. The more the users, the smaller the image size.
- Up to 16 images are supported. If a user only sends audio, the user will still occupy a position for displaying an image.

**Screen sharing template (LayoutParams.Template = 2)**

- It is suitable for video conferencing and online education.
- The screen shared by the speaker is always displayed as a big image on the left, while other users' screens are aligned vertically on the right.
- The `LayoutParams.MainVideoUserId` and `LayoutParams.MainVideoStreamType` parameters can be used to control what the primary image on the left shows.
- There can be up to 8 small images per column and up to 2 columns in total. Up to 1 big image and 15 small images are supported.
- If a user only sends audio, the user will still occupy a position for displaying an image.

**Picture-in-Picture template (LayoutParams.Template = 3)**

- This template mixes two video images in the room in the mode of "one big and one small, one front and one back", that is, one video in the room is played back in full screen, and the other video floats as a small image above the big image. The position of the small image can be specified by parameters.
- You can use the `MainVideoUserId` and `MainVideoStreamType` parameters in `LayoutParams` to specify the user ID and stream type of the big image.
- You can use the `SmallVideoLayoutParams` parameter in `LayoutParams` to specify the user ID, stream type, and layout position of the small image.
- Use case 1: in the online education scenario, the teacher's camera (usually as the small image) and screen (usually as the big image) can be mixed along with the voices of students in the room.
- Use case 2: in the 1v1 video call scenario, the remote user's screen (usually as the big image) and the local user's screen (usually as the small image) can be mixed.

**Custom template (LayoutParams.Template = 4)**

- It is suitable for scenarios where you need to customize the position of each video image. You can preset their positions through the `PresetLayoutConfig` parameter in `LayoutParams` (which is an array).
- You can skip specifying the `UserId` parameter in the `PresetLayoutConfig` array, and the layout engine will assign the users entering the room to each position specified in the `PresetLayoutConfig` array in the order of room entry.
- If one of the values in the `PresetLayoutConfig` array is specified with the `UserId` parameter, the layout engine will reserve the corresponding position in the screen for the specified user.
- If a user only upstreams audio without video, the user will still occupy a position for displaying an image.
- After the preset positions in the `PresetLayoutConfig` array are used up, the layout engine will no longer mix other users' images and voices.

>! The On-cloud MixTranscoding service supports up to 16 audio/video streams at the same time. If a user only has audio, the user will still occupy a stream.

#### 2. Configuring mixing and encoding parameters

Through the [EncodeParams](https://intl.cloud.tencent.com/document/product/647/36760#EncodeParams) parameter in `StartMCUMixTranscode`, you can set the mixing and encoding parameters:

| Name            | Description                                         | Recommended Value |
| --------------- | -------------------------------------------- | ------ |
| AudioSampleRate | Audio sample rate of output stream for mixtranscoding                        | 48000  |
| AudioBitrate    | Output stream audio bitrate in Kbps for mixtranscoding               | 64     |
| AudioChannels   | Number of sound channels of output stream for mixtranscoding                        | 2      |
| VideoWidth      | Output stream width for mixtranscoding, which is required for audio/video output              | Custom |
| VideoHeight     | Output stream height for mixtranscoding, which is required for audio/video output              | Custom |
| VideoBitrate    | Output stream bitrate in Kbps for mixtranscoding, which is required for audio/video output | Custom |
| VideoFramerate  | Output stream frame rate for mixtranscoding, which is required for audio/video output            | 15     |
| VideoGop        | Output stream GOP for mixtranscoding, which is required for audio/video output            | 3      |
| BackgroundColor | Output stream background color for mixtranscoding                           | Custom |

#### 3. Configuring whether to enable on-cloud recording

Through the [OutputParams](https://intl.cloud.tencent.com/document/product/647/36760#OutputParams) parameter in `StartMCUMixTranscode`, you can specify the destination of the video stream after mix.

- **OutputParams.RecordId**
This parameter is used to configure whether to enable [on-cloud recording](https://intl.cloud.tencent.com/document/product/647/35426). If you use it to enable on-cloud recording, the mixed audio/video streams will be recorded and saved as files on [VOD](https://intl.cloud.tencent.com/product/vod). The recording files are named in the format of `OutputParams.RecordId_start time_end time`, such as `file001_2020-02-16-12-12-12_2020-02-16-13-13-13`.
- **OutputParams.RecordAudioOnly**
  If you want to record audio only, set the `OutputParams.RecordAudioOnly` parameter to 1, indicating that streams will be recorded as .mp3 files.

#### 4. Configuring whether to enable CDN relayed live streaming

- **OutputParams.StreamId**
  This parameter is used to configure whether to enable [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242). If you use it to enable CDN relayed live streaming, the mixed audio/video streams are sent to the [LVB system](https://intl.cloud.tencent.com/product/LVB). However, you cannot playback the stream with CDN before you activate LVB and configure a playback domain name.
- **OutputParams.PureAudioStream**
  If you want audio live streaming only, set the `OutputParams.PureAudioStream` parameter to 1, indicating that only mixed audio streams will be forwarded to CDN.

### Ending On-cloud MixTranscoding

Call the RESTful API [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) from your server to end mixtranscoding.

<span id="sdkapi"></span>

## Method 2. Mixing Through SDK APIs on the Client

A mixtranscoding command can be easily initiated with the TRTC SDK by calling the corresponding [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) API for your platform. The SDK currently provides four commonly used mixtranscoding schemes:

<table>
<thead>
<tr>
<th>Parameter</th>
<th width="10%">PureAudio</th>
<th width="10%">PresetLayout</th>
<th width="10%">ScreenSharing</th>
<th>Manual</th>
</tr>
</thead>
<tbody><tr>
<td>Number of calls</td>
<td>Only one call of the API is required</td>
<td>Only one call of the API is required</td>
<td>Only one call of the API is required</td>
<td>The mixtranscoding API needs to be called in the following scenarios: <li>A co-anchor joins</li><li>A co-anchor leaves</li><li>A co-anchor enables/disables the camera</li><li>A co-anchor enables/disables the mic</li></td>
</tr>
<tr>
<td>Content to be mixed</td>
<td>Audio only</td>
<td>Customizable content</td>
<td>Video image at the student end is not mixed</td>
<td>Customizable content</td>
</tr>
<tr>
<td>audioSampleRate</td>
<td>48000 is recommended</td>
<td>48000 is recommended</td>
<td>48000 is recommended</td>
<td>48000 is recommended</td>
</tr>
<tr>
<td>audioBitrate</td>
<td>64 is recommended</td>
<td>64 is recommended</td>
<td>64 is recommended</td>
<td>64 is recommended</td>
</tr>
<tr>
<td>audioChannels</td>
<td>2 is recommended</td>
<td>2 is recommended</td>
<td>2 is recommended</td>
<td>2 is recommended</td>
</tr>
<tr>
<td>videoWidth</td>
<td>No need to set</td>
<td>It cannot be 0</td>
<td>0 is recommended</td>
<td>It cannot be 0</td>
</tr>
<tr>
<td>videoHeight</td>
<td>No need to set</td>
<td>It cannot be 0</td>
<td>0 is recommended</td>
<td>It cannot be 0</td>
</tr>
<tr>
<td>videoBitrate</td>
<td>No need to set</td>
<td>It cannot be 0</td>
<td>0 is recommended</td>
<td>It cannot be 0</td>
</tr>
<tr>
<td>videoFramerate</td>
<td>No need to set</td>
<td>15 is recommended</td>
<td>15 is recommended</td>
<td>15 is recommended</td>
</tr>
<tr>
<td>videoGOP</td>
<td>No need to set</td>
<td>3 is recommended</td>
<td>3 is recommended</td>
<td>3 is recommended</td>
</tr>
<tr>
<td>mixUsers array</td>
<td>No need to set</td>
<td>Set with a placeholder</td>
<td>No need to set</td>
<td>Set with a real `userId`</td>
</tr>
</tbody></table>


<span id="PureAudio"></span>

### PureAudio

#### Use cases

The PureAudio mode is suitable for pure audio applications such as audio call (AudioCall) and voice chat room (VoiceChatRoom), where you can set parameters when calling the [enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) API of the SDK.
In PureAudio mode, the SDK will automatically mix multiple audio streams in a room into one.

#### Directions

1. When calling the `enterRoom()` function to enter the room, set the `AppScene` parameter to `TRTCAppSceneAudioCall` or `TRTCAppSceneVoiceChatRoom` based on your business needs to make it clear that there is no video but only audio in the current room.
2. Enable [relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and set the `streamId` parameter in `TRTCParams` to specify the destination of the mixed audio/video stream output by MCU.
3. Call `startLocalAudio()` to enable local audio capturing and audio upstreaming.
>? As On-cloud MixTranscoding essentially mixes multiple streams into the audio/video stream of the current user (i.e., the mixtranscoding command initiator), the current user must have upstream audio before streams can be mixed.
4. Call the `setMixTranscodingConfig()` API to enable On-cloud MixTranscoding, set the `mode` parameter in `TRTCTranscodingConfig` to **TRTCTranscodingConfigMode_Template_PureAudio**, and specify the parameters that affect the audio output quality such as `audioSampleRate`, `audioBitrate`, and `audioChannels`.
5. After the above steps are performed, the relayed audio stream of the current user will be automatically mixed with audios of other users in the room, and then you can configure a playback domain name for relayed live streaming as described in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242) or record the mixed audio stream as described in [On-cloud Recording](https://intl.cloud.tencent.com/document/product/647/35426).

>! In PureAudio mode, you don't need to call the `setMixTranscodingConfig()` API multiple times; instead, you only need to call it once after successfully entering the room and enabling local audio upstreaming.

<span id="PresetLayout"></span>

### PresetLayout

#### Use cases

The PresetLayout mode is suitable for applications involving both audio and video such as video call (VideoCall) and interactive live streaming (LIVE), where you can set parameters when calling the [enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) API of the SDK.
In PresetLayout mode, the SDK will automatically mix multiple audio/video streams in a room into one according to the video layout rules you preset.

#### Directions

1. When calling the `enterRoom()` function to enter the room, set the `AppScene` parameter to `TRTCAppSceneVideoCall` or `TRTCAppSceneLIVE` based on your business needs.
2. Enable [relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and set the `streamId` parameter in `TRTCParams` to specify the destination of the mixed audio/video stream output by MCU.
3. Call `startLocalPreview()` and `startLocalAudio()` to enable local audio/video upstreaming.
>? As On-cloud MixTranscoding essentially mixes multiple streams into the audio/video stream of the current user (i.e., the mixtranscoding command initiator), the current user must have upstream audio/video before streams can be mixed.
4. Call the `setMixTranscodingConfig()` API to enable On-cloud MixTranscoding, set the `mode` parameter in `TRTCTranscodingConfig` to **TRTCTranscodingConfigMode_Template_PresetLayout**, and specify the parameters that affect the audio output quality such as `audioSampleRate`, `audioBitrate`, and `audioChannels` as well as the parameters that affect the video output quality such as `videoWidth`, `videoHeight`, `videoBitrate`, and `videoFramerate`.
5. Assemble the `mixUser` parameter. In PresetLayout mode, use three placeholders **$PLACE_HOLDER_REMOTE$**, **$PLACE_HOLDER_LOCAL_MAIN$**, and **$PLACE_HOLDER_LOCAL_SUB$** for the `userId` parameter in `mixUser`, which are described as follows:
<table>
<tr><th>Placeholder</th><th>Description</th><th>Multiple Occurrences Allowed</th></tr><tr>
<td>$PLACE_HOLDER_LOCAL_MAIN$</td><td>Local camera</td><td>No</td>
</tr><tr>
<td>$PLACE_HOLDER_LOCAL_SUB$</td><td>Local screen sharing (only image)</td><td>No</td>
</tr><tr>
<td>$PLACE_HOLDER_REMOTE$</td><td>Remote co-anchor. Multiple ones can be set at the same time</td><td>Yes</td>
</tr></table>
6. After the above steps are performed, the relayed audio stream of the current user will be automatically mixed with audios of other users in the room, and then you can configure a playback domain name for relayed live streaming as described in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242) or record the mixed audio stream as described in [On-cloud Recording](https://intl.cloud.tencent.com/document/product/647/35426).
![](https://main.qcloudimg.com/raw/4119e41cefe59b7a8b8edf675babdd38.png)

#### Sample code

This document uses the Objective-C code for iOS as an example to describe how to mix streams in order to display one big video image and two small ones at the same time with the small ones on top.

``` Objective-C
TRTCTranscodingConfig *config = [[TRTCTranscodingConfig alloc] init];
// Set the resolution to 720x1280 px, bitrate to 1,500 Kbps, and frame rate to 20 fps
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
// Use the PresetLayout mode
config.mode = TRTCTranscodingConfigMode_Template_PresetLayout;
config.mixUsers = [NSMutableArray new];

// Camera image position of anchor
TRTCMixUser* local = [TRTCMixUser new];
local.userId = @"$PLACE_HOLDER_LOCAL_MAIN$"; 
local.zOrder = 0;   // `zOrder` value of 0 indicates that the anchor's video image is at the bottom
local.rect   = CGRectMake(0, 0, videoWidth, videoHeight);
local.roomID = nil; // `roomID` needs to be specified for a remote user but not the local user
[config.mixUsers addObject:local];
		
// Video image position of co-anchor
TRTCMixUser* remote1 = [TRTCMixUser new];
remote1.userId = @"$PLACE_HOLDER_REMOTE$"; 
remote1.zOrder = 1;
remote1.rect   = CGRectMake(400, 800, 180, 240); // For reference only
remote1.roomID = 97392; // `roomID` needs to be specified for a remote user but not the local user
[config.mixUsers addObject:remote1];

// Video image position of co-anchor
TRTCMixUser* remote2 = [TRTCMixUser new];
remote2.userId = @"$PLACE_HOLDER_REMOTE$"; 
remote2.zOrder = 1;
remote2.rect   = CGRectMake(400, 500, 180, 240); // For reference only
remote2.roomID = 97392; // `roomID` needs to be specified for a remote user but not the local user
[config.mixUsers addObject:remote2];
		
// Initiate the On-cloud MixTranscoding service
[_trtc setMixTranscodingConfig:config];
```

>! In PresetLayout mode, you don't need to call the `setMixTranscodingConfig()` API multiple times; instead, you only need to call it once after successfully entering the room and enabling local audio upstreaming.

<span id="ScreenSharing"></span>

### ScreenSharing

#### Use cases

The ScreenSharing mode is suitable for applications such as online education and interactive classrooms, where you can set the `AppScene` parameter to `TRTCAppSceneLIVE` when calling the [enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) API of the SDK.
In ScreenSharing mode, the SDK will first build a canvas based on the target resolution you select. If the teacher does not enable ScreenSharing, the SDK will scale up the camera image proportionally and draw it onto the canvas. After the teacher enables ScreenSharing, the SDK will draw the video image shared on the screen onto the same canvas. By building a canvas, you can ensure consistency in the output resolution of the mixtranscoding module in order to prevent video compatibility issues between recording and webpage playback (common players do not support videos whose resolution changes).

#### Directions

1. When calling the `enterRoom()` function to enter the room, set the `AppScene` parameter to `TRTCAppSceneLIVE` based on your business needs.
2. Enable [relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and set the `streamId` parameter in `TRTCParams` to specify the destination of the mixed audio/video stream output by MCU.
3. Call `startLocalPreview()` and `startLocalAudio()` to enable local audio/video upstreaming.

>? As On-cloud MixTranscoding essentially mixes multiple streams into the audio/video stream of the current user (i.e., the mixtranscoding command initiator), the current user must have upstream audio/video before streams can be mixed.

4. Call the `setMixTranscodingConfig()` API to enable On-cloud MixTranscoding, set the `mode` parameter in `TRTCTranscodingConfig` to **TRTCTranscodingConfigMode_Template_ScreenSharing**, and specify the parameters that affect the audio output quality such as `audioSampleRate`, `audioBitrate`, and `audioChannels` as well as the parameters that affect the video output quality such as `videoWidth`, `videoHeight`, `videoBitrate`, and `videoFramerate`.

 >?If both the `videoWidth` and `videoHeight` parameters are specified as 0, the SDK will automatically calculate a suitable resolution based on the aspect ratio of the user's current screen.

5. After the above steps are performed, the relayed audio stream of the current user will be automatically mixed with audios of other users in the room, and then you can configure a playback domain name for relayed live streaming as described in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242) or record the mixed audio stream as described in [On-cloud Recording](https://intl.cloud.tencent.com/document/product/647/35426).
![](https://main.qcloudimg.com/raw/675e67bfaff40451b60a21aa403217d4.gif)

>! 
>
>- The ScreenSharing mode only supports Windows and macOS.
>- In ScreenSharing mode, you don't need to call the `setMixTranscodingConfig()` API multiple times; instead, you only need to call it once after successfully entering the room and enabling local audio upstreaming.
>- As video content is primarily the shared screen in teaching mode, and it is a waste of bandwidth to transmit camera image and screen image at the same time, it is recommended to draw the camera image and the video images of students onto the current screen through the `setLocalVideoRenderCallback()` and `setRemoteVideoRenderCallback()` APIs.
>- By specifying the `videoWidth` and `videoHeight` parameters in `TRTCTranscodingConfig` as 0, you can let the SDK select the output resolution intelligently. For example, if the teacher's current screen width is smaller than 1920 px, the SDK will use the actual resolution of the teacher's current screen; otherwise, the SDK will select 1920x1080 (16:9), 1920x1200 (16:10), or 1920x1440 (4:3) based on the current screen aspect ratio.

<span id="Manual"></span>

### Manual

#### Use cases

The Manual mode is suitable for applications for which none of the above automatic modes are suitable. It is most flexible and can implement various mixtranscoding schemes through free combinations, but it is most difficult to use.
In Manual mode, you need to set all the parameters in `TRTCTranscodingConfig` and listen on the `onUserVideoAvailable()` and `onUserAudioAvailable()` callbacks in `TRTCCloudDelegate` so as to constantly adjust the `mixUsers` parameter according to the audio/video status of each user with mic on in the current room; otherwise, mixtranscoding will fail.

#### Directions

1. When calling the `enterRoom()` function to enter the room, set the `AppScene` parameter based on your business needs.
2. Enable [relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and set the `streamId` parameter in `TRTCParams` to specify the destination of the mixed audio/video stream output by MCU.
3. Call `startLocalAudio()` to enable local audio upstreaming (or also call `startLocalPreview()` to enable video upstreaming) based on your business needs.
>? As On-cloud MixTranscoding essentially mixes multiple streams into the audio/video stream of the current user (i.e., the mixtranscoding command initiator), the current user must have upstream audio/video before streams can be mixed.
4. Call the `setMixTranscodingConfig()` API to enable On-cloud MixTranscoding, set the `mode` parameter in `TRTCTranscodingConfig` to **TRTCTranscodingConfigMode_Manual**, and specify the parameters that affect the audio output quality such as `audioSampleRate`, `audioBitrate`, and `audioChannels`. If your business scenario involves video, you also need to set the parameters that affect the video output quality such as `videoWidth`, `videoHeight`, `videoBitrate`, and `videoFramerate`.
5. Listen on the `onUserVideoAvailable()` and `onUserAudioAvailable()` callbacks in `TRTCCloudDelegate` and specify the **mixUsers** parameter as needed.
 >?Different from the PresetLayout mode, the Manual mode requires you to specify the `userId` parameter in each `mixUser` as the real co-anchor ID and set the `pureAudio` parameter in `mixUser` based on whether the co-anchor has enabled video.
6. After the above steps are performed, the relayed audio stream of the current user will be automatically mixed with audios of other users in the room, and then you can configure a playback domain name for relayed live streaming as described in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242) or record the mixed audio stream as described in [On-cloud Recording](https://intl.cloud.tencent.com/document/product/647/35426).

>! In Manual mode, you need to listen on the mic-on/off actions of co-anchors in the room and call the `setMixTranscodingConfig()` API multiple times based on the number and audio/video status of the co-anchors.

## Applicable Fees

### Calculating fees

To perform On-cloud MixTranscoding, the audio/video streams input to the MCU cluster need to be decoded, re-encoded, and then output, which will incur additional fees. Therefore, TRTC will charge additional value-added service fees to users who use the MCU cluster for On-cloud MixTranscoding. Such fees are billed based on the **transcoding output resolution** and **transcoding duration**. The higher the transcoding output resolution and the longer the transcoding duration, the higher the fees. For more information, please see [On-cloud MixTranscoding Billing Overview](https://intl.cloud.tencent.com/zh/document/product/647/38929).

### Saving costs

- **Under the server RESTful API-based On-cloud MixTranscoding scheme, to stop On-cloud MixTranscoding**, one of the following conditions must be met:
  - All users (including the anchor and viewers) have left the room.
  - The RESTful API [StopMCUMixTranscode](https://intl.cloud.tencent.com/zh/document/product/647/37760) is called to actively stop On-cloud MixTranscoding.
- **Under the client SDK API-based On-cloud MixTranscoding scheme, to stop On-cloud MixTranscoding**, one of the following conditions must be met:
  - The anchor who initiated On-cloud MixTranscoding (by calling the client API `setMixTranscodingConfig`) has exited the room.
  - [setMixTranscodingConfig](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) is called with the parameter set to `nil/null` to actively stop On-cloud MixTranscoding.

In other cases, TRTC will try its best to maintain On-cloud MixTranscoding continuously. Therefore, to avoid unexpected costs, please end On-cloud MixTranscoding in the above methods as soon as possible when it is no longer needed.


