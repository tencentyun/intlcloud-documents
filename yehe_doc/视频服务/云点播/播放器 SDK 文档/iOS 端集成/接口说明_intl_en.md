## TXVodPlayer

### VOD player

See [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html).
The player pulls audio/video data from the specified VOD stream URL and plays the data after decoding and local rendering.
The player has the following capabilities:

- Play FLV, MP4, and HLS files by URL (general playback) or by file ID (VOD playback).
- Take screenshots of the video stream.
- Adjust the brightness, volume level, and playback progress using gestures.
- Change the resolution manually or select a resolution automatically according to current network bandwidth.
- Change the playback speed, flip the video, and use hardware decoding for acceleration.
- For more information on the capabilities of the player, see [Video Playback Overview](https://intl.cloud.tencent.com/document/product/266/38295).

### Player configuration APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [config](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3ad68ed80140f20cf3229bf344886a04) | Configures VOD. For more information on the configuration, see [TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html). |
| [isAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | Sets whether to start playback automatically after `startVodPlay` is called. Auto-play is on by default.                         |
| [token](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a946828345d302a28708d78fa1a931763) | Sets the token for HLS encryption. After the token is set, the player will automatically add `voddrm.token.TOKEN TextureView` before the filename in the URL.  |
| [loop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1cdc15a39387295573f41caee9a05932) | Sets whether to loop `SurfaceView`.                                   |
| [enableHWAcceleration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aa3ea979a6be5feba0da24f2b18555395) | Sets whether to enable hardware acceleration.                                 |
| [setExtentOptionInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__ios.html#a842c8863f91f274031be0109a5cb28f5) | Sets the player business parameters in the format of `<NSString *, id>`.             |

### Basic playback APIs  
| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------------- |
| [startVodPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a89ac47a6b808c8ca424a65adb8870bc6) | Plays a video from an HTTP URL. Since v10.7, `startPlay` has been replaced by `startVodPlay`, and you need to call `V2TXLivePremier#setLicence` or `TXLiveBase#setLicence` to set the license in order to use the playback feature (you only need to set the license once). Otherwise, playback will fail (black screen). You can use a live stream publishing license, UGSV license, or video playback license to activate the playback feature. |
| [startVodPlayWithParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#acfae73abaadc60e2e1091ffae0c5c700) | Plays a video by VOD file ID. Since v10.7, `startPlayWithParams` has been replaced by `startVodPlayWithParams`, and you need to call `V2TXLivePremier#setLicence` or `TXLiveBase#setLicence` to set the license in order to use the playback feature (you only need to set the license once). Otherwise, playback will fail (black screen). You can use a live stream publishing license, UGSV license, or video playback license to activate the playback feature. |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7d59ca6180c4af0eb7bd63c08161f84d) | Stops the audio/video stream.                                 |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8438e3403946accc1986a05b89ee7b03) | Gets whether playback is ongoing.              |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7167f5c196fc5e167bfabde1a730e81d) | Pauses playback. The player will stop pulling data and freeze on the last frame. |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a41de8150eff044a237990c271d57ea27) | Resumes playback. The player will resume pulling data. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#adb8448443e6f0551eaad429d70b9f01c) | Seeks to a specified time point of the video stream (in seconds). |
| [currentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8b0ca7fda398996b355179bd9a479785) | Gets the current playback time point in seconds. |
| [duration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7fd4f66e650bd1656a97d1db7fabaeda) | Gets the total video duration in seconds. |
| [playableDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a4acb1f7a723d342f7bfb9c5e540e5e77) | Gets the playable video duration in seconds. |
| [width](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3eeed61a3424d2f907c8a1e420fddf6d) | Gets the video width. |
| [height](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a822ae85493a742654ba563619492b26a) | Gets the video height. |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a41001e6276c4853500f78579d6bd2218) | Sets the playback start time. |

### Video APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9646437dc38d7dcce8c32dfec5d0bc5b) | Gets the current video frame image.<br>**Note: Because this operation is time-consuming, the screenshot will be called back asynchronously.** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aaf347826e1a9fad9998c0eea9791ed0c) | Sets whether to flip the video image.                                                  |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1d79db46540e804a7bb9fc8cd87a3d99) | Sets the VOD playback speed. Default value: 1.0.                                |
| [bitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9a325ed94acf6b545c88755855449a12) | Returns the current playback bitrate index.                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a1aa8e1f3a63b46c8a1166447e2457abc) | Sets the current playback bitrate index for seamless definition switch. <br>You may need to wait momentarily to switch the definition. |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a3819261f776bfda7e95e3b0bf30445a4) | Sets the [image fill mode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae). |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ade93023de1bcd8374b62f5a2bf4beeee) | Sets the [rotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f). |

