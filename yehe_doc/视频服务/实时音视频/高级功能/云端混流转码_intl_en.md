## Use Cases

In scenarios such as [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and [on-cloud recording](https://intl.cloud.tencent.com/document/product/647/35426), you may need to mix multiple audio and video streams in a TRTC room into one stream, which can be achieved using TRTC’s stream mixing and transcoding MCU cluster. The MCU cluster can mix multiple audio and video streams as needed and distribute the mixed stream to live streaming CDNs and the on-cloud recording system.

You can enable or disable On-Cloud MixTranscoding using the following methods.

- **Method 1**: via the server-side RESTful APIs `StartMCUMixTranscode` (for [numeric room ID](https://intl.cloud.tencent.com/document/product/647/37761)/[string-type room ID](https://intl.cloud.tencent.com/document/product/647/39637)) and `StopMCUMixTranscode` (for [numeric room ID](https://intl.cloud.tencent.com/document/product/647/37760)/[string-type room ID](https://intl.cloud.tencent.com/document/product/647/39636)), which can also be used to enable and disable CDN relayed live streaming and on-cloud recording.
- **Method 2**: via the client-side API [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93). The figure below explains how it works. 
  ![](https://main.qcloudimg.com/raw/fd3017e7eb263b538fba858a362eab13.png)

>! Method 2 can be used in TRTC SDK for iOS, Android, Windows, macOS, Electron, Flutter, and desktop browsers.

## How It Works

On-Cloud MixTranscoding involves three processes: decoding, mixing, and encoding.

- **Decoding**: the MCU decodes multiple audio and video streams.
- **Mixing**: the MCU mixes multiple channels of images and arranges the images according to the layout template specified in the stream mixing command from the SDK. It also mixes the decoded audio signals of different channels.
- **Encoding**: the MCU encodes the mixed video and audio and mixes them into a single stream before sending it to the downstream system (e.g., live streaming or recording).

![](https://main.qcloudimg.com/raw/fd3017e7eb263b538fba858a362eab13.png)

[](id:restapi)

## Method 1: Using Server-Side RESTful APIs

### Enabling On-Cloud MixTranscoding

Call the RESTful API [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) from your server to enable On-Cloud MixTranscoding. Finish the following configurations during the process.

[](id:restapi_step1)

#### 1. Set the image layout mode (required)
Use [LayoutParams](https://intl.cloud.tencent.com/document/product/647/36760#LayoutParams) in `StartMCUMixTranscode` to select one of the following layout templates.
![](https://main.qcloudimg.com/raw/be0205b5f624679302e57ca5aa1b133f.png)

**Floating (LayoutParams.Template = 0)**

- The entire screen is covered by the video image of the first user who enters the room, and the images of other users are displayed as small images in horizontal rows in the bottom-left corner in room entry sequence.
- The screen can accommodate up to 4 rows of 4 small images each, which float over the big image.
- Up to 1 big image and 15 small images can be displayed.
- A user sending audio only still occupies an image spot.

**Grid (LayoutParams.Template = 1)**

- The images of all users split the screen evenly. The more the users, the smaller the image dimensions.
- Up to 16 images can be displayed. A user sending audio only still occupies an image spot.

**Screen sharing (LayoutParams.Template = 2)**

- This template is designed for video conferencing and online classes.
- The shared screen (or camera image of the anchor) is always displayed as the big image, which occupies the left side of the screen, and the images of other users stack in the right side.
- Use `LayoutParams.MainVideoUserId` and `LayoutParams.MainVideoStreamType` to specify the image displayed as the big image on the left.
- Up to 2 columns of a maximum of 8 small images each can be displayed. There can be 1 big image and 15 small images at most.
- A user sending audio only still occupies an image spot.

**Picture-in-picture (LayoutParams.Template = 3)**

- This template mixes a big image with a small image. The big image covers the entire screen, and the small image floats over the big image. You can specify the position of the small image.
- Use `MainVideoUserId` and `MainVideoStreamType` in `LayoutParams` to specify the user ID whose image is displayed as the big image and the stream type.
- Use `SmallVideoLayoutParams` in `LayoutParams` to specify the user ID whose image is displayed as the small image, the stream type, and the position of the image.
- Use case 1: during an online class, the template may mix the teacher’s camera image (usually displayed as the small image) and screen (usually displayed as the big image), as well as the audio of students.
- Use case 2: in a one-to-one video call, the template may mix the image of the remote user (usually displayed as the big image) and that of the local user (usually displayed as the small image).

**Custom (LayoutParams.Template = 4)**

- Custom templates allow you to specify the image position of each user. You can use `PresetLayoutConfig` (an array) to preset the position of each image in stream mixing.
- If you do not set `UserId` in `PresetLayoutConfig`, the layout engine will assign users to the positions specified by `PresetLayoutConfig` in room entry sequence.
- If you specify a `UserId` in `PresetLayoutConfig`, the layout engine will reserve the position for the specified user.
- A user sending audio only still occupies an image spot.
- When all positions specified by `PresetLayoutConfig` are occupied, the layout engine will stop mixing the video and audio of other users.

>! On-Cloud MixTrancoding can mix up to 16 audio and video streams at a time. A user sending audio only still counts as a stream.

[](id:restapi_step2)
#### 2. Set encoding parameters for stream mixing (required)
Use [EncodeParams](https://intl.cloud.tencent.com/ko/document/product/647/36760#EncodeParams) in `StartMCUMixTranscode` to set the following encoding parameters.

| Parameter            | Description                                         | Recommended Value |
| --------------- | -------------------------------------------- | ------ |
| AudioSampleRate | Audio sample rate                         | 48000  |
| AudioBitrate    | Audio bitrate (Kbps)               | 64     |
| AudioChannels   | Number of sound channels                         | 2      |
| VideoWidth      | Video width, required for audio-video output              | Custom |
| VideoHeight     | Video height, required for audio-video output              | Custom |
|VideoBitrate        | Video bitrate, in Kbps, required for audio-video output | Custom |
| VideoFramerate  | Frame rate, required for audio-video output            | 15     |
| VideoGop        | GOP, required for audio-video output            | 3      |
| BackgroundColor | Background color                            | Custom |

[](id:restapi_step4)
#### 3. Specify a `streamID` for the mixed stream (required)
- **OutputParams.StreamId**
  Use this parameter to specify a `streamID` for the mixed stream in CSS CDN. You can play back this stream only if you have activated CSS and configured a playback domain name.
- **OutputParams.PureAudioStream**
  If you want to stream audio only, set the `OutputParams.PureAudioStream` parameter to `1`, and only audio data will be forwarded to CDNs after stream mixing.

[](id:restapi_step3)
#### 4. Set whether to enable on-cloud recording (optional)
- **OutputParams.RecordId**
  Use this parameter to specify whether to enable [on-cloud recording](https://intl.cloud.tencent.com/document/product/647/35426). If you enable on-cloud recording, mixed streams will be recorded and saved in [VOD](https://intl.cloud.tencent.com/product/vod). The recording files are named in the format of `OutputParams.RecordId_start time_end time`, e.g. `file001_2020-02-16-12-12-12_2020-02-16-13-13-13`.
- **OutputParams.RecordAudioOnly**
  If you want to record audio only, set the `OutputParams.RecordAudioOnly` parameter to `1`, and mixed streams will be recorded as MP3 files.

### Stopping On-Cloud MixTranscoding

Call the RESTful API [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) from your server to stop On-Cloud MixTranscoding.

[](id:sdkapi)

## Method 2: Using Client-Side SDK APIs

Sending a stream mixing command using the TRTC SDK is simple. Just call the [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) API. The TRTC SDK offers four stream mixing modes currently.

<table>
<thead><tr><th>Parameter</th>
<th width="10%">Audio-only Mode (`PureAudio`)</th>
<th width="10%">Preset Layout Mode (`PresetLayout`)</th>
<th width="10%">Screen Sharing Mode (`ScreenSharing`)</th>
<th>Manual Mode (`Manual`)</th>
</tr></thead>
<tbody><tr>
<td>Call</td>
<td>Once</td>
<td>Once</td>
<td>Once</td>
<td>You need to call the stream mixing API whenever one of the following happens: <li>A co-anchor joins. </li><li>A co-anchor leaves. </li><li>A co-anchor turns on/off the camera. </li><li>A co-anchor turns on/off the mic.</li></td>
</tr><tr>
<td>Mixed content</td>
<td>Audio only</td>
<td>You can specify the content to be mixed for each channel.</td>
<td>Students’ videos are not mixed.</td>
<td>You can specify the content to be mixed for each channel.</td>
</tr><tr>
<td>audioSampleRate</td>
<td>48000 is recommended.</td>
<td>48000 is recommended.</td>
<td>48000 is recommended.</td>
<td>48000 is recommended.</td>
</tr><tr>
<td>audioBitrate</td>
<td>64 is recommended.</td>
<td>64 is recommended.</td>
<td>64 is recommended.</td>
<td>64 is recommended.</td>
</tr><tr>
<td>audioChannels</td>
<td>2 is recommended.</td>
<td>2 is recommended.</td>
<td>2 is recommended.</td>
<td>2 is recommended.</td>
</tr>
<tr><td>videoWidth</td>
<td>-</td>
<td>Cannot be 0</td>
<td>0 is recommended.</td>
<td>Cannot be 0</td>
</tr><tr>
<td>videoHeight</td>
<td>-</td>
<td>Cannot be 0</td>
<td>0 is recommended.</td>
<td>Cannot be 0</td>
</tr><tr>
<td>videoBitrate</td>
<td>-</td>
<td>Cannot be 0</td>
<td>0 is recommended.</td>
<td>Cannot be 0</td>
</tr><tr>
<td>videoFramerate</td>
<td>-</td>
<td>15 is recommended.</td>
<td>15 is recommended.</td>
<td>15 is recommended.</td>
</tr><tr>
<td>videoGOP</td>
<td>-</td>
<td>3 is recommended.</td>
<td>3 is recommended.</td>
<td>3 is recommended.</td>
</tr><tr>
<td>mixUsers array</td>
<td>-</td>
<td>Use placeholders for the setting.</td>
<td>-</td>
<td>Use actual `userIds` for the setting.</td>
</tr></tbody></table>


[](id:PureAudio)

### Audio-only mode (`PureAudio`)

#### Use cases

The audio-only mode is suitable for scenarios such as audio calls (`AudioCall`) and audio chat rooms (`VoiceChatRoom`). You can select this mode when calling the [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) API of the SDK.
In this mode, the SDK automatically mixes all the audio streams in a room into one stream.

#### Directions

1. When calling the `enterRoom()` function to enter a room, set the `AppScene` parameter to `TRTCAppSceneAudioCall` or `TRTCAppSceneVoiceChatRoom`, which indicates that there will be only audio in the room.
2. Enable [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and specify the `streamId` parameter in `TRTCParams` for mixed streams.
3. Call `startLocalAudio()` to enable local audio capturing and uploading.
>? On-Cloud MixTranscoding mixes multiple streams into the stream of the current user, i.e., the user who sends the stream mixing command. Therefore, stream mixing works only if the current user is sending audio.
4. Call the `setMixTranscodingConfig()` API to enable On-Cloud MixTranscoding. You need to set the `mode` parameter in `TRTCTranscodingConfig` to **TRTCTranscodingConfigMode_Template_PureAudio**, and specify audio quality-related parameters such as `audioSampleRate`, `audioBitrate`, and `audioChannels`.
5. After the above steps are performed, the audio of other users in the room will be automatically mixed into the relayed audio stream of the current user. You can then follow the instructions in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242) to configure a playback domain name for relayed live streaming or record the mixed audio stream as described in [On-Cloud Recording](https://intl.cloud.tencent.com/document/product/647/35426).

>! In the audio-only mode, you only need to call the `setMixTranscodingConfig()` API once after entering a room and enabling local audio publishing.

[](id:PresetLayout)
### Preset layout mode
#### Use cases
The preset layout mode is suitable for scenarios that involve the transfer of both audio and video, such as video calls (`VideoCall`) and interactive live streaming (`LIVE`). You can select this mode when calling the [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) API of the SDK.
In the preset layout mode, the SDK automatically mixes multiple audio and video streams in a room into one stream according to the preset layout rules.

#### Directions
1. When calling the `enterRoom()` function to enter a room, set the `AppScene` parameter to `TRTCAppSceneVideoCall` or `TRTCAppSceneLIVE`, whichever fits your needs.
2. Enable [relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and specify the `streamId` parameter in `TRTCParams` for mixed streams.
3. Call `startLocalPreview()` and `startLocalAudio()` to enable local audio and video publishing.
>? On-Cloud MixTranscoding mixes multiple streams into the stream of the current user, i.e., the user who sends the stream mixing command. Therefore, stream mixing works only if the current user is sending audio and video.
4. Call the `setMixTranscodingConfig()` API to enable On-Cloud MixTranscoding. You need to set the `mode` parameter in `TRTCTranscodingConfig` to **TRTCTranscodingConfigMode_Template_PresetLayout**, and specify audio quality-related parameters such as `audioSampleRate`, `audioBitrate`, and `audioChannels`, as well as video quality-related parameters such as `videoWidth`, `videoHeight`, `videoBitrate`, and `videoFramerate`.
5. Assemble the `mixUser` parameter. In the preset layout mode, you must set `userId` to a placeholder, which could be **$PLACE_HOLDER_REMOTE$**, **$PLACE_HOLDER_LOCAL_MAIN$**, or **$PLACE_HOLDER_LOCAL_SUB$**. Their meanings are described below.
<table>
<tr><th>Placeholder</th><th>Description</th><th>Multiple Allowed</th></tr><tr>
<td>$PLACE_HOLDER_LOCAL_MAIN$</td><td>Local camera image</td><td>No</td>
</tr><tr>
<td>$PLACE_HOLDER_LOCAL_SUB$</td><td>Local screen sharing image (image only)</td><td>No</td>
</tr><tr>
<td>$PLACE_HOLDER_REMOTE$</td><td>Remote co-anchor(s)</td><td>Yes</td>
</tr></table>
6. After the above steps are performed, the audio of other users in the room will be automatically mixed into the relayed audio stream of the current user. You can then follow the instructions in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242) to configure a playback domain name for relayed live streaming or record the mixed audio stream as described in [On-Cloud Recording](https://intl.cloud.tencent.com/document/product/647/35426).

![](https://main.qcloudimg.com/raw/4119e41cefe59b7a8b8edf675babdd38.png)

[](id:example_code)

#### Sample code
You can use the code below to implement a layout where two vertically stacked small images float over a big image.
<dx-codeblock>
::: iOS  Objective-C 
TRTCTranscodingConfig *config = [[TRTCTranscodingConfig alloc] init];
// Set the resolution to 720 x 1280 px, bitrate to 1500 Kbps, and frame rate to 20 FPS
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
    
NSMutableArray *mixUsers = [NSMutableArray new];
// Position of the camera image of the anchor
TRTCMixUser* local = [TRTCMixUser new];
local.userId = @"$PLACE_HOLDER_LOCAL_MAIN$";
local.zOrder = 0;   // When `zOrder` is set to `0`, it indicates that the anchor's image is displayed at the bottom.
local.rect   = CGRectMake(0, 0, videoWidth, videoHeight);
local.roomID = nil; // Required for remote users but not for the local user
[mixUsers addObject:local];

// Image position of co-anchor
TRTCMixUser* remote1 = [TRTCMixUser new];
remote1.userId = @"$PLACE_HOLDER_REMOTE$";
remote1.zOrder = 1;
remote1.rect   = CGRectMake(400, 800, 180, 240); // For reference only
remote1.roomID = @"97392"; // Required for remote users but not for the local user
[mixUsers addObject:remote1];

// Image position of co-anchor
TRTCMixUser* remote2 = [TRTCMixUser new];
remote2.userId = @"$PLACE_HOLDER_REMOTE$";
remote2.zOrder = 1;
remote2.rect   = CGRectMake(400, 500, 180, 240); // For reference only
remote2.roomID = @"97392"; // Required for remote users but not for the local user
[mixUsers addObject:remote2];

config.mixUsers = mixUsers;
// Enable On-Cloud MixTranscoding
[_trtc setMixTranscodingConfig:config];
:::
::: Android java
TRTCCloudDef.TRTCTranscodingConfig config = new TRTCCloudDef.TRTCTranscodingConfig();
// Set the resolution to 720 x 1280 px, bitrate to 1500 Kbps, and frame rate to 20 FPS
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;

// Use the preset layout mode
config.mode = TRTCCloudDef.TRTC_TranscodingConfigMode_Template_PresetLayout;
config.mixUsers = new ArrayList<>();

// Position of the camera image of the anchor
TRTCCloudDef.TRTCMixUser local = new TRTCCloudDef.TRTCMixUser();
local.userId = "$PLACE_HOLDER_LOCAL_MAIN$";
local.zOrder = 0;   // When `zOrder` is set to `0`, it indicates that the anchor's image is displayed at the bottom
local.x      = 0;
local.y      = 0;
local.width  = videoWidth;
local.height = videoHeight;
local.roomId = null; // Required for remote users but not for the local user
config.mixUsers.add(local);

// Image position of co-anchor
TRTCCloudDef.TRTCMixUser remote1 = new TRTCCloudDef.TRTCMixUser();
remote1.userId = "$PLACE_HOLDER_REMOTE$";
remote1.zOrder = 1;
remote1.x      = 400; // For reference only
remote1.y      = 800; // For reference only
remote1.width  = 180; // For reference only
remote1.height = 240; // For reference only
remote1.roomId = 97392; // Required for remote users but not for the local user
config.mixUsers.add(remote1);

// Image position of co-anchor
TRTCCloudDef.TRTCMixUser remote2 = new TRTCCloudDef.TRTCMixUser();
remote2.userId = "$PLACE_HOLDER_REMOTE$";
remote2.zOrder = 1;
remote1.x      = 400; // For reference only
remote1.y      = 500; // For reference only
remote1.width  = 180; // For reference only
remote1.height = 240; // For reference only
remote1.roomId = 97393; // Required for remote users but not for the local user
config.mixUsers.add(remote2);

// Enable On-Cloud MixTranscoding.
trtc.setMixTranscodingConfig(config);
:::
::: C++ C++
TRTCTranscodingConfig config;
// Set the resolution to 720 x 1280 px, bitrate to 1500 Kbps, and frame rate to 20 FPS
config.videoWidth      = 1280;
config.videoHeight     = 720;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;

// Use the preset layout mode
config.mode == TRTCTranscodingConfigMode_Template_PresetLayout
TRTCMixUser* mixUsersArray = new TRTCMixUser[3];
mixUsersArray[0].userId      = "$PLACE_HOLDER_LOCAL_MAIN$";
mixUsersArray[0].zOrder      = 0; // When `zOrder` is set to `0`, it indicates that the anchor's image is displayed at the bottom.
mixUsersArray[0].rect.left   = 0;
mixUsersArray[0].rect.top    = 0;    
mixUsersArray[0].rect.right  = videoWidth;
mixUsersArray[0].rect.bottom = videoHeight;
mixUsersArray[0].roomId      = nullptr; // Required for remote users but not for the local user

mixUsersArray[1].userId      = "$PLACE_HOLDER_REMOTE$";
mixUsersArray[1].zOrder      = 1;
mixUsersArray[1].rect.left   = 400; // For reference only
mixUsersArray[1].rect.top    = 800; // For reference only
mixUsersArray[1].rect.right  = 180; // For reference only
mixUsersArray[1].rect.bottom = 240; // For reference only
mixUsersArray[1].roomId      = 97392; // Required for remote users but not for the local user

mixUsersArray[2].userId      = "$PLACE_HOLDER_REMOTE$";
mixUsersArray[2].zOrder      = 1;
mixUsersArray[2].rect.left   = 400; // For reference only
mixUsersArray[2].rect.top    = 500; // For reference only   
mixUsersArray[2].rect.right  = 180; // For reference only
mixUsersArray[2].rect.bottom = 240; // For reference only
mixUsersArray[2].roomId      = 97393; // Required for remote users but not for the local user
config.mixUsersArray = mixUsersArray;

// Enable On-Cloud MixTranscoding
trtc->setMixTranscodingConfig(&config);
:::
::: C# C#
TRTCTranscodingConfig config = new TRTCTranscodingConfig();
// Set the resolution to 720 x 1280 px, bitrate to 1500 Kbps, and frame rate to 20 FPS
config.videoWidth      = 1280;
config.videoHeight     = 720;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
config.mode = RTCTranscodingConfigMode.TRTCTranscodingConfigMode_Template_PresetLayout;
TRTCMixUser[] mixUsersArray = new TRTCMixUser[3];

// Position of the camera image of the anchor
TRTCMixUser local = new TRTCMixUser();
local.userId = "$PLACE_HOLDER_LOCAL_MAIN$";
local.zOrder = 0; // When `zOrder` is set to `0`, it indicates that the anchor's image is displayed at the bottom.
local.roomId = null; // Required for remote users but not for the local user
RECT rtLocal = new RECT() {
    left   = 0, 
    top    = 0,
    right  = videoWidth,
    bottom = videoHeight
};
local.rect = rtLocal;
mixUsersArray[0] = local;

// Image position of co-anchor
TRTCMixUser remote1 = new TRTCMixUser();
remote1.userId = "$PLACE_HOLDER_REMOTE$";
remote1.zOrder = 1;
remote1.roomID = 97392; // Required for remote users but not for the local user
RECT rtRemote1 = new RECT() { // For reference only
    left   = 420,
    top    = 81,
    right  = 240 + left,
    bottom = 240 + top
};
remote1.rect = rtRemote1;
mixUsersArray[1] = remote1;

// Image position of co-anchor
TRTCMixUser remote2 = new TRTCMixUser();
remote2.userId = "$PLACE_HOLDER_REMOTE$";
remote2.zOrder = 1;
remote2.roomId = 97393; // Required for remote users but not for the local user
RECT rtRemote2 = new RECT() { // For reference only
    left   = 660,
    top    = 400,
    right  = 240 + left,
    bottom = 240 + top
};
rtRemote2.rect   = rtRemote2;
mixUsersArray[2] = remote2;

// Enable On-Cloud MixTranscoding
config.mixUsersArray = mixUsersArray;
trtc.setMixTranscodingConfig(config);
:::
::: Flutter java
TRTCCloud trtcCloud = await TRTCCloud.sharedInstance();
trtcCloud.setMixTranscodingConfig(TRTCTranscodingConfig(
  appId: 1252463788, // For reference only
  bizId: 3891, // For reference only
  // Set the resolution to 720 x 1280 px, bitrate to 1500 Kbps, and frame rate to 20 FPS
  videoWidth: 720,
  videoHeight: 1280,
  videoBitrate: 1500,
  videoFramerate: 20,
  videoGOP: 2,
  audioSampleRate: 48000,
  audioBitrate: 64,
  audioChannels: 2,

  // Use the preset layout mode
  mode: TRTCCloudDef.TRTC_TranscodingConfigMode_Template_PresetLayout,

  mixUsers: [
  // Position of the camera image of the anchor
    TRTCMixUser(
      userId: "$PLACE_HOLDER_LOCAL_MAIN$",
      roomId: null, // Required for remote users but not for the local user
      zOrder: 0, // When `zOrder` is set to `0`, it indicates that the anchor's image is displayed at the bottom
      x: 0, // For reference only
      y: 0,
      streamType: 0,
      width: 300,
      height: 400),
    TRTCMixUser(
      userId: '$PLACE_HOLDER_REMOTE$',
      roomId: '256', // Required for remote users but not for the local user
      zOrder: 1,
      x: 100, // For reference only
      y: 100,
      streamType: 0,
      width: 160,
      height: 200)
  ],
));
:::
::: Web JavaScript
try {
  // Present layout mode
  const config = {
   mode: 'preset-layout',
   videoWidth: 720,
   videoHeight: 1280,
   videoBitrate: 1500,
   videoFramerate: 20,
   videoGOP: 2,
   audioSampleRate: 48000,
   audioBitrate: 64,
   audioChannels: 2,
   // Preset the positions of the local camera stream and two remote streams.
   mixUsers: [
      {
        width: 720,
        height: 1280,
        locationX: 0,
        locationY: 0,
        pureAudio: false,
        userId: 'jack', // Placeholder for the local camera stream. Pass in the `userId` of the user whose camera stream is pushed.
        zOrder: 1
      },
      {
        width: 180,
        height: 240,
        locationX: 400,
        locationY: 800,
        pureAudio: false,
        userId: '$PLACE_HOLDER_REMOTE$', // Placeholder for a remote image
        zOrder: 2
      },
      {
        width: 180,
        height: 240,
        locationX: 400,
        locationY: 500,
        pureAudio: false,
        userId: '$PLACE_HOLDER_REMOTE$', // Placeholder for a remote image
        zOrder: 2
      }
    ];
  }
  await client.startMixTranscode(config);
} catch (error) {
  console.error('startMixTranscode failed ', error);
}
:::
</dx-codeblock>  

>! 
>- In the preset layout mode, you only need to call the `setMixTranscodingConfig()` API once after entering a room and enabling local audio publishing.
- The naming of the API for web is slightly different from that for other platforms. For details, please see [Client.startMixTranscode()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode).

[](id:ScreenSharing)
### Screen sharing mode (`ScreenSharing`)
#### Use cases
The screen sharing mode is suitable for scenarios such as online classes and interactive classrooms. You can select this mode by setting the `AppScene` parameter to `TRTCAppSceneLIVE` when calling the [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) API of the SDK.
In the screen sharing mode, the SDK prepares a canvas in the specified resolution. When the teacher is not sharing his or her screen, the SDK stretches the teacher’s camera image to fit the canvas. After the teacher enables screen sharing, the SDK does the same to the screen sharing image. This ensures consistency in the resolution of mixed streams and avoids incompatibility issues caused by inconsistencies in the resolution of recorded and played back videos (average players cannot play videos with changing resolution.)

#### Directions
1. When calling the `enterRoom()` function to enter a room, set the `AppScene` parameter to `TRTCAppSceneLIVE`.
2. Enable [relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and specify the `streamId` parameter in `TRTCParams` for mixed streams.
3. Call `startLocalPreview()` and `startLocalAudio()` to enable local audio and video publishing.
>? On-Cloud MixTranscoding mixes multiple streams into the stream of the current user, i.e., the user who sends the stream mixing command. Therefore, stream mixing works only if the current user is sending audio.
4. Call the `setMixTranscodingConfig()` API to enable On-Cloud MixTranscoding. You need to set the `mode` parameter in `TRTCTranscodingConfig` to **TRTCTranscodingConfigMode_Template_ScreenSharing**, and specify audio quality-related parameters such as `audioSampleRate`, `audioBitrate`, and `audioChannels`, as well as video quality-related parameters such as `videoWidth`, `videoHeight`, `videoBitrate`, and `videoFramerate`.
>? If both `videoWidth` and `videoHeight` are set to `0`, the SDK will work out an appropriate resolution based on the aspect ratio of the user's screen.
5. After the above steps are performed, the audio of other users in the room will be automatically mixed into the relayed audio stream of the current user. You can then follow the instructions in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242) to configure a playback domain name for relayed live streaming or record the mixed audio stream as described in [On-Cloud Recording](https://intl.cloud.tencent.com/document/product/647/35426).

![](https://main.qcloudimg.com/raw/675e67bfaff40451b60a21aa403217d4.gif)
>! 
>- The screen sharing mode is supported on Windows and macOS only.
>- In the screen sharing mode, you only need to call the `setMixTranscodingConfig()` API once after entering a room and enabling local audio publishing.
>- The teacher’s screen constitutes the main part of an online class. Publishing the teacher’s camera data at the same time would drive up bandwidth usage. Given this, you are advised to use `setLocalVideoRenderCallback()` and `setRemoteVideoRenderCallback()` to display the teacher’s camera image and students’ images on the shared screen.
>- You can have the SDK select an output resolution automatically by setting both `videoWidth` and `videoHeight` in `TRTCTranscodingConfig` to `0`. If the teacher's screen width is smaller than 1920 px, the SDK will use the actual resolution of the teacher's screen; otherwise it will select a resolution from 1920 x 1080 px (16:9), 1920 x 1200 px (16:10), and 1920 x 1440 px (4:3), depending on the aspect ratio of the teacher’s screen.

[](id:Manual)

### Manual mode (`Manual`)
#### Use cases
You can use the manual mode for scenarios whose stream mixing requirements none of the above modes meets. The manual mode has the highest flexibility (you can customize all kinds of stream mixing modes) but the lowest usability.
In the manual mode, you must set all the parameters in `TRTCTranscodingConfig` and listen for the `onUserVideoAvailable()` and `onUserAudioAvailable()` callbacks in `TRTCCloudDelegate`. The callbacks keep you up to date about the users who are sending audio and video in the room so that you can modify the `mixUsers` parameter accordingly. Otherwise stream mixing will fail.

#### Directions
1. When calling the `enterRoom()` function to enter a room, set the `AppScene` parameter based on your needs.
2. Enable [relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242) and specify the `streamId` parameter in `TRTCParams` for mixed streams.
3. Call `startLocalAudio()` to enable local audio publishing. You may also call `startLocalPreview()` to enable video publishing.
>? On-Cloud MixTranscoding mixes multiple streams into the stream of the current user, i.e., the user who sends the stream mixing command. Therefore, stream mixing works only if the current user is sending audio and video.
4. Call the `setMixTranscodingConfig()` API to enable On-Cloud MixTranscoding. You need to set the `mode` parameter in `TRTCTranscodingConfig` to **TRTCTranscodingConfigMode_Manual**, and specify audio quality-related parameters such as `audioSampleRate`, `audioBitrate`, and `audioChannels`. If your applications also involve the transfer of video data, you also need to set video quality-related parameters such as `videoWidth`, `videoHeight`, `videoBitrate`, and `videoFramerate`.
5. Listen for the `onUserVideoAvailable()` and `onUserAudioAvailable()` callbacks in `TRTCCloudDelegate` and set the **mixUsers** parameter as needed.
 >?Unlike the preset layout mode, in the manual mode, you must set each `userId` in `mixUser` to the actual user ID of each co-anchor and set the `pureAudio` parameter in `mixUser` based on whether a co-anchor has enabled video.
6. After the above steps are performed, the audio of other users in the room will be automatically mixed into the relayed audio stream of the current user. You can then follow the instructions in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242) to configure a playback domain name for relayed live streaming or record the mixed audio stream as described in [On-Cloud Recording](https://intl.cloud.tencent.com/document/product/647/35426).
> In the manual mode, you need to listen for the mic on/off events of co-anchors in the room and call the `setMixTranscodingConfig()` API multiple times depending on the number of co-anchors and whether they are sending audio and video.

## Billing

### Cost calculation

During On-Cloud MixTranscoding, the MCU cluster decodes and re-encodes the audio and video streams sent to it. As a result, TRTC charges an additional fee from clients who use the MCU cluster for On-Cloud MixTranscoding. The fee varies with the **resolution of transcoded streams** and **transcoded duration**. The higher the resolution and the longer the duration, the higher the cost. For details, see [On-Cloud MixTranscoding Billing](https://intl.cloud.tencent.com/document/product/647/38929).

### Cost control

- **If you use server-side RESTful APIs, stream mixing stops when either of the following conditions is met.
  - All users, including anchors and audience, have left the room.
  - You have called [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760) to manually stop stream mixing.
- **If you use client-side APIs of the TRTC SDK, stream mixing stops when either of the following conditions is met.
  - The anchor who started stream mixing. i.e., the user who called the client-side API `setMixTranscodingConfig`, has left the room.
  - You have called [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) and set the parameter to `nil`/`null` to manually stop stream mixing.

In all other cases, TRTC will continue to mix streams in the cloud. Therefore, to reduce costs, you are advised to stop stream mixing using one of the above methods when you no longer need it.



