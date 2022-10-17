## TXVodPlayer

### VOD player

For more information, see [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html).
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
| [setConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ae69bc2dd060217e595c38f0dc819290a) | Sets the player configuration information. For more information on the configuration, see [TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html). |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a64eefab5bdb76cef17f609560eec5830) | Sets the player's rendering view `TXCloudVideoView`. |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aeb2f15f370d50b6261b7832f02a0f411) | Sets the player's rendering view `TextureView`.                             |
| [setSurface](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ac06d94f1ed4ec1441c075e4ba556eb37) | Sets the player's rendering view `SurfaceView`.                             |
| setStringOption                                              | Sets the player business parameters in the format of `<String,Object>`.                |

### Basic playback APIs  
| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a32fe5a77dedc7fc903345f00e6c47c3a) | Starts playing back the video at the specified HTTP URL. |
| startPlay | Starts playing back the video of the specified `fileId` by passing in the `TXPlayInfoParams` parameter. |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a6abf34bf566c275476b1706593cb0fe1) | Stops playback. |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ac651fc45a9f04e4db6f258f8cdd7bbcf) | Gets whether playback is ongoing.      |
| [pause](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a7167f5c196fc5e167bfabde1a730e81d) | Pauses playback by stopping the retrieval of stream data and retaining the last-frame image. |
| [resume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a41de8150eff044a237990c271d57ea27) | Resumes playback by resuming the retrieval of stream data. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a914c54a0122cba5ad78d84f893df8578) | Seeks to a specified time point of the video stream (in seconds). |
| [seek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aa5d7fcf690ac3a1102ffa3c02192674d) | Seeks to a specified time point of the video stream (in ms). |
| [getCurrentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a128b89dd39053d6d19d262a5f45110cd) | Gets the current playback time point in seconds. |
| [getBufferDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#acebd6ae9dd87e10c8959a24d3b6d5e7f) | Gets the total buffer duration in seconds. |
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a83ee44393f1e0db930be75b73ff47812) | Gets the total video duration in seconds. |
| [getPlayableDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a37cb584556d48d043b93dfec33c40a97) | Gets the playable video duration in seconds. |
| [getWidth](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a67a0997183f24da19b776d96c1052998) | Gets the video width. |
| [getHeight](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a07efb2a4e9a982688c8bb3c3f21d1092) | Gets the video height. |
| [setAutoPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a5e0e3d950eb3f525634adc7a9f60eab7) | Sets whether to start VOD automatically after call of `startPlay`. VOD starts automatically by default. |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a8f767f79fb69496cdbc532fced5dff33) | Sets the playback start time. |
| [setToken](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a5f9eadc88ca97238f84226462f095536) | Sets the token for HLS encryption. |
| [setLoop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a3f5ae863c82509d1ed266503e8138781) | Sets whether to loop the video. |
| [isLoop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aaa3fcc823e0fce316dea1cc9162f1c8e) | Returns the loop playback status. |

### Video APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enableHardwareDecode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a33b092e7e79aab66b494e7034021b2f9) | Enables/Disables video hardware decoding.                                       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a6f1c0c128052960f084ef6d1d7a77b09) | Gets the current video frame image.<br>**Note: Because this operation is time-consuming, the screenshot will be called back asynchronously.** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a4add579d2ec825502c5e3832aced5bc1) | Sets whether to flip the video image horizontally.                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#add2bcd36c051900d697853155494865b) | Sets the VOD playback speed. Default value: 1.0.                                |
| [getBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#af6f9e1e680baa611642fb168007b1c45) | Returns the current playback bitrate index.                                     |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a61f524a6ed275edaf9e9a0997f64d491) | Sets the current playback bitrate index for seamless definition switch. You may need to wait momentarily to switch the definition. |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a6e1e1e12120b92f4884d3ea1a8e2cc94) | Sets the [image fill mode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae). |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | Sets the [image rendering angle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f). |

### Audio APIs

| API                                                          | Description                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a85d2bb3409165c1b7b2c53f8d61a03e2) | Sets whether to mute the player.                      |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a9b8946403b8b3ac8e11f3a78e9d531ca) | Sets the volume level. Value range: 0–100.           |
| [setRequestAudioFocus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a676f0935eca038719f58100d31f169b1) | Sets whether to get the audio focus automatically. The audio focus is gotten automatically by default. |

### Event notification APIs

