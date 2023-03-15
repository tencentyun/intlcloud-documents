## TXVodPlayer

### VOD player

See [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html).
The player pulls audio/video data from the specified VOD stream URL and plays the data after decoding and local rendering.
The player has the following capabilities:

- FLV, MP4, and HLS files can be played back in two playback methods: basic playback (by URL) and VOD playback (by `Fileid `).
- Screenshots of the video stream can be taken.
- The brightness, volume level, and playback progress can be adjusted through gestures.
- Resolution can be switched manually or resolution can be automatically switched to adapt to the current network bandwidth.
- Different playback speeds can be specified, videos can be flipped horizontally, and hardware acceleration can be enabled.
- For more information about all capabilities of the player, see [Overview](https://intl.cloud.tencent.com/document/product/266/38295).

### Player configuration APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [config](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a3ad68ed80140f20cf3229bf344886a04) | Configures VOD. For more information on the configuration, see [TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html). |
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | Sets whether to start playback immediately after call of `startPlay`. Default value: YES.                         |
| [token](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | Sets the token for HLS encryption. After the token is set, the player will automatically add `voddrm.token.TOKEN TextureView` before the filename in the URL.  |
| [loop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1cdc15a39387295573f41caee9a05932) | Sets whether to loop `SurfaceView`.                                   |
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) | Sets whether to enable hardware acceleration.                                 |
| [setExtentOptionInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a842c8863f91f274031be0109a5cb28f5) | Sets the player business parameters in the format of `<NSString *, id>`.             |

### Basic playback APIs  
| API                                                                                                            | Description                                                                                                                                                                                     |
| ------------------------------------------------------------ | ---------------------------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ac1af59fe9e4bc2b390661787097d2c8b) | Starts playing back the video at the specified HTTP URL. |
| [startPlayDrm:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aaa492de602b58d75b0489435b20be811) | Starts playing back a file encrypted with standard FairPlay DRM. |
| [startPlayWithParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a0b4db90eafbc8c4d9be498e5ffefe961) | Starts playing back the video of the specified `fileId`.    |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | Stops playback.                      |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a8438e3403946accc1986a05b89ee7b03) | Gets whether playback is ongoing.                  |
| [pause](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | Pauses playback by stopping the retrieval of stream data and retaining the last-frame image. |
| [resume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a41de8150eff044a237990c271d57ea27) | Resumes playback by getting the stream data again. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | Seeks to the video stream to the specified time point in s. |
| [currentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a8b0ca7fda398996b355179bd9a479785) | Gets the current playback time point in seconds. |
| [duration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7fd4f66e650bd1656a97d1db7fabaeda) | Gets the total video duration in seconds. |
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a4acb1f7a723d342f7bfb9c5e540e5e77) | Gets the playable video duration in seconds. |
| [width](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a3eeed61a3424d2f907c8a1e420fddf6d) | Gets the video width. |
| [height](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a822ae85493a742654ba563619492b26a) | Gets the video height. |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a41001e6276c4853500f78579d6bd2218) | Sets the playback start time. |
| [setupVideoWidget:insertIndex:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a370c35a44549bad3a162741c288b8eb8) | Creates the video rendering view. This control is used to display the video content. |
| [removeVideoWidget](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#adf77d29895e70602556fdc51b931951e) | Removes the video rendering view.                           |

### Video APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a9646437dc38d7dcce8c32dfec5d0bc5b) | Gets the current video frame image.<br>**Note: As this operation is time-consuming, the screenshot will be called back asynchronously.** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aaf347826e1a9fad9998c0eea9791ed0c) | Sets whether to flip the video image horizontally.                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | Sets the VOD playback speed. Default value: 1.0.                                |
| [bitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a9a325ed94acf6b545c88755855449a12) | Returns the current playback bitrate index.                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1aa8e1f3a63b46c8a1166447e2457abc) | Sets the current playback bitrate index for seamless definition switch. <br>You may need to wait momentarily to switch the definition. |
| [supportedBitrates](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a1c7f996e3c1e5ec04fe3f3b184491495) | Returns the supported bitrates (definitions) if the playback address is a master playlist.     |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | Sets the [image fill mode](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae). |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | Sets the [image rendering angle](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f). |
| [enterPictureInPicture](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ae0118065e4d29cb7dbab4ccd0ba6b3e5) | Enters the PiP mode. |
| [exitPictureInPicture](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a5f0bc0ade6e99f31392f6f8d897ae84c) | Exits the PiP mode.                                             |

