## TXVodPlayer

### VOD player

See [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html).
The player pulls audio/video data from the specified VOD stream URL and plays the data after decoding and local rendering.
The player has the following capabilities:

- FLV, MP4, and HLS files can be played back in two playback methods: basic playback (by URL) and VOD playback (by `Fileid `).
- Screenshots of the video stream can be taken.
- The brightness, volume level, and playback progress can be adjusted through gestures.
- Resolution can be switched manually or resolution can be automatically switched to adapt to the current network bandwidth.
- Different playback speeds can be specified, videos can be flipped horizontally, and hardware acceleration can be enabled.
- For more information about all capabilities of the player, see [Overview](https://www.tencentcloud.com/document/product/266/38295).

### Player configuration APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ae69bc2dd060217e595c38f0dc819290a) | Sets the player configuration information. For more information on the configuration, see [TXVodPlayConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html). |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a64eefab5bdb76cef17f609560eec5830) | Sets the player's rendering view `TXCloudVideoView`. |
| [setPlayerView](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aeb2f15f370d50b6261b7832f02a0f411) | Sets the player's rendering view `TextureView`.                             |
| [setSurface](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ac06d94f1ed4ec1441c075e4ba556eb37) | Sets the player's rendering view `SurfaceView`.                             |
| [setStringOption](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a23eedd175a85f171cb7c34638bab0c45) | Sets the player business parameters in the format of `<String,Object>`.                |

### Basic playback APIs  
| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ----------------------------------------------------- |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a32fe5a77dedc7fc903345f00e6c47c3a) | Starts playing back the video at the specified HTTP URL. |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ac255cbe3a0481014f3d8aa4a6ca4d581) | Starts playing back the video of the specified `fileId` by passing in the `TXPlayInfoParams` parameter. |
| [startPlayDrm](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a1e8443952146701507adb219d8b992b1) | Plays back a DRM-encrypted video.|
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a6abf34bf566c275476b1706593cb0fe1) | Stops playback.                      |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ac651fc45a9f04e4db6f258f8cdd7bbcf) | Gets whether playback is ongoing.                  |
| [pause](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a7167f5c196fc5e167bfabde1a730e81d) | Pauses playback by stopping the retrieval of stream data and retaining the last-frame image. |
| [resume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a41de8150eff044a237990c271d57ea27) | Resumes playback by getting the stream data again. |
| [seek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a914c54a0122cba5ad78d84f893df8578) | Seeks to a specified time point of the video stream (in seconds). |
| [seek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aa5d7fcf690ac3a1102ffa3c02192674d) | Seeks to a specified time point of the video stream (in ms). |
| [getCurrentPlaybackTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a128b89dd39053d6d19d262a5f45110cd) | Gets the current playback time point in seconds. |
| [getBufferDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#acebd6ae9dd87e10c8959a24d3b6d5e7f) | Gets the total buffer duration in seconds. |
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a83ee44393f1e0db930be75b73ff47812) | Gets the total video duration in seconds. |
| [getPlayableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a37cb584556d48d043b93dfec33c40a97) | Gets the playable video duration in seconds. |
| [getWidth](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a67a0997183f24da19b776d96c1052998) | Gets the video width. |
| [getHeight](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a07efb2a4e9a982688c8bb3c3f21d1092) | Gets the video height. |
| [setAutoPlay](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a5e0e3d950eb3f525634adc7a9f60eab7) | Sets whether to start VOD automatically after call of `startPlay`. VOD starts automatically by default. |
| [setStartTime](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a8f767f79fb69496cdbc532fced5dff33) | Sets the playback start time. |
| [setToken](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a5f9eadc88ca97238f84226462f095536) | Sets the token for HLS encryption. |
| [getEncryptedPlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#acc32bf00b94774e5314cb733f9f339df) | Gets the encrypted playback key.                            |
| [setLoop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a3f5ae863c82509d1ed266503e8138781) | Sets whether to loop the video. |
| [isLoop](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aaa3fcc823e0fce316dea1cc9162f1c8e) | Returns the loop playback status. |

### Video APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enableHardwareDecode](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a33b092e7e79aab66b494e7034021b2f9) | Enables/Disables video hardware decoding.                                       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a6f1c0c128052960f084ef6d1d7a77b09) | Gets the current video frame image.<br/>**Note: Because this operation is time-consuming, the screenshot will be called back asynchronously.** |
| [setMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a4add579d2ec825502c5e3832aced5bc1) | Sets whether to flip the video image horizontally.                                                   |
| [setRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#add2bcd36c051900d697853155494865b) | Sets the VOD playback speed. Default value: 1.0.                                |
| [getBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#af6f9e1e680baa611642fb168007b1c45) | Returns the current playback bitrate index.                                     |
| [getSupportedBitrates](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aedacfbc888f5446ab2318ea3a7199700) | Returns the supported bitrates (definitions) if the playback address is HLS. |
| [setBitrateIndex](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a61f524a6ed275edaf9e9a0997f64d491) | Sets the current playback bitrate index for seamless definition switch. You may need to wait momentarily to switch the definition. |
| [setRenderMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a6e1e1e12120b92f4884d3ea1a8e2cc94) | Sets the [image fill mode](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a0645160ad90c67581f7f226a6c0c46ae). |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | Sets the [image rendering angle](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#ad00f3ee125e574cab63d955e03f5f23f). |

### Audio APIs

| API                                                          | Description                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a85d2bb3409165c1b7b2c53f8d61a03e2) | Sets whether to mute the player.                      |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a9b8946403b8b3ac8e11f3a78e9d531ca) | Sets the volume level. Value range: 0–100.           |
| [setRequestAudioFocus](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a676f0935eca038719f58100d31f169b1) | Sets whether to get the audio focus automatically. The audio focus is gotten automatically by default. |

### Event notification APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setPlayListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a0735b006fe8c56875665cb66881af144) | Sets the player callback (this API has been deprecated, and we recommend you use [setVodListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61)). |
| [setVodListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#adb0e51670b947f15cca9a98d7d804e61) | Sets the player callback.                                       |

### TRTC APIs

You can use the following APIs to push the audio/video streams of the VOD player through TRTC. For more information on TRTC services, see the TRTC [Overview](https://cloud.tencent.com/document/product/647/16788) page.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [attachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#ad6bd04b37a89012102e7bb71ea5554a6) | Binds VOD to [TRTC](https://cloud.tencent.com/document/product/647/16788). |
| [detachTRTC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a5b947acf9f4fc992f0f02f8d87de3334) | Unbinds VOD from [TRTC](https://cloud.tencent.com/document/product/647/16788). |
| [publishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a8298f704cb659c725da28a27e08afbed) | Starts pushing the video stream.                                             |
| [unpublishVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#aaa6ecf72bfa9e35078561dd98d62be0c) | Cancels pushing the video stream.                                             |
| [publishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a7f1b46c4ae27f86188dc29f0f5d64b95) | Starts pushing the audio stream.                                             |
| [unpublishAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayer__android.html#a206d786a74ae3b71766755135161773e) |  Cancels pushing the audio stream.                                             |

## ITXVodPlayListener

VOD callback notifications.
### Basic SDK callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onPlayEvent](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPlayListener__android.html#aad1d875808cd4a68d429762e492aad05) | VOD playback event notification. For more information, see the [playback event list](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a3c3fa833bb8585df2f362da5b70c610a) and [event parameters](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#a5cb5e37938b510270847d4f5c751a594). |
| [onNetStatus](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPlayListener__android.html#a2be0a0294ae21e68e736ac8fa4d3085d) | VOD player [network status notification](https://liteav.sdk.qcloud.com/doc/api/en/classcom_1_1tencent_1_1rtmp_1_1TXLiveConstants.html#aa7190fc964cf23a567b56d9793ad5737). |

## TXVodPlayConfig

VOD player configuration class.

### Basic configuration APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setConnectRetryCount](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a30911117043dc5b3f559abf5eb1e9ce9) | Sets the maximum number of player reconnection attempts.                                         |
| [setConnectRetryInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a5f3b8315c6276bd1c03c999ce01e4f8f) | Sets the player reconnection interval in seconds.                                 |
| [setTimeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#ae44a6096c42cdb61adc10370ca2a42b6) | Sets the player connection timeout period in seconds.                             |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a6ad0d546e6da3abacd5d4ea8bd6f94de) | Sets the VOD cache directory, which takes effect for MP4 and HLS files. <br/>This API has been deprecated and is not recommended. |
| [setMaxCacheItems](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#acc2f17764df9bb52163dac9faf81f11e) | Sets the maximum number of cached files. <br/>This API has been deprecated and is not recommended. |
| [setPlayerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a3594024855210dc07f50a6d7c5f8b088) | Sets the player type. <br>This API has been deprecated and is not recommended. |
| [setHeaders](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a9ca40412371b505f9d52fbe95fdbaa6f) | Sets custom HTTP headers.                                    |
| [setEnableAccurateSeek](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a3caff179964976945f3754f1ec48a42b) | Sets whether to enable accurate seek. Default value: true.                               |
| [setAutoRotate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#ab360b681c220c2adb57de2758916b227) | If it is set to `YES`, the MP4 file will be automatically rotated according to the rotation angle set in the file, which can be obtained from the `PLAY_EVT_CHANGE_ROTATION` event. Default value: YES |
| [setSmoothSwitchBitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a23fb393011e4663d0dfa765b72665a46) | Sets whether to enable smooth switching for multi-bitrate HLS streams. Default value: false.                             |
| [setCacheMp4ExtName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#aaeccb662be133d4ded4fc17df29b94b5) | Sets the cached MP4 file extension.                                        |
| [setProgressInterval](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a01a46ce89e4979a6397b6deb2525007c) | Sets the progress callback interval in ms.                                 |
| [setMaxBufferSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a2705841bfedb3c44839cc355eaad26dc) | Sets the maximum preloading buffer size in MB.                                    |
| [setMaxPreloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a78d73bb26332151cbf5f8aa10240a4a5) | Sets the maximum preloading buffer size in MB.                         |
| [setExtInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a080c7ab4f3b6f06e690561889eca3594) | Sets the extended information.                                               |
| [setPreferredResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a369c5980be4748b11216a686482e910f) | Starts playing back the most preferred bitstream according to the configured `preferredResolution` if there are multiple HLS bitstreams. Here, `preferredResolution` is the product of the video width and height (width x height) and can only take effect if it is set before playback starts. |
| [setOverlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#abd8626115358e211fcbc5347a34b2e18) | Sets the HLS security hardening encryption and decryption key.                                   |
| [setOverlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#adcdc2c60303e4b67757583904836dfab) | Sets the HLS security hardening encryption and decryption IV.                                    |
| [setEnableRenderProcess](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#ab48a6ca2e64a61942f714c2b74710ba8) | Sets whether to allow postrendering and postproduction features. |
| [setMediaType](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPlayConfig__android.html#a532518afe8abf910920278a0c21f225f) | Sets the media asset type, which is `auto` by default.                             |

## TXPlayerGlobalSetting

Global configuration of the VOD player.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setCacheFolderPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__android.html#adf3cf9c0b96e7eeb97b5e9ed56743df8) | Sets the cache directory of the playback engine. After setting, this directory will be first read and written during downloading, predownloading, and player use. |
| [setMaxCacheSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerGlobalSetting__android.html#a27de4890873400d4d4ff2c624138786d) | Sets the maximum cache size in MB of the playback engine. After setting, the backend will clear files in the cache directory automatically according to the set value. |

## TXVodPreloadManager

Predownloading API class of the VOD player.

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | --------------------------------------------- |
| [getInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__android.html#a9e52c1e94ef4b2a35fdb6dfbf89f5e92) | Gets the `TXVodPreloadManager` instance object in singleton mode.                    |
| [startPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__android.html#a1968e49655bc231c54247f9189176911) | Sets the playback engine cache directory before starting predownloading. |
| [stopPreload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodPreloadManager__android.html#aa8425852d9c185f71b3933ac61834c5c) | Stops predownloading.                                                   |

## ITXVodPreloadListener

The callback for video predownloading.

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [onComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPreloadListener__android.html#a2004a619f03a97617661985f0f79a767) | Video predownloading is completed. |
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodPreloadListener__android.html#aac11d56117d32f2e1bf6afafb940db77) | An error occurred during video predownload.   |

## TXVodDownloadManager 

Video download API class of the VOD player. Currently, only non-nested M3U8 videos can be downloaded. SimpleAES-encrypted videos will be encrypted again with Tencent Cloud's private encryption algorithm to improve the security.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a84b3db42095ccb149b8f9be57ecdc0cc) | Gets the `TXVodDownloadManager` instance object in singleton mode.                   |
| [setHeaders](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a9ca40412371b505f9d52fbe95fdbaa6f) | Sets download HTTP headers.                                               |
| [setListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a123ff28866dca6b525f1f2defde28199) | Sets the download callback method, which must be set before download.                             |
| [startDownloadUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a3e6424357de962092cff42d4c1a68654) | Starts downloading the video at the specified URL.                                          |
| [startDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a1d58d3e216c1016eb8d5cc051dd300f7) | Starts downloading the video of the specified `fileid`.                                        |
| [stopDownload](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a86b884a71a6a11e729a964478612ed65) | Stops the download. If `ITXVodDownloadListener.onDownloadStop` is called back, the download stops successfully. |
| [deleteDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a0dab7dad33ef2b555abf31f07ab6447d) | Deletes the download information.                                                 |
| [getDownloadMediaInfoList](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#ad82cf86e7bad17efa86df162a4286a05) | Gets the download lists of all users.                                   |
| [getDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#ac8b38266ea66940fdd406487ff45a2fd) | Gets the download information.                                   |
| [getDownloadMediaInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadManager__android.html#a7e03beed3e30d3243b91853856da9d53) | Gets the download information.                                   |

## ITXVodDownloadListener

VOD download notifications.

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ----------------------------------------------- |
| [onDownloadStart](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a3cbbd786c51f86aba84a182edd054343) | Download started.   |
| [onDownloadProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a4dd74690b9ed22442ba9956d29d69b32) | The download progress was updated.                                    |
| [onDownloadStop](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#ac70254aa0f35a4ba01fc8de93214112b) | Download stopped.   |
| [onDownloadFinish](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a0b6eb0287eea736f84ebe8c212ab2219) | Download ended.                                         |
| [onDownloadError](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#ae0faac6397f8df5a2d1e57e56e6e4ec3) | An error occurred during download.                           |
| [hlsKeyVerify](https://liteav.sdk.qcloud.com/doc/api/en/group__ITXVodDownloadListener__android.html#a206077037e4a5f8ef81707ec82514523) | Verifies the decryption key by the player if an encrypted file is found during HLS stream download. |


## TXVodDownloadDataSource

Tencent Cloud video `fileid` download source, which can be passed in as a parameter during download.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [TXVodDownloadDataSource](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aef4a9306eddebbd7920089e48e09b260) | Builds a function to pass in parameters such as `appid`, `fileid`, `quality`, `psign`, and `username`.                                    |
| [getAppId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#ab95e1b8c990ed3e41fc623e5e9ed47c3) | Gets the `appid` that is passed in.                                |
| [getFileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aae60f2e5054da59d0f2d239d0e673cc8) | Gets the `fileid` that is passed in.                                |
| [getPSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aa7c355a0046a91c5f302f1602b985462) | Gets the `psign` that is passed in.                                     |
| [getQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#ab03cb85fa393531d1fb702ab1e92008f) | Gets the `quality` that is passed in.                                     |
| [getUserName](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#ae3cc9307a896bbfcf570a0d077708f58) | Gets the `userName` that is passed in, which is `default` by default.                          |
| [getToken](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a20c1ba8630591cc399a35a7abc535728) | Gets the `token` that is passed in.                                     |
| [getOverlayKey](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a8cceb76d2594cecb6615652a854e3245) | Gets the `overlayKey` that is passed in.                                |
| [getOverlayIv](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a86ac7a9d6239880059fc109128c9bb4b) | Gets the `overlayIv` that is passed in.                                     |

### Definition ID constants

| Code | Constant Definition | Description |
| ---- | ------------------------------------------------------------ | -------- |
| 0    | [QUALITY_OD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#abb1129f5ddec88f4eb579e96afdd741a) | Original     |
| 1    | [QUALITY_FLU](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a5b5a1363633c76ecfb35dea5daf3e0b2) | LD     |
| 2    | [QUALITY_SD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aad857cb177a777ba09aed2a312a3fe1f) | SD     |
| 3    | [QUALITY_HD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a70195f7d2882bf1918f599ff1c555717) | HD     |
| 4    | [QUALITY_FHD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#aff4ebd940acb1937be588b6eb7879183) | FHD   |
| 5    | [QUALITY_2K](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a69635e7ebfc9895b840c7a5f1817e7b3) | 2K       |
| 6    | [QUALITY_4K](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a35eb8012dab226b7d0714ad98560715d) | 4K       |
| 1000 | [QUALITY_UNK](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadDataSource__android.html#a3380895e1edc2eb4394cac5d2b40fda5) | Undefined   |

## TXVodDownloadMediaInfo

Class to get VOD download information such as download progress and playback link.

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | -------------------------------------------- |
| [getDataSource](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#ab8d408191666ef004ae7d1e4f8d4840a) | Gets the download source specified by the `fileid` passed in for video download by `fileid`.                                    |
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a08c13081c0665a4336a0f022c955fb69) | Gets the total duration of the downloaded video.                                |
| [getPlayableDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#aea8be4cac1aaa5b79a1c3faf13ece59c) | Gets the playable duration of the downloaded video.                                |
| [getSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a3c4029b904a61a9873e6d12785ce19a1) | Gets the total size of the file being downloaded. This API takes effect only for download by `fileid`.            |
| [getDownloadSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#ab2ab8161365b107da0cf398c2e683533) | Gets the size of the downloaded file. This API takes effect only for download by `fileid`.            |
| [getProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#afdfeed8666fff88f32b73cbd1d3a2770) | Gets the current download progress.                         |
| [getPlayPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a52f40379c9ced15ea1d26d800ad6ac4b) | Gets the current playback path, which can be passed in to `TXVodPlayer` for playback.                         |
| [getDownloadState](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a2184d61558a641a71115c9efe9ad3a48) | Gets the download status.                       |
| [isDownloadFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#aed26755c5919fc7125e4e2400d30d1bc) | Determines whether the download is completed.                       |

### Static attributes

| Code | Attribute Definition | Description |
| ---- | ------------------------------------------------------------ | ---------- |
| 0    | [STATE_INIT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a1ac9cfa17538972c579f1bff39c2fe83) | Download was initialized.  |
| 1    | [STATE_START](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a89be56b1eb6cd1441eae8ee501a995e1) | Download started.   |
| 2    | [STATE_STOP](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a88533f2a5acf4b41400bd14feeab9106) | Download stopped.   |
| 3    | [STATE_ERROR](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#a7474da17fe98cc77b5bfd257f5f39317) | An error occurred during download.   |
| 4    | [STATE_FINISH](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodDownloadMediaInfo__android.html#abd0a89abf65650e0e16b613e34d8466f) | Download was completed.   |

## TXPlayerAuthBuilder

The configuration for encrypted video playback through `fileId`.

| API                                                          | Description                 |
| ------------------------------------------------------------ | -------------------- |
| [setAppId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#a0b43955512510cd5c4930c236f3666bb) | The application's `appId`.         |
| [setFileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#abd423a3f7b11333d1b68506e25e4b77e) | The file ID.             |
| [setTimeout](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#ac8cc3ccb3adfc2533c4a8fa97274625d) | The encrypted link timeout timestamp. |
| [setExper](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#a9855f630f9444c767a8085d68892faa1) | The preview duration.           |
| [setUs](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#aca22d76e37e78b330084f6b228594894) | The unique request ID.       |
| [setSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#afb81925d434438d6903b8016b0f26d8d) | The hotlink protection signature.         |
| [setHttps](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerAuthBuilder__android.html#adcd67a70185ef7680ecfe0162aee0273) | Whether to use HTTPS requests.    |

## TXBitrateItem

The video bitrate information.

| API                                                          | Description                     |
| ------------------------------------------------------------ | -------------------------- |
| [index](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#a750b5d744c39a06bfb13e6eb010e35d0) | The number of the stream in the m3u8 file. |
| [width](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#a2474a5474cbff19523a51eb1de01cda4) | The video width of this stream.    |
| [height](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#ad12fc34ce789bce6c8a05d8a17138534) | The video height of this stream.    |
| [bitrate](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#ab5d8e1788d02d0e52941a0778776e289) | The video bitrate of this stream.    |
| [compareTo](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBitrateItem__android.html#a1062863c4ed9def2a8af6edb834792a0) | Whether the bitrates of two streams are the same.|

## TXImageSprite

The image sprite parsing class.

| API                                                          | Description                               |
| ------------------------------------------------------------ | ---------------------------------- |
| [TXImageSprite](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#a0daa097ae5eaabb45ce5899d641108be) | Constructor.                          |
| [setVTTUrlAndImageUrls](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#aea98e261dc8911344659a9e6c113f8e8) | Sets the image sprite URL. |
| [getThumbnail](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#a16a3b680fcd8da1468d3ccfe675d47ed) | Gets a thumbnail.     |
| [release](https://liteav.sdk.qcloud.com/doc/api/en/group__TXImageSprite__android.html#a23b477d0e2d399f75d585d154c346591) | This API must be called after use; otherwise, memory leaks will occur. |

## TXPlayerDrmBuilder

The DRM playback information.

| API                                                          | Description                  |
| ------------------------------------------------------------ | --------------------- |
| [TXPlayerDrmBuilder](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#acee757f8bcb8d6af23f4963184f7b791) | Constructs a DRM playback information object. |
| [setProvisionUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#a5f55511af44ef3e6619988d4002d1aa5) | Sets the URL of the certificate provider. |
| [setKeyLicenseUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#ac293b2b09e849a2b54382180c44dc37f) | Sets the URL of the decryption key. |
| [setPlayUrl](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayerDrmBuilder__android.html#ad3970dca8235512ed26d2afd492de595) | Sets the URL of the media file to be played back. |

## TXPlayInfoParams

Parameters for video playback through `fileId`.

| API                                                          | Description                  |
| ------------------------------------------------------------ | ------------------------ |
| [TXPlayInfoParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#a1f5bbdc7d3a4817ace0ff64e70af964c) | Constructor.               |
| [getAppId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#ab95e1b8c990ed3e41fc623e5e9ed47c3) | Gets the application's `appId`.             |
| [getFileId](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#aae60f2e5054da59d0f2d239d0e673cc8) | Gets the file ID.             |
| [getPSign](https://liteav.sdk.qcloud.com/doc/api/en/group__TXPlayInfoParams__android.html#aa7c355a0046a91c5f302f1602b985462) | Gets the encryption signature of a video. |



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
| ------ | ------------------------------------- | ------------------------------------------------------------ |
| \-2301 | PLAY\_ERR\_NET\_DISCONNECT            | The network was disconnected and could not be reconnected after multiple retries. You can restart the player to perform more connection retries. |
| \-2305 | PLAY\_ERR\_HLS\_KEY                   | Failed to get the HLS decryption key.                                  |
| 2101   | PLAY\_WARNING\_VIDEO\_DECODE\_FAIL    | Failed to decode the current video frame.  |
| 2102   | PLAY\_WARNING\_AUDIO\_DECODE\_FAIL    | Failed to decode the current audio frame.  |
| 2103   | PLAY\_WARNING\_RECONNECT              | The network was disconnected, and automatic reconnection was performed (the `PLAY_ERR_NET_DISCONNECT` event will be thrown after three failed attempts). |
| 2106   | PLAY\_WARNING\_HW\_ACCELERATION\_FAIL | Failed to start the hardware decoder, and the software decoder was used instead.   |
| \-2304 | PLAY\_ERR\_HEVC\_DECODE\_FAIL         | Failed to decode with H.265. |
| \-2303 | PLAY\_ERR\_FILE\_NOT\_FOUND           | The file to be played back does not exist.                                               |

## Player SDK Constants

The following constants are made available through `TXVodConstants` starting from v10.0:

### Image fill mode

| Code | Event Definition | Description |
| ---- | ------------------------------------------------------------ | ------------------ |
| 0    | [RENDER_MODE_FULL_FILL_SCREEN](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0645160ad90c67581f7f226a6c0c46ae) | The video image is scaled proportionally to fill the entire screen. |
| 1    | [RENDER_MODE_ADJUST_RESOLUTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga7bc7babd208fa82866f80e9340a5354c) | The video image is scaled proportionally to fit the screen. |

### Image rendering angle

| Code | Event Definition | Description |
| ---- | ------------------------------------------------------------ | -------- |
| 0    | [RENDER_ROTATION_PORTRAIT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gad00f3ee125e574cab63d955e03f5f23f) | Normal portrait mode. |
| 270  | [RENDER_ROTATION_LANDSCAPE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga17bdfecb387ddb3b34a96a0474bd73e3) | Landscape mode (90-degree clockwise rotation). |

### Playback event list

| Code | Event Definition | Description |
| ----- | ------------------------------------------------------------ | ------------------------------ |
| 2003  | [VOD_PLAY_EVT_RCV_FIRST_I_FRAME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gad745daba38f53e17c19f648e51246044) | The network received the first renderable video data packet (IDR).  |
| 2004  | [VOD_PLAY_EVT_PLAY_BEGIN](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gada58f2a016424a22d053ff02818b705e) | Video playback started.                                               |
| 2005  | [VOD_PLAY_EVT_PLAY_PROGRESS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga69a17c951f665b929c0ced3e946b41b0) | The video playback progress was changed.                   |
| 2006  | [VOD_PLAY_EVT_PLAY_END](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga9a4e84bd9d9e9c7ae1db0cfd3875e74a) | Video playback ended.                                           |
| 2007  | [VOD_PLAY_EVT_PLAY_LOADING](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga755928f9307a228f5b94c054fe888384) | The video is loading.                                               |
| 2008  | [VOD_PLAY_EVT_START_VIDEO_DECODER](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga7c3fc61aaa8865bccee4deb0b237f9e0) | The decoder started. |
| 2009  | [VOD_PLAY_EVT_CHANGE_RESOLUTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa02aa77b481d6817ddd60ca3cad7131e) | The video resolution changed.    |
| 2010  | [VOD_PLAY_EVT_GET_PLAYINFO_SUCC](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaebd8ad6fe4c09ebb9205422ed072b61f) | Obtained the VOD file information successfully. |
| 2011  | [VOD_PLAY_EVT_CHANGE_ROTATION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga440c3d89bec97cea7170d293d590d5fd) | The video is rotated.                   |
| 2013  | [VOD_PLAY_EVT_VOD_PLAY_PREPARED](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga81e281a76a84d61f9f76cc45d51b7bd7) | The video is loaded. |
| 2014  | [VOD_PLAY_EVT_VOD_LOADING_END](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga22ef1d7404af3661eb6b600a6e6399fd) | Loading ended.                    |
| 2026  | [VOD_PLAY_EVT_RCV_FIRST_AUDIO_FRAME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaecd3bbe2687021e769985deb88bd04ce) | The audio is played back for the first time. |
| 2103  | [VOD_PLAY_WARNING_RECONNECT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga029b64e10522699e622bd42706d10f65) | Network disconnected. Automatic reconnection has been enabled. |
| -2301 | [VOD_PLAY_ERR_NET_DISCONNECT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae0ebb051cf1166a8c71cd0b981d260cc) | The network was disconnected and could not be reconnected after multiple retries.  |
| -2303 | [VOD_PLAY_ERR_FILE_NOT_FOUND](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga1e71f9fdafabb1bd16fab933c308d070) | The file does not exist. |
| -2304 | [VOD_PLAY_ERR_HEVC_DECODE_FAIL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga79b7f1b580d0cab34fc5616ae474660f) | Failed to decode with H.265. |
| -2305 | [VOD_PLAY_ERR_HLS_KEY](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa3130bf22ec63513ddca17ef3a24267a) | Failed to get the HLS decryption key.                                  |
| -2306 | [VOD_PLAY_ERR_GET_PLAYINFO_FAIL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0b2d0a807f32a21c215eb0d523d1ba67) | Failed to get the VOD file information. |
| 2106  | [VOD_PLAY_WARNING_HW_ACCELERATION_FAIL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaf669a195862852295bbfd67d77143097) | Failed to start the hardware decoder, and the software decoder was used instead.   |
| -5    | [VOD_PLAY_ERR_INVALID_LICENSE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gafde8fcf56aeef512220ea06e92db2e40) | The license was invalid, and playback failed. |

### Playback event parameters

| Event Definition | Description |
| ------------------------------------------------------------ | ---------------------------- |
| [EVT_UTC_TIME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gafee483734d4d3a831a30c602406e77d6) | The UTC time |
| [EVT_TIME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga5cb5e37938b510270847d4f5c751a594) | The event occurrence time |
| [EVT_DESCRIPTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga103453280f89ab536f1cc18f7b3cbf53) | The event description |
| [EVT_PARAM1](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gad627c73ec08206efdd221293acc5e716) | Event parameter 1                    |
| [EVT_PARAM2](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa15b5dbb07de07d1b2dbe14cfcd4c3f8) | Event parameter 2                    |
| [EVT_PLAY_COVER_URL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga40e4910ac679c2301b56d2b353782c45) | The video thumbnail |
| [EVT_PLAY_URL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gac913635a62c07ee774965c946db60cae) | The video URL |
| [EVT_PLAY_NAME](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga018b2b66f3393288356448fd2520049b) | The video name |
| [EVT_PLAY_DESCRIPTION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga78f0b6a56bce879ab53e5c955ae9b72a) | The video description                     |
| [EVT_PLAY_PROGRESS_MS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0aa1661deb8e647fab5fd9f49e80c7f9) | The playback progress in milliseconds |
| [EVT_PLAY_DURATION_MS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga3abe5f92aa39728811ef148c2a9ad830) | The total playback duration in milliseconds |
| [EVT_PLAY_PROGRESS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga3f1f479ffccbb042f9fdf3f21a3276fc) | The playback progress                     |
| [EVT_PLAY_DURATION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga2c453eed399f105eec5803a3894ad81d) | The total playback duration                     |
| [EVT_PLAYABLE_DURATION_MS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga315c2ebea16fbabde6dfa05b46365ec1) | The playable duration of the VOD file in milliseconds |
| [EVT_PLAYABLE_RATE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gab00428b5d3902980f809f281ab3113cd) | The playback speed                     |
| [EVT_PLAYABLE_DURATION](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga27916804840b52c8b012c65f23f5295c) | The playable duration of the VOD file               |
| [EVT_IMAGESPRIT_WEBVTTURL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gac5b62b9cd23553e5caa4ea25b8093594) | The download URL of the image sprite WebVTT file |
| [EVT_IMAGESPRIT_IMAGEURL_LIST](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga8b4b82a700fad6dc290c6b9df836b379) | The download URL of the image sprite            |
| [EVT_DRM_TYPE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga8f621b0e05158b432a9bfce15b51929d) | The encryption type                     |
| [EVT_CODEC_TYPE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga9aea07e52f99dfc5ce83e627207c3013) | The video codec type                 |
| [EVT_KEY_FRAME_CONTENT_LIST](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaf27d14de4e5ba1057f1687fb953bf0d6) | The video keyframe description           |
| [EVT_KEY_FRAME_TIME_LIST](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaad3ea1d65ffad606f0e72b45229c883a) | The keyframe time          |

### Playback network status notification parameters

| Event Definition | Description |
| ------------------------------------------------------------ | ------------------- |
| [NET_STATUS_CPU_USAGE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga66b91ad00c61489fc2d7465999d1a77a) | The CPU utilization           |
| [NET_STATUS_VIDEO_WIDTH](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga12f4f516e8a103c43cf1fd3409e3a076) | The resolution's width       |
| [NET_STATUS_VIDEO_HEIGHT](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaccbc5e1a57b7575b7ecf812cb939002e) | The resolution's height      |
| [NET_STATUS_VIDEO_FPS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga2ceaa8d4f26f94231cceb46ebc1ec01f) | The current video frame rate        |
| [NET_STATUS_VIDEO_GOP](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gacd77aba1bb25077ecd03269c311479b8) | The current video GOP         |
| [NET_STATUS_VIDEO_BITRATE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa7190fc964cf23a567b56d9793ad5737) | The bitrate of the video data      |
| [NET_STATUS_AUDIO_BITRATE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae77d554c71c9e298e09ae39cde8ff698) | The bitrate of the audio data      |
| [NET_STATUS_NET_SPEED](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae2899ec3669bbf6261cead660c6e797c) | The network speed            |
| [NET_STATUS_AUDIO_CACHE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga71bf377ea1925873217c1c5ee600af53) | The number of audio frames            |
| [NET_STATUS_VIDEO_CACHE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga9e8fcc05e66967e0eb3348da202c7cde) | The number of video frames            |
| [NET_STATUS_AUDIO_INFO](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga4107d46355fbcb54973cdfb82f25a2f4) | The audio information of the current stream    |
| [NET_STATUS_NET_JITTER](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga04f0c226d2b7571d07f118e05f43dc3a) | The network jitter status        |
| [NET_STATUS_SERVER_IP](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga0d7111f8bfbb9aba0d2ea9e2c8d6d7bd) | The connected server IP |
| [NET_STATUS_VIDEO_DPS](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga1ef238d0f43788fa5a5e01ea3d1cfce7) | The current frame rate of the video output by the decoder  |
| [NET_STATUS_QUALITY_LEVEL](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga8f86732d6a56638c8697c20e614c8d68) | The network quality           |

### Player asset types

| Code | Event Definition | Description |
| ---- | ------------------------------------------------------------ | ------------------------- |
| 0    | [MEDIA_TYPE_AUTO](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#ga7d204fdc431c5c3ffea9f5da094edf5f) | The `auto` type                  |
| 1    | [MEDIA_TYPE_HLS_VOD](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gae915784aa6e5b694a599cb79bb5f6051) | The HLS VOD media asset for adaptive bitrate streaming |
| 2    | [MEDIA_TYPE_HLS_LIVE](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gacf7595f6e4617ad0da6e120ada7c7605) | The HLS live stream media asset for adaptive bitrate streaming |

### Uncategorized variables

| Code | Event Definition | Description |
| ---- | ------------------------------------------------------------ | ------------------- |
| -1   | [INDEX_AUTO](https://liteav.sdk.qcloud.com/doc/api/en/group__TXVodConstants__android.html#gaa49e56e7580286e85bce4c88feddb057) | The index for adaptive bitrate |