| API | Description |
| ---------------------- | ---------------------- |
| [setPlayListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a0735b006fe8c56875665cb66881af144) | Sets the player callback (it has been disused, and we recommend you use [setVodListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61) instead). |
| [setVodListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61) | Sets the player callback.                                 |
| [onNotifyEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a1e4be8c3cfef68a8909d66a9243b6ec5) | VOD playback event notification.                                 |
| [onNetSuccess](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ae6febac01c1cba85f8fe387a0c14d9d0) | VOD network status notification.                             |
| [onNetFailed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a74942758292eb41138c7a01ed9056da2) | Network exception notification for playback by `fileId`.                         |

### TRTC APIs

You can use the following APIs to push the audio/video streams of the VOD player through TRTC. For more information on TRTC services, see the TRTC [Overview](https://intl.cloud.tencent.com/document/product/647/35078) page.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#ad6bd04b37a89012102e7bb71ea5554a6) | Binds VOD to [TRTC](https://intl.cloud.tencent.com/document/product/647/35078). |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a5b947acf9f4fc992f0f02f8d87de3334) | Unbinds VOD from [TRTC](https://intl.cloud.tencent.com/document/product/647/35078). |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a8298f704cb659c725da28a27e08afbed) | Starts pushing the video stream.                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#aaa6ecf72bfa9e35078561dd98d62be0c) | Cancels pushing the video stream.                                             |
| [publishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | Starts pushing the audio stream.                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#a206d786a74ae3b71766755135161773e) |  Cancels pushing the audio stream.                                             |

## ITXVodPlayListener

VOD callback notifications.
### Basic SDK callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXVodPlayListener__android.html#aad1d875808cd4a68d429762e492aad05) | VOD playback event notification. For more information, see the [playback event list](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a) and [event parameters](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594). |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXVodPlayListener__android.html#a2be0a0294ae21e68e736ac8fa4d3085d) | [Network status notification](https://liteav.sdk.qcloud.com/doc/api/zh-cn/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737) of the VOD player. |

## TXVodPlayConfig

VOD player configuration class.

### Basic configuration APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConnectRetryCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a30911117043dc5b3f559abf5eb1e9ce9) | Sets the maximum number of player reconnection attempts.                                         |
| [setConnectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a5f3b8315c6276bd1c03c999ce01e4f8f) | Sets the player reconnection interval in seconds.                                 |
| [setTimeout](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#ae44a6096c42cdb61adc10370ca2a42b6) | Sets the player connection timeout period in seconds.                             |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a6ad0d546e6da3abacd5d4ea8bd6f94de) | Sets the VOD cache directory, which takes effect for MP4 and HLS files.                       |
| [setMaxCacheItems](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#acc2f17764df9bb52163dac9faf81f11e) | Sets the maximum number of cached files. This API has been deprecated. Use `TXPlayerGlobalSetting#setMaxCacheSize` for global configuration. |
| [setPlayerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a3594024855210dc07f50a6d7c5f8b088) | Sets the player type.                                             |
| [setHeaders](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a9ca40412371b505f9d52fbe95fdbaa6f) | Sets custom HTTP headers.                                    |
| [setEnableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a3caff179964976945f3754f1ec48a42b) | Sets whether to enable accurate seek. Default value: true.                               |
| [setAutoRotate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#ab360b681c220c2adb57de2758916b227) | If it is set to `YES`, the MP4 file will be automatically rotated according to the rotation angle set in the file, which can be obtained from the `PLAY_EVT_CHANGE_ROTATION` event. Default value: YES |
| [setSmoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a23fb393011e4663d0dfa765b72665a46) | Sets whether to enable smooth switching for multi-bitrate HLS streams. Default value: false.                             |
| [setCacheMp4ExtName](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#aaeccb662be133d4ded4fc17df29b94b5) | Sets the cached MP4 file extension.                                        |
| [setProgressInterval](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a01a46ce89e4979a6397b6deb2525007c) | Sets the progress callback interval in ms.                                 |
| [setMaxBufferSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayConfig__android.html#a2705841bfedb3c44839cc355eaad26dc) | Sets the maximum preloading buffer size in MB.                                    |
| setMaxPreloadSize                                            | Sets the maximum preloading buffer size in MB.                                    |
| setExtInfo                                                   | Sets the extended information.                                               |
| setPreferredResolution                                       | Starts playing back the most preferred bitstream according to the configured `preferredResolution` if there are multiple HLS bitstreams. Here, `preferredResolution` is the product of the video width and height and can only take effect if it is set before playback starts. |

## TXPlayerGlobalSetting

Global configuration of the VOD player.

| API | Description |
| ------------------ | ------------------------------------------------------------ |
| setCacheFolderPath | Sets the cache directory of the playback engine. After setting, this directory will be first read and written during downloading, predownloading, and player use. |
| setMaxCacheSize    | Sets the maximum cache size in MB of the playback engine. After setting, the backend will clear files in the cache directory automatically according to the set value. |

## TXVodPreloadManager

Predownloading API class of the VOD player.

| API | Description |
| ------------ | ------------------------------------------------------------ |
| getInstance  | Gets the `TXVodPreloadManager` instance object in singleton mode.                    |
| startPreload | Sets the playback engine cache directory (`TXPlayerGlobalSetting#setCacheFolderPath`) and cache size (`TXPlayerGlobalSetting#setMaxCacheSize`) before starting predownloading. |
| stopPreload  | Stops predownloading.                                                   |

## TXVodDownloadManager 

Video download API class of the VOD player. Currently, only non-nested M3U8 videos can be downloaded. SimpleAES-encrypted videos will be encrypted again with Tencent Cloud's private encryption algorithm to improve the security.

| API | Description |
| ------------------------ | ------------------------------------------------------------ |
| getInstance              | Gets the `TXVodDownloadManager` instance object in singleton mode.                   |
| setHeaders               | Sets download HTTP headers.                                               |
| setListener              | Sets the download callback method, which must be set before download.                             |
| startDownloadUrl         | Starts downloading the video at the specified URL.                                          |
| startDownload            | Starts downloading the video of the specified `fileid`.                                        |
| stopDownload             | Stops the download. If `ITXVodDownloadListener.onDownloadStop` is called back, the download stops successfully. |
| deleteDownloadMediaInfo  | Deletes the download information.                                                 |
| getDownloadMediaInfoList | Gets the download lists of all users.                                   |
| getDownloadMediaInfo     | Gets the download information.                                   |

## ITXVodDownloadListener

VOD download notifications.

| API | Description |
| ------------------ | -------------------------------------------- |
| onDownloadStart    | Download started.                                     |
| onDownloadProgress | The download progress was updated.                                 |
| onDownloadStop     | Download stopped.                                     |
| onDownloadFinish   | Download ended.                                     |
| onDownloadError    | An error occurred during download.                           |


## TXVodDownloadDataSource

Tencent Cloud video `fileid` download source, which can be passed in as a parameter during download.

| API | Description |
| ------------------         | -------------------------------------------- |
| TXVodDownloadDataSource    | Builds a function to pass in parameters such as `appid`, `fileid`, `quality`, `psign`, and `username`.                                    |
| getAppId  | Gets the `appid` that is passed in.                                |
| getFileId  | Gets the `fileid` that is passed in.                                |
| getPSign     | Gets the `psign` that is passed in.                                     |
| getQuality   | Gets the `quality` that is passed in.                                     |
| getUserName    | Gets the `userName` that is passed in, which is `default` by default.                          |


## TXVodDownloadMediaInfo

Class to get VOD download information such as download progress and playback link.

| API | Description |
| ------------------         | -------------------------------------------- |
| getDataSource    | Gets the download source specified by the `fileid` passed in for video download by `fileid`.                                    |
| getDuration  | Gets the total duration of the downloaded video.                                |
| getPlayableDuration  | Gets the playable duration of the downloaded video.                                |
| getSize     | Gets the total size of the file being downloaded. This API takes effect only for download by `fileid`.            |
| getDownloadSize   | Gets the size of the downloaded file. This API takes effect only for download by `fileid`.            |
| getProgress    | Gets the current download progress.                         |
| getPlayPath    | Gets the current playback path, which can be passed in to `TXVodPlayer` for playback.                         |
| getDownloadState    | Gets the download status.                       |
| isDownloadFinished    | Determines whether the download is completed.                       |


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
| ------ | ------------------------------------- | ------------------------------------------------------- |
| \-2301 | PLAY\_ERR\_NET\_DISCONNECT            | The network was disconnected and could not be reconnected after multiple retries. You can restart the player to perform more connection retries. |
| \-2305 | PLAY\_ERR\_HLS\_KEY                   | Failed to get the HLS decryption key.                                  |
| 2101   | PLAY\_WARNING\_VIDEO\_DECODE\_FAIL    | Failed to decode the current video frame.  |
| 2102   | PLAY\_WARNING\_AUDIO\_DECODE\_FAIL    | Failed to decode the current audio frame.  |
| 2103   | PLAY\_WARNING\_RECONNECT              | The network was disconnected, and automatic reconnection was performed (the `PLAY_ERR_NET_DISCONNECT` event will be thrown after three failed attempts). |
| 2106   | PLAY\_WARNING\_HW\_ACCELERATION\_FAIL | Failed to start the hardware decoder, and the software decoder was used instead.   |
| \-2304 | PLAY\_ERR\_HEVC\_DECODE\_FAIL         | Failed to decode with H.265. |
| \-2303 | PLAY\_ERR\_FILE\_NOT\_FOUND           | The file to be played back does not exist.                                               |
