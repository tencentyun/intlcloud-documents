## TXLivePlayer
 
### Video player

For more information, see [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html).

TXLivePlayer decodes the audio and video data in live streams and performs local rendering. It provides the following capabilities:

- For Tencent Cloud's playback addresses, use low-delay playback to implement live streaming mic connect.
- For Tencent Cloud's playback addresses, use live streaming time shifting to implement seamless switching between live viewing and time-shifting viewing.
- Custom audio and video data processing allows you to process the audio and video data in live streams based on project requirements and then render and playback them.

### Basic SDK APIs 

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | Sets the playback callback. For more information, see the detailed definition in the `TXLivePlayListener.h` file.     |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | Sets the video processing callback. For more information, see the detailed definition in the `TXVideoCustomProcessDelegate.h` file. |
| [audioRawDataDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a4d08f185792a92a087aff32b52b6b7b9) | Sets the audio processing callback. For more information, see the detailed definition in the `TXAudioRawDataDelegate.h` file. |
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) |  Sets whether to enable hardware acceleration. Default value: NO.                               |
| [config](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aac73c062f0bbe5d97be40d85b68cb98a) | Sets [TXLivePlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aac73c062f0bbe5d97be40d85b68cb98a) playback configuration items. For more information, see the detailed definition in the `TXLivePlayConfig.h` file. |
| [recordDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7a3f4c66d5019d8e8899823e04be924d) | Sets the short video recording callback. For more information, see the detailed definition in the `TXLiveRecordListener.h` file. |
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a946828345d302a28708d78fa1a931763) | Sets whether to start playback immediately after call of `startPlay`. This API takes effect only for VOD. Default value: YES.           |


### Basic playback APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | -------------------------------------------------- |
| [setupVideoWidget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a9195fa66ee874328a5b48400f2a0cb14) | Creates the video rendering view. This control is used to display the video content. |
| [removeVideoWidget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#adf77d29895e70602556fdc51b931951e) | Removes the video rendering widget.                           |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a37e97416ec7a5853d217679be49cea26) | Plays back the RTMP audio/video stream at the specified URL.                |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | Stops the audio/video stream.                                 |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7d3378ad416bfd00522acaedefc47dda) | Gets whether playback is ongoing.                                     |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | Pauses playback.                                         |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a41de8150eff044a237990c271d57ea27) | Resumes playback. This API can be used for VOD and live streaming.                       |


### Video APIs

| API                                                          | Description                 |
| ------------------------------------------------------------ | -------------------- |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | Sets the orientation of the video image.     |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | Sets the image cropping mode. |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aa24051e4c0271d994a5008cfc2db4775) | Takes a screenshot.               |


### Audio APIs

| API                                                          | Description                                   |
| ------------------------------------------------------------ | -------------------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | Mutes/Unmutes the player.                             |
| [setVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a5a3bf801bad5591a3d8fe284aa6b3134) | Sets the volume level.                             |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#ad56c52832a8efe45d6e0c50049406d74) | Sets the audio playback mode (speaker or receiver). |
| [setAudioVolumeEvaluationListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a87d74a7afe3f768bd9e7ca276a189533) | Sets the volume level callback.                 |


### Live streaming time shifting APIs

| API                                                          | Description                                    |
| ------------------------------------------------------------ | ------------------------------------------ |
| [prepareLiveSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#acf638c46e1e866ef06abda5ac938f07f) | Prepares for live streaming time shifting and pulls the playback start time of the live stream. |
| [resumeLive](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a4fa26fd4aea472d02de56d5f0bf653bf) | Resumes live playback from time-shifting playback.                   |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | -                                          |


### Video recording APIs

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a7224d5a8ab5fadc1d4c0fe1feb6ac972) | Starts short video recording. |
| [stopRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a13313c5410c2a10a704b991f28141e6e) | Stops short video recording. |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | Sets the playback speed.   |


### Other APIs

| API                                                          | Description                                    |
| ------------------------------------------------------------ | ----------------------------------------- |
| [setLogViewMargin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#aa906f88b51df74ab8f3c1125d9856293) | Sets the margin between the rendering view and the status floating view.  |
| [showVideoDebugLog](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a70ec322b088ad3c38b5a41d7528467f2) | Sets whether to display the playback status statistics and event message floating view. |
| [switchStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a88751ad91dff45a9d6cc96dbda903b69) | Switches FLV live streams smoothly.                        |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#a16c53e91f9b32aaf4bf3d409a3790ef6) | Calls an experimental API.                     |


### Enumerated values

| Enumerated Value                                                         | Description                   |
| ------------------------------------------------------------ | ---------------------- |
| [TX_Enum_PlayType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html#gaa164f735d1c349ce715f313c5d75892a) | Supported live streaming and VOD types. |


## TXLivePlayConfig

### TXLivePlayer parameter configuration module

For more information, see [TXLivePlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__ios.html#interfaceTXLivePlayConfig).

It is used to set [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__ios.html) parameters, most of which cannot take effect if they are set after playback starts.

## TXLivePlayListener

### TXLivePlayer callback notifications

For more information, see [TXLivePlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayListener__ios.html).

| API | Description |
| ------------------------------------------------------------ | -------------- |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayListener__ios.html#a1e33d0cf9ed5f89ea2db32d0d7db9701) | Live streaming event notification. |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayListener__ios.html#aee80e62b7950c7d0a75ab97d993c10c6) | Network status notification. |

