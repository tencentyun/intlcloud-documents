## TXLivePlayer

### Video player

For more information, see [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html).
 
TXLivePlayer decodes the audio and video data in live streams and performs local rendering. It provides the following capabilities:

- For Tencent Cloud's playback addresses, use low-delay playback to implement live streaming mic connect.
- For Tencent Cloud's playback addresses, use live streaming time shifting to implement seamless switching between live viewing and time-shifting viewing.
- Custom audio and video data processing allows you to process the audio and video data in live streams based on project requirements and then render and playback them.

### Basic SDK APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) | Creates a [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) instance. |
| [setConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#aec057eaad309a040e689eae94d81f6c2) | Sets [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) playback configuration items. |
| [setPlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a0735b006fe8c56875665cb66881af144) | Sets the stream push callback.                                           |


### Basic playback APIs  

| API                                                          | Description                            |
| ------------------------------------------------------------ | ------------------------------- |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a64eefab5bdb76cef17f609560eec5830) | Sets the player's rendering view.     |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a966517cd67d967afe969b3d275239934) | Starts playback.            |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a6abf34bf566c275476b1706593cb0fe1) | Stops playback.                      |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#ac651fc45a9f04e4db6f258f8cdd7bbcf) | Gets whether playback is ongoing.                  |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a7167f5c196fc5e167bfabde1a730e81d) | Pauses playback.                      |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a41de8150eff044a237990c271d57ea27) | Resumes playback.                      |
| [setSurface](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#ac06d94f1ed4ec1441c075e4ba556eb37) | Uses the surface mode for local rendering. |
| [setSurfaceSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#adfa92e76bde9450b135c48f531e5434d) | Sets the rendering surface size.       |


### Playback configuration APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | ---------------------- |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a6e1e1e12120b92f4884d3ea1a8e2cc94) | Sets the playback rendering mode.     |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | Sets the image rendering angle.     |
| [enableHardwareDecode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a33b092e7e79aab66b494e7034021b2f9) | Enables hardware acceleration.         |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a85d2bb3409165c1b7b2c53f8d61a03e2) | Sets whether to mute the player.     |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a3f0305de6ccd826ab62c442408416df9) | Sets the audio playback mode.     |
| [setVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a6715d5315d47c73b3838f2cb771e7b58) | Sets the volume level.             |
| [switchStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a53f1f75a9a06e03bbb35e2ff5368c6f9) | Switches between definitions.         |
| [setAudioVolumeEvaluationListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#acd5e085b916732b2141ddae9ef93fc21) | Sets the volume level callback. |


### Local recording and screenshot APIs

| API                                                          | Description                 |
| ------------------------------------------------------------ | -------------------- |
| [setVideoRecordListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#acd229e0c77d3eea61dc0762557417478) | Sets the recording callback.   |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#aed6b1e9d26a36166ee31c0544bd95ca4) | Starts video recording.       |
| [stopRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a13313c5410c2a10a704b991f28141e6e) | Stops video recording.       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a1377ad3e2678d3fef21f5037e274dd1a) | Takes a screenshot locally during playback. |


### Custom data processing APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------------- |
| [addVideoRawData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a31d3d4067f5e61b80d7b750a6b5d97e2) | Sets the software decoding data carrier buffer. |
| [setVideoRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a093d4928d038dcc1c5413e771b5f8962) | Sets the software decoding video data callback.    |
| [setAudioRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a36183b7ad026bc3e9718e82e38497e96) | Sets the audio data callback.          |


### Live streaming time shifting APIs

| API | Description |
| ------------------------------------------------------------ | -------------- |
| [prepareLiveSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a081d01beb281348300bd9e9689949c59) | Prepares for live streaming time shifting. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a914c54a0122cba5ad78d84f893df8578) | Seeks to the live stream playback time. |
| [resumeLive](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a4fa26fd4aea472d02de56d5f0bf653bf) | Resumes live streaming. |


### Screenshot callback APIs

For more information, see [ITXSnapshotListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXSnapshotListener).

| API | Description |
| ------------------------------------------------------------ | ---------- |
| [onSnapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) | A screenshot taken. |


### Video data callback APIs for software decoding

For more information, see [ITXVideoRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXVideoRawDataListener).

| API                                                          | Description |
| ------------------------------------------------------------ | ------------------------------ |
| [onVideoRawDataAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a466e71718261727174795a3cd2b95d9e/34775#onvideorawdataavailable) | A frame decoded by the software decoder. |


### Raw audio data callback APIs

For more information, see [ITXAudioRawDataListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXAudioRawDataListener).

| API                                                          | Description                               |
| ------------------------------------------------------------ | ---------------------------------- |
| [onPcmDataAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a33e835ad16580a93ae40e0723368af32) | Audio playback data in PCM format. |
| [onAudioInfoChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#a2aa86c3f5bd33047692b3d4dd0a59c32) | Audio playback information.                 |


### Player volume callback APIs

For more information, see [ITXAudioVolumeEvaluationListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#interfacecom_1_1tencent_1_1rtmp_1_1TXLivePlayer_1_1ITXAudioVolumeEvaluationListener).

| API                                                          | Description                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [onAudioVolumeEvaluationNotify](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html#ae83090684b162568b729c010acd69828) | The player's volume level. Value range: 0–100. |

## TXLivePlayConfig

### TXLivePlayer parameter configuration module

For more information, see [TXLivePlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#classcom_1_1tencent_1_1rtmp_1_1TXLivePlayConfig).

It is used to set [TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayer__android.html) parameters, most of which cannot take effect if they are set after playback starts.

### Common APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------- |
| [setAutoAdjustCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#ad2b54e62edb8d9cf287ac34a0ee0bc6e) | Sets whether to automatically adjust the cache time.   |
| [setCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#ac911ed6c1650c8723d11bb4aaa49f73f) | Sets the player cache time.         |
| [setMaxAutoAdjustCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#ab400433f30e53d4827b8c16c449c107c) | Sets the maximum cache time.         |
| [setMinAutoAdjustCacheTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#af495df5fea5e42779c007c5600e7bc4a) | Sets the minimum cache time.         |
| [setVideoBlockThreshold](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a5d403dd5553d58ce309f26dbec61e20f) | Sets the video lagging alarm threshold for the player. |
| [setConnectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a30911117043dc5b3f559abf5eb1e9ce9) | Sets the maximum number of player reconnection attempts.         |
| [setConnectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a5f3b8315c6276bd1c03c999ce01e4f8f) | Sets the player reconnection interval.         |


### Dedicated APIs

| API | Description |
| ------------------------------------------------------------ | -------------- |
| [setEnableMessage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a7c8e9ce786b57f2fddf921c4f336523d) | Enables the message channel. |
| [enableAEC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXLivePlayConfig__android.html#a2fb8e9e6f182cdd49f1260484cc484e5) | Sets acoustic echo cancellation (AEC). |


## ITXLivePlayListener

### TXLivePlayer callback notifications

For more information, see [ITXLivePlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXLivePlayListener__android.html).

| API | Description |
| ------------------------------------------------------------ | -------------- |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXLivePlayListener__android.html#a57e1f63dbe15f1242e3b842d0454f74f) | Playback event notification. |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXLivePlayListener__android.html#a826de3acd9a9d2da1604a076772f2f2e) | Network status notification. |