### Audio APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ----------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a861e656ed3fbdd5522fdf8801c07ab83) | Sets whether to mute the player.     |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#ac92633d1cdfff1f93f48b7aec1d35b98) | Sets the volume level. Value range: 0–100.           |

### Event notification APIs

| API                                                 | Description                                                                                                                   |
| ---------------------- | ---------------------- |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a6c78c9dda50ec1aa28a71d5548c45d71) | Sets player callbacks. We recommend you use [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) instead. |
| [vodDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a609f883ff450c123d75b04a902aabe79) | Sets player callbacks.                                 |
| [videoProcessDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a9eab6c2e67b2eae1bddf6fbf6978ba03) | Sets the video rendering callback (supported only if hardware encoding is used).                  |

### TRTC APIs

You can use the following APIs to push the audio/video streams of the VOD player through TRTC. For more information on TRTC services, see the TRTC [Overview](https://intl.cloud.tencent.com/document/product/647/35078) page.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#affcfcba7937a7ef88a918afb0b3d73bc) | Binds VOD to [TRTC](https://intl.cloud.tencent.com/document/product/647/35078). |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a5b947acf9f4fc992f0f02f8d87de3334) | Unbinds VOD from [TRTC](https://intl.cloud.tencent.com/document/product/647/35078). |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a8298f704cb659c725da28a27e08afbed) | Starts pushing the video stream.                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#aaa6ecf72bfa9e35078561dd98d62be0c) | Cancels pushing the video stream.                                             |
| [publishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | Starts pushing the audio stream.                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html#a206d786a74ae3b71766755135161773e) | Cancels pushing the audio stream.                                             |

## TXVodPlayListener

VOD callback notifications.
### Basic SDK callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayListener__ios.html#a6330db18bb40862fc2d66474fc34166b) | VOD playback event notification. For more information, see the [playback event list](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a) and [event parameters](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594). |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayListener__ios.html#a08721fef1ba130fd182de4bed3b4430e) | [Network status notification](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737) of the VOD player. |

## TXVodPlayConfig

VOD player configuration class.

### Basic configuration APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [connectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ad89d728973fb42eced3ac18be873af1b) | Sets the maximum number of player reconnection attempts.         |
| [connectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a07fde7cd21980c096b5bbd93aed137d5) | Sets the player reconnection interval in seconds.                                 |
| [timeout](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a39233eb85b4cbae04411577510e7c5e6) | Sets the player connection timeout period in seconds.                             |
| [cacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aec1a8f0064562368fe3c2df4f7fb72eb) | Sets the VOD cache directory, which takes effect for MP4 and HLS files.                       |
| [maxCacheItems](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aedbc9cc868baa2c44e3badbe6fdf4a43) | Sets the maximum number of cached files.                                           |
| [playerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a4595fb5853016c5e5919324e71ad6f4c) | Sets the player type.                                             |
| [headers](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ad69aaf8885027863ea19657425ef1974) | Sets custom HTTP headers.                                    |
| [enableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#ada91e71bad4df942e6190650915a7728) | Sets whether to enable accurate seek. Default value: true.                               |
| [autoRotate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa1a372684aaaf95b9b17abf0c7a4e6c6) | Sets whether to enable auto rotation. If the parameter is set to `YES` (default), MP4 files will be automatically rotated. <br>You can get the rotation angle from the `PLAY_EVT_CHANGE_ROTATION` callback. |
| [smoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa1caeddde1f950ec7965dcc721109928) | Sets whether to enable smooth switch for multi-bitrate HLS streams. Default value: false.                             |
| [progressInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#a943e212cbd5e3d89de0529ab7c6042fb) | Sets the progress callback interval in ms.                                 |
| [maxBufferSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__ios.html#aa4934cef81784d3a195a5d95a43953f5) | Sets the maximum buffer size in MB.                                    |
| maxPreloadSize                                               | Sets the maximum preloading size in MB.                                    |
| firstStartPlayBufferTime                                     | Sets the duration (ms) of video that needs to be loaded before playback starts. Default value: 100 ms. |
| nextStartPlayBufferTime                                      | Sets the minimum data to buffer when there is insufficient buffer data or after seeking is performed. Default value: 250 ms.  |
| overlayKey                                                   | Sets the HLS security hardening encryption and decryption key.                                   |
| overlayIv                                                    | Sets the HLS security hardening encryption and decryption IV.                                    |
| extInfoMap                                                   | Sets the extended information.                                               |
| preferredResolution                                          | Sets the preferred resolution. In case of multi-bitrate HLS streams, the resolution specified by `preferredResolution` (width x height) will be played. This API works only if it is called before playback. |
| enableRenderProcess                                          | Sets whether to enable post-rendering and post-processing (such as that used by the super-resolution plugin). They are enabled by default.    |

## TXPlayerGlobalSetting

Global configuration of the VOD player.

| API                                                                                                            | Description                                                                                                                                                                                     |
| ------------------ | ------------------------------------------------------------ |
| setCacheFolderPath | Sets the cache directory of the playback engine. After setting, this directory will be first read and written during predownloading and player use. |
| setMaxCacheSize    | Sets the playback engine’s maximum cache size in MB. The cache directory will be cleared automatically if its size exceeds the specified value. |

## TXVodPreloadManager

Predownloading API class of the VOD player.

| API                                                                                                            | Description                                                                                                                                                                                     |
| ------------- | ------------------------------------------------------------ |
| sharedManager | Gets a singleton object of `TXVodPreloadManager`.                    |
| startPreload | Starts predownloading. Before you call this API, make sure you have called `TXPlayerGlobalSetting#setCacheFolderPath` and `TXPlayerGlobalSetting#setMaxCacheSize` to set the cache directory and maximum cache size. |
| stopPreload   | Stops predownloading.                                                   |

## TXVodDownloadManager

Video download API class of the VOD player.

| API | Description |
| ------------------------ | ------------------------------------------------------------ |
| shareInstance            | Gets a singleton object of `TXVodDownloadManager`.                   |
| setDownloadPath          | Sets the root directory to save downloaded files.                                               |
| setHeaders               | Sets download HTTP headers.                                               |
| setListener              | Sets the download callback. This API must be called before the download.                             |
| startDownloadUrl         | Starts downloading the video at the specified URL.                                          |
| startDownload            | Starts downloading the video of the specified `FileID`.                                        |
| stopDownload             | Stops the download. If `ITXVodDownloadListener.onDownloadStop` is called back, the download stops successfully. |
| deleteDownloadFile       | Deletes the downloaded file.                                                 |
| deleteDownloadMediaInfo  | Deletes the download information.                                                 |
| getDownloadMediaInfoList | Gets the download lists of all users.                                   |



## ITXVodDownloadListener

VOD download notifications.

| API                                                                                                            | Description                                                                                                                                                                                     |
| ------------------ | -------------------------------------------- |
| onDownloadStart    | Download started.                                     |
| onDownloadProgress | The download progress was updated.                                 |
| onDownloadStop     | Download stopped.                                     |
| onDownloadFinish   | Download ended.                                     |
| onDownloadError    | An error occurred during download.                           |
| hlsKeyVerify       | The decryption key for downloading encrypted HLS files. |



## Error Codes

### Normal events

| Code | Event Definition | Description |
| ---- | -------------------------- | ----------------------------------------------------------- |
| 2004 | PLAY_EVT_PLAY_BEGIN        | Video playback started, and the loading icon animation (if any) ended.                |
| 2005 | PLAY_EVT_PLAY_PROGRESS     | The video playback progress (including the current playback progress, the loaded duration, and the total video duration).      |
| 2007 | PLAY_EVT_PLAY_LOADING      | The video is being loaded. The `LOADING_END` event will be reported if video playback resumes. |
| 2014 | PLAY_EVT_VOD_LOADING_END   | Video loading ended, and video playback resumed.                        |
| 2006 | PLAY_EVT_PLAY_END          | Video playback ended.                                           |
| 2013 | PLAY_EVT_VOD_PLAY_PREPARED | The player is ready.                                |
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
| 2103  | PLAY_WARNING_RECONNECT            | The player was disconnected and is trying to reconnect. The `PLAY_ERR_NET_DISCONNECT` event will be thrown after three failed attempts. |
| 2106  | PLAY_WARNING_HW_ACCELERATION_FAIL | Failed to start the hardware decoder, and the software decoder was used instead.   |
| -2304 | PLAY_ERR_HEVC_DECODE_FAIL         | H.265 decoding failed. |
| -2303 | PLAY_ERR_FILE_NOT_FOUND           | The file to be played back does not exist.                                           |