### Audio APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ----------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | Sets whether to mute the player.     |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#ac92633d1cdfff1f93f48b7aec1d35b98) | Sets the volume level. Value range: 0–100.           |

### Event notification APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | The event callback. We recommend you use [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79). |
| [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) | Sets the player callback.                                       |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | Sets the video rendering callback (supported by hardware encoding only).                                 |

### TRTC APIs

You can use the following APIs to push the audio/video streams of the VOD player through TRTC. For more information on TRTC services, see the TRTC [Overview](https://cloud.tencent.com/document/product/647/16788) page.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#affcfcba7937a7ef88a918afb0b3d73bc) | Binds VOD to [TRTC](https://cloud.tencent.com/document/product/647/16788). |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a5b947acf9f4fc992f0f02f8d87de3334) | Unbinds VOD from [TRTC](https://cloud.tencent.com/document/product/647/16788). |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a8298f704cb659c725da28a27e08afbed) | Starts pushing the video stream.                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#aaa6ecf72bfa9e35078561dd98d62be0c) | Cancels pushing the video stream.                                             |
| [publishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | Starts pushing the audio stream.                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a206d786a74ae3b71766755135161773e) | Cancels pushing the audio stream.                                             |

### Class methods

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------- |
| [getEncryptedPlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#acdb2823140afb92657f840b7b765636d) | Gets the encrypted playback key.                            |
| [isSupportPictureInPicture](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a2b0eae752e8cd548572e747a85602c71) | Queries whether the current device supports the picture-in-picture (PiP) feature. |

## TXVodPlayListener

VOD callback notifications.
### Basic SDK callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent:event:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#a6330db18bb40862fc2d66474fc34166b) | VOD playback event notification. For more information, see the [playback event list](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a) and [event parameters](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594). |
| [onNetStatus:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#a08721fef1ba130fd182de4bed3b4430e) | VOD player [network status notification](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737). |
| [onPlayer:pictureInPictureStateDidChange:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#ac0e5e698f62a9d8a58b0e8e63fc8afb1) | The callback for PiP status.                                             |
| [onPlayer:pictureInPictureErrorDidOccur:withParam:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayListener__ios.html#a4dcee189760af5752bd112a725994d0b) | The callback for PiP error status.                                             |

## TXVodPlayConfig

VOD player configuration class.

### Basic configuration APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [connectRetryCount](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ad89d728973fb42eced3ac18be873af1b) | Sets the maximum number of player reconnection attempts.         |
| [connectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a07fde7cd21980c096b5bbd93aed137d5) | Sets the player reconnection interval in seconds.                                 |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a39233eb85b4cbae04411577510e7c5e6) | Sets the player connection timeout period in seconds.                             |
| [cacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aec1a8f0064562368fe3c2df4f7fb72eb) | Sets the VOD cache directory, which takes effect for MP4 and HLS files. <br>This API has been deprecated. We recommend you use [TXPlayerGlobalSetting##setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html). |
| [maxCacheItems](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aedbc9cc868baa2c44e3badbe6fdf4a43) | Sets the maximum number of cached files. <br>This API has been deprecated. We recommend you use [TXPlayerGlobalSetting#setMaxCacheSizeMB](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html). |
| [playerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a4595fb5853016c5e5919324e71ad6f4c) | Sets the player type.                                             |
| [headers](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ad69aaf8885027863ea19657425ef1974) | Sets custom HTTP headers.                                    |
| [enableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ada91e71bad4df942e6190650915a7728) | Sets whether to enable accurate seek. Default value: true.                               |
| [autoRotate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aa1a372684aaaf95b9b17abf0c7a4e6c6) | If it is set to `YES`, the MP4 file will be automatically rotated according to the rotation angle set in the file, which can be obtained from the `PLAY_EVT_CHANGE_ROTATION` event. Default value: YES |
| [smoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aa1caeddde1f950ec7965dcc721109928) | Sets whether to enable smooth switch for multi-bitrate HLS streams. Default value: false.                             |
| [progressInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a943e212cbd5e3d89de0529ab7c6042fb) | Sets the progress callback interval in ms.                                 |
| [maxBufferSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#aa4934cef81784d3a195a5d95a43953f5) | Sets the maximum preloading buffer size in MB.                                    |
| [maxPreloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a3ae31483070f62cf35abd9003ccce0e0) | Sets the maximum preloading buffer size in MB.                         |
| [firstStartPlayBufferTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a5a6373341623385672a12e9e3617c1c2) | Sets the duration (in ms) of the video data that needs to be loaded during the first buffering. Default value: 100 ms. |
| [nextStartPlayBufferTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ab17865763b40e7d86913dd2c6fb3110f) | The minimum buffered data size to stop buffering (secondary buffering for insufficient buffered data or progress bar drag buffering caused by `seek`) in ms. Default value: 250 ms. |
| [overlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#adc41276c8fa265cb622657b581ba3f3b) | Sets the HLS security hardening encryption and decryption key.                                   |
| [overlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a3de0b922b54d46f11a8e203026d44fed) | Sets the HLS security hardening encryption and decryption IV.                                    |
| [extInfoMap](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a55b7d33d270ac9004aad798bd6027879) | Sets the extended information.                                               |
| [preferredResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#afcfb593028655bbac25a753f8ffe9904) | Starts playing back the most preferred bitstream according to the configured `preferredResolution` if there are multiple HLS bitstreams. Here, `preferredResolution` is the product of the video width and height (width x height) and can only take effect if it is set before playback starts. |
| [enableRenderProcess](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a3b7f6694446ab09764315f003192fc5a) | Sets whether to allow postrendering and postproduction features such as super resolution plugin, which is enabled by default.     |
| [playerPixelFormatType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ac1ae36ec22cc49f49ceb7842cb86be3b) | The video format called back by the video rendering object.                               |
| [keepLastFrameWhenStop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#ace241f4953a14aac301ecd1e196de3f8) | Whether to retain the last image frame when `stopPlay` is called. Default value: NO.           |
| [mediaType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__ios.html#a5877610faab7f5148bc34072a0c92a5b) | Sets the media asset type.                                               |
|                                                              |                                                              |

## TXPlayerGlobalSetting

Global configuration of the VOD player.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__ios.html#a604b66ab880e7a5d056ce5c3132ddf48) | Sets the cache directory of the playback engine. After setting, this directory will be first read and written during predownloading and player use. |
| [setMaxCacheSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__ios.html#ad511345d985ae9bc271a1e867c3f71f0) | Sets the maximum cache size in MB of the playback engine. After setting, the backend will clear files in the cache directory automatically according to the set value. |

## TXVodPreloadManager

Predownloading API class of the VOD player.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#a84882e4d61f22f51a18d3b639d881138) | Gets the `TXVodPreloadManager` instance object in singleton mode.                    |
| [startPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#af67a02c9fba5c07f83b2d36d24b764fd) | Sets the playback engine cache directory (`TXPlayerGlobalSetting#setCacheFolderPath`) and cache size (`TXPlayerGlobalSetting#setMaxCacheSize`) before starting predownloading. |
| [stopPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#a5c29884349c8f6436eff8f70f302d33e) | Stops predownloading.                                                   |

### Callback for video predownloading

| API | Description |
| ------------------------------------------------------------ | -------------- |
| [onComplete:url:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#aa887ac7b6bcf155eb22816f880eed270) | The callback for download completion. |
| [onError:url:error:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__ios.html#a07e337f1e638e458a3e761507deec525) | The callback for download error. |

## TXVodDownloadManager

Video download API class of the VOD player.

### TXVodDownloadDataSource

| API                                                          | Description                     |
| ------------------------------------------------------------ | ------------------------- |
| [auth](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a59eb64ffe11d0bdee5c67009f5ebdd8c) | The `fileid` information.                |
| [quality](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ab674303410c354ab3d0d6957b86dcf14) | The download definition, which is the original resolution by default.      |
| [token](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a2f0d5a61a262b1362f51c943b6a03f17) | Enter the token if the address is encrypted. |
| [templateName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a0c960f307400330cb261513cde7c2906) | The definition template.                |
| [fileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a66c446aeaf5eef1ee21764d4bdf7b8ae) | The file ID.                    |
| [pSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a0411129c1f5cf0bdfac7baabeb12c7a2) | The signature information.                  |
| [appId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a5b3217c0ab223c526d557b09d2b0d6c0) | The application's `appId`, which is required.         |
| [userName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac38202c6f4861ad216f9fbc5d962b5ab) | The account name.                  |
| [overlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#adc41276c8fa265cb622657b581ba3f3b) | The `HLS EXT-X-KEY` encryption/decryption parameter.  |
| [overlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a3de0b922b54d46f11a8e203026d44fed) | The `overlayIv` encryption/decryption parameter.     |

### TXVodDownloadMediaInfo

| API                                                          | Description                            |
| ------------------------------------------------------------ | ------------------------------- |
| [isDownloadFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#aca53b9773ade9052bc8ff2592bea0c01) | Whether download is completed.                    |
| [dataSource](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a74a85fcd734fe688c3a65083dc815a6a) | The download object specified by`fileid`, which is optional.          |
| [url](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a43481294fa1d2f0ebe7cff14b17726cc) | The download address.                        |
| [userName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac38202c6f4861ad216f9fbc5d962b5ab) | The account name.                  |
| [duration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac6e4b2a3cf932b33832d4e4e4e7cd0de) | The duration.                            |
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a1945ed3669e000f80e294331d6c302b4) | The playable duration.                      |
| [size](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a439227feff9d7f55384e8780cfc2eb82) | The total file size in bytes.          |
| [downloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a15989d553be239ea233f9957236fa767) | The size of the downloaded part in bytes.         |
| [segments](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a32e4172d8952ac9f1db668982da57128) | The total number of segments.                        |
| [downloadSegments](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac2e85e36301b166ed1bb92844f6f5399) | The number of downloaded segments.                 |
| [progress](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac7abb4766cd3f65c31f56279d7decff8) | The progress.                            |
| [playPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a6567e969a0aa9ef88a4a2ff601ea8527) | The playback path, which can be passed in to `TXVodPlayer` for playback. |
| [speed](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a218b4f7c6cc2681a99c23a3b089d68b1) | The download speed in B/s.             |
| [downloadState](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ae87c7de3c7e2888cfe6298bc25c4f9be) | The download status.                        |

### TXVodDownloadManager

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [shareInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a8a1039302b46bec56fcc15c2ffdcbf16) | Gets the `TXVodDownloadManager` instance object in singleton mode.                   |
| [setDownloadPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a5ca035da8c8f8771f08fe15c6857a304) | Sets the download root directory.                                               |
| [headers](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ad69aaf8885027863ea19657425ef1974) | Sets download HTTP headers.                                               |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a507e1dcc250a5764bd84d6e8a6598b23) | Sets the download callback method, which must be set before download.                             |
| [startDownloadUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ac886a33c24af3bea16b4b2b9ab1bcfde) | Starts downloading the video at the specified URL.                                          |
| [startDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a6093eec0836566ad15a4fdeb2b0682e9) | Starts downloading the video of the specified `FileID`.                                        |
| [stopDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#af1c09ed1089c935a46d6f9d8f1587dc4) | Stops the download. If `ITXVodDownloadListener.onDownloadStop` is called back, the download stops successfully. |
| [deleteDownloadFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a9564ad5e676445ffe2cccdbfacfd7b11) | Deletes the downloaded file.                                                 |
| [deleteDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a8f38d437419ecbe1d906e5826893194e) | Deletes the download information.                                                 |
| [getDownloadMediaInfoList](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#adad0276021a21fdfca8b1925b8c46ca5) | Gets the download lists of all users.                                   |
| [getDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a255dd9b7ce63b862e0674ba144a68aac) | Gets the download information.                                   |
| [getOverlayKeyIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a4b0e452471aa28879bd855886127bcfd) | Gets the `HLS EXT-X-KEY`.                                          |
| [genRandomHexStringForHls](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a0c96770dd135d266dfc14779fedad775) | Gets a random number for encryption.                                            |
| [encryptHexStringHls:](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ab6277c0f8c42ee94a1a56055ead6ea13) | Encrypts.                                                       |

### TXVodDownloadDelegate

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------- |
| [onDownloadStart](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ad375a3205d19472a2e5f22fbce384f6a) | Download started.                                         |
| [onDownloadProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a7fcc9b089f4cabcd1b843fdccbd7f58b) | The download progress was updated.                                    |
| [onDownloadStop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a11ad404425936a29dd9f2edc1aaca8f6) | Download stopped.                                    |
| [onDownloadFinish](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a4453811b7217726930d8f05b62cc4902) | Download ended.                                         |
| [onDownloadError](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#adf5abf41239950b68347a085704db523) | An error occurred during download.                           |
| [hlsKeyVerify](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#a32e5b4e7d5eaa14a9b144747e174390f) | Verifies the decryption key by the player if an encrypted file is found during HLS stream download. |

### [TXDownloadError](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ga625ad66cfaed6a449961936a37740dd9)

The download error code

| Enumerated Value | Description |
| --------------------- | ------------------ |
| TXDownloadSuccess     | Download succeeded.           |
| TXDownloadAuthFaild   | Failed to authenticate the `fileid`.     |
| TXDownloadNoFile      | The file with the specified resolution does not exist.     |
| TXDownloadFormatError | The format is not supported.         |
| TXDownloadDisconnet   | The network was disconnected.           |
| TXDownloadHlsKeyError | Failed to get the HLS decryption key. |
| TXDownloadPathError   | Failed to access the download directory.   |

### [TXVodDownloadMediaInfoState](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ga7378c6cdd737126deb060ee3eb31f00a)

The download status

| Enumerated Value | Description |
| --------------------------------- | ---------- |
| TXVodDownloadMediaInfoStateInit   | Download was initialized. |
| TXVodDownloadMediaInfoStateStart  | Download started.   |
| TXVodDownloadMediaInfoStateStop   | Download stopped.   |
| TXVodDownloadMediaInfoStateError  | An error occurred during download.   |
| TXVodDownloadMediaInfoStateFinish | Download was completed.   |

### [TXVodQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__ios.html#ga7079416c4ef1fec0f33755d7a2bc7c58)

The definition of the downloaded video

| Enumerated Value | Description |
| --------------- | -------- |
| TXVodQualityOD  | Original     |
| TXVodQualityFLU | LD     |
| TXVodQualitySD  | SD     |
| TXVodQualityHD  | HD     |
| TXVodQualityFHD | FHD   |
| TXVodQuality2K  | 2K       |
| TXVodQuality4K  | 4K       |

## TXPlayerAuthParams

The configuration for encrypted video playback through `fileId`.

| API                                                          | Description                 |
| ------------------------------------------------------------ | -------------------- |
| [appId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a5b3217c0ab223c526d557b09d2b0d6c0) | The application's `appId`.         |
| [fileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a66c446aeaf5eef1ee21764d4bdf7b8ae) | The file ID.             |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a4f13e124e054004dcd7930ecd6df0f57) | The encrypted link timeout timestamp. |
| [exper](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a9e4e9de0c34814be700575f5ebdf725e) | The preview duration.           |
| [us](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a6a5fc78b476fcbcdcc2a9888faa75ea3) | The unique request ID.       |
| [sign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a37aa22c94233901cd1afee101f759348) | The hotlink protection signature.         |
| [https](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthParams__ios.html#a33d23e482c312a90cae72781bdfa1c4a) | Whether to use HTTPS requests.    |

## TXBitrateItem

The HLS multi-bitrate information.

| API | Description |
| ------------------------------------------------------------ | ------------------- |
| [index](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#a43d1d245fab4496928fe2e287fdc3f59) | The number of the stream in the m3u8 file. |
| [width](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#ab581e554cfc9559c9e2cd57ecf126d02) | The video width of this stream.    |
| [height](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#a1cdeaaebe1687fd7b3237fd45e3d5740) | The video height of this stream.    |
| [bitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__ios.html#abee909d3e29c2c87de16464920736759) | The video bitrate of this stream.    |

## TXImageSprite

The image sprite parsing tool.

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [setVTTUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__ios.html#a0075e38dc6b4291851c35f896ce7a28d) | Sets the image sprite URL. |
| [getThumbnail](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__ios.html#a4561e9ea43d7273caf9197d96f5f7307) | Gets a thumbnail.     |

## TXPlayerDrmBuilder

The VOD DRM constructor.

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [certificateUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__ios.html#a24e49ee9ffc468e63b10c120af3a842f) | The URL of the certificate provider. |
| [keyLicenseUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__ios.html#a1d393eafdb9cc90f7f6beeeb8eb94157) | The URL of the decryption key.   |
| [playUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__ios.html#ab08c768d03824654011cf36aedc16193) | The playback URL.       |

## Error Codes

### Normal events

| Code | Event Definition | Description |
| ---- | -------------------------- | ----------------------------------------------------------- |
| 2004 | PLAY_EVT_PLAY_BEGIN        | Video playback started, and the loading icon animation (if any) ended.                |
| 2005 | PLAY_EVT_PLAY_PROGRESS     | Video playback progress (including the current playback progress, loading progress, and total video duration).      |
| 2007 | PLAY_EVT_PLAY_LOADING      | The video is being loaded. The `LOADING_END` event will be reported if video playback resumes. |
| 2014 | PLAY_EVT_VOD_LOADING_END   | Video loading ended, and video playback resumed.                        |
| 2006 | PLAY_EVT_PLAY_END          | Video playback ended.                                           |
| 2013 | PLAY_EVT_VOD_PLAY_PREPARED | The player has been prepared and can start playback.                                |
| 2003 | PLAY_EVT_RCV_FIRST_I_FRAME | The network received the first renderable video data packet (IDR).  |
| 2009 | PLAY_EVT_CHANGE_RESOLUTION | The video resolution changed.                                            |
| 2011 | PLAY_EVT_CHANGE_ROTATION   | The MP4 video was rotated.                                          |



### Warnings

| Code | Event Definition | Description |
| ----- | --------------------------------- | ------------------------------------------------------------ |
| -2301 | PLAY_ERR_NET_DISCONNECT           | The network was disconnected and could not be reconnected after multiple retries. You can restart the player to perform more connection retries. |
| -2305 | PLAY_ERR_HLS_KEY                  | Failed to get the HLS decryption key.                                      |
| 2101  | PLAY_WARNING_VIDEO_DECODE_FAIL    | Failed to decode the current video frame.                                          |
| 2102  | PLAY_WARNING_AUDIO_DECODE_FAIL    | Failed to decode the current audio frame.                                         |
| 2103  | PLAY_WARNING_RECONNECT            | The network was disconnected, and automatic reconnection was performed (the `PLAY_ERR_NET_DISCONNECT` event will be thrown after three failed attempts). |
| 2106  | PLAY_WARNING_HW_ACCELERATION_FAIL | Failed to start the hardware decoder, and the software decoder was used instead.   |
| -2304 | PLAY_ERR_HEVC_DECODE_FAIL         | Failed to decode with H.265. |
| -2303 | PLAY_ERR_FILE_NOT_FOUND           | The file to be played back does not exist.                                           |

## Player SDK Constants

### [Definitions of event codes and error codes](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodSDKEventDef__ios.html#gabc22cbb50603d49430a22f2812d9e616)

| Enumerated Value | Description |
| ---------------------------------------- | ------------------------------------------------------------ |
| VOD_PLAY_EVT_RCV_FIRST_I_FRAME           | Playback event: Received the first video frame successfully.                             |
| VOD_PLAY_EVT_RCV_FIRST_AUDIO_FRAME       | Playback event: Received the first audio frame successfully.                             |
| VOD_PLAY_EVT_PLAY_BEGIN                  | Playback event: Playback started.                                       |
| VOD_PLAY_EVT_PLAY_PROGRESS               | Playback event: The playback progress was updated. This event is applicable to the VOD player only.          |
| VOD_PLAY_EVT_PLAY_END                    | Playback event: Playback ended.                                       |
| VOD_PLAY_EVT_PLAY_LOADING                | Playback event: The data is buffering.                                         |
| VOD_PLAY_EVT_START_VIDEO_DECODER         | Playback event: The video decoder started.                                 |
| VOD_PLAY_EVT_CHANGE_RESOLUTION           | Playback event: The video resolution changed.                                 |
| VOD_PLAY_EVT_GET_PLAYINFO_SUCC           | Playback event: Obtained the information of the VOD file successfully. This event is applicable to the VOD player only. |
| VOD_PLAY_EVT_CHANGE_ROTATION             | Playback event: The rotation angle of the MP4 video changed. This event is applicable to the VOD player only. |
| VOD_PLAY_EVT_VOD_PLAY_PREPARED           | Playback event: Video loading was completed. This event is applicable to the VOD player only.          |
| VOD_PLAY_EVT_VOD_LOADING_END             | Playback event: Video buffering ended. This event is applicable to the VOD player only.          |
| VOD_PLAY_EVT_STREAM_SWITCH_SUCC          | Playback event: Switched the video stream between different definitions successfully. |
| VOD_PLAY_EVT_VOD_PLAY_TCP_CONNECT_SUCC   | TCP connection succeeded.                                                 |
| VOD_PLAY_EVT_VOD_PLAY_FIRST_VIDEO_PACKET | Received the first data frame successfully.                                                 |
| VOD_PLAY_EVT_VOD_PLAY_SEEK_COMPLETE      | Video playback seeking was completed.                                           |
| VOD_PLAY_EVT_AUDIO_SESSION_INTERRUPT     | Playback event: The audio session was interrupted by another app. This event is applicable to iOS only. |
| VOD_PLAY_ERR_NET_DISCONNECT              | Live streaming error: The network was disconnected and couldn't be reconnected after three retries. |
| VOD_PLAY_ERR_FILE_NOT_FOUND              | VOD error: The file to be played back does not exist.                                     |
| VOD_PLAY_ERR_HLS_KEY                     | VOD error: Failed to get the HLS decryption key.                              |
| VOD_PLAY_ERR_GET_PLAYINFO_FAIL           | VOD error: Failed to get the information of the VOD file.                         |

### [PiP error type](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodSDKEventDef__ios.html#ga2b903483a07868f795ed52c27bfc08ac)

| Enumerated Value | Description |
| ------------------------------------------------ | -------------------------------------------- |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_NONE                | No error. |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_DEVICE_NOT_SUPPORT  | The device model or system version doesn't support PiP (only supported on iPadOS 9+ and iOS 14+). |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PLAYER_NOT_SUPPORT  | The player doesn't support PiP.                                 |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_VIDEO_NOT_SUPPORT   | The video doesn't support PiP.                                   |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PIP_IS_NOT_POSSIBLE | The PiP controller is unavailable.                             |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_ERROR_FROM_SYSTEM   | The PiP controller reported an error.                               |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PLAYER_NOT_EXIST    | The player object does not exist.                             |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PIP_IS_RUNNING      | The PIP feature is running.                             |
| TX_VOD_PLAYER_PIP_ERROR_TYPE_PIP_NOT_RUNNING     | The PIP feature has not been started.                             |

### [PiP controller status](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodSDKEventDef__ios.html#ga96479f1446227115f7183ae97a1527e3)

| Enumerated Value | Description |
| ---------------------------------- | -------------- |
| TX_VOD_PLAYER_PIP_STATE_UNDEFINED  | No status is set.    |
| TX_VOD_PLAYER_PIP_STATE_WILL_START | PiP will start soon. |
| TX_VOD_PLAYER_PIP_STATE_DID_START  | PiP started. |
| TX_VOD_PLAYER_PIP_STATE_WILL_STOP  | PiP will end soon. |
| TX_VOD_PLAYER_PIP_STATE_DID_STOP   | PiP ended. |
| TX_VOD_PLAYER_PIP_STATE_RESTORE_UI | The UI was reset.        |
