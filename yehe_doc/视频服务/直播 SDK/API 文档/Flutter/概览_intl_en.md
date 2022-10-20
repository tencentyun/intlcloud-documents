## V2TXLivePlayer

### Video player

For details, see [V2TXLivePlayer](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/v2_tx_live_player-library.html).
The player pulls audio/video data from the specified live streaming URL and plays the data after decoding and local rendering.
The player has the following capabilities:
- Playing over protocols including RTMP, HTTP-FLV, TRTC, and WebRTC
- Taking screenshots of streamed video
- Delay adjustment. You can set the minimum and maximum cache time for auto adjustment by the player.
- Custom video processing. You can process live video based on your project requirements before rendering and playback.

### Basic SDK APIs

| API                          | Description           |
| -------------------- | ---------------- |
| [addListener](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/addListener.html) | Sets player callbacks. |


### Basic playback APIs  

| API                          | Description           |
| --------------- | --------------------------- |
| [setRenderViewID](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/setRenderViewID.html) | Sets the player’s rendering view (`ViewID`). |
| [startLivePlay](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/startLivePlay.html) | Since v10.7, `startPlay` has been replaced by `startLivePlay`, and you need to call `V2TXLivePremier#setLicence` to set the license to use the live playback feature (you only need to set the license once). Otherwise, playback will fail (black screen). You can use a live stream publishing license, UGSV license, or video playback license to activate the live playback feature. If you don’t have any of the licenses, you can [buy one](https://www.tencentcloud.com/document/product/1071/38546) or [apply for a trial license for free](https://console.tencentcloud.com/live/license) to use the feature. |
| [stopPlay](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/stopPlay.html) | Stops playback.      |
| [isPlaying](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/isPlaying.html) | Gets whether playback is ongoing.  |

### Video APIs

| API                          | Description                |
| --------------------- | -------------------------- |
| [setRenderRotation](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/setRenderRotation.html)     | Sets video rotation. |
| [setRenderFillMode](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/setRenderFillMode.html)     | Sets the fill mode. |
| [pauseVideo](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/pauseVideo.html) | Pauses the player’s video. |
| [resumeVideo](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/resumeVideo.html)     | Resumes the player’s video. |
| [snapshot](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/snapshot.html)  | Takes a screenshot of the played video. |

### Audio APIs

| API | Description |
| ---------------------- | ---------------------- |
| [pauseAudio](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/pauseAudio.html) | Pauses the player’s audio.   |
| [resumeAudio](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/resumeAudio.html) | Resumes the player’s audio.   |
| [setPlayoutVolume](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/setPlayoutVolume.html) |  Sets the volume. |
| [enableVolumeEvaluation](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/enableVolumeEvaluation.html) | Enables the volume reminder for playback. |

### Other APIs

| API | Description |
| ---------------------- | ---------------------- |
| [setCacheParams](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/setCacheParams.html) | Sets the minimum and maximum cache time (seconds) for auto adjustment by the player.   |
| [showDebugView](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer/showDebugView.html) | Sets whether to show the debug view of player status information.  |

## V2TXLivePlayerObserver
Player callbacks
### Basic SDK callback APIs

| API                                     | Description                                  |
| --------- | --------------- |
| [onError](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html)   | Callback for error. This callback is returned when the player encounters an error. |
| [onWarning](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html) | Callback for warning    |
| [onConnected](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html) | Callback for successfully connecting to the server    |

### Video callback APIs
| API                                     | Description                                  |
| --------- | --------------- |
| [onVideoPlaying](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html)   | Callback for video playback |
| [onVideoLoading](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html)   | Callback for loading video|
| [onVideoResolutionChanged](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html)   | Callback for change of player resolution|
| [onSnapshotComplete](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html) | Callback for a screenshot taken    |
| [onRenderVideoFrame](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html) | Callback for custom video rendering|

### Audio callback APIs
| API                                     | Description                                  |
| --------- | --------------- |
| [onAudioPlaying](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html)   | Callback for audio playback |
| [onAudioLoading](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html)   | Callback for loading audio|
| [onPlayoutVolumeUpdate](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html) | Callback of the player’s volume     |

### Statistics callback APIs
| API                                     | Description                                  |
| --------- | --------------- |
| [onStatisticsUpdate](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/V2TXLivePlayerListenerType.html)   | Callback of player statistics|

## V2TXLivePusher

### Stream publisher

For details, see [V2TXLivePusher](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html).

`V2TXLivePusher` encodes local audio/video and publishes the encoded data to a specified URL. It supports any publishing server.
It has the following capabilities:
- Custom video capturing. You can customize audio/video data sources based on your project requirements.
- Retouching, filters, and stickers. `V2TXLivePusher` integrates multiple retouching algorithms (natural & smooth) and color space filters (custom filters are supported).
- QoS control technology. `V2TXLivePusher` can adapt automatically to different upstream network conditions by controlling audio/video traffic in real time based on the network conditions of hosts.
- Facial feature adjustment and animated widgets. Powered by YouTu’s AI facial recognition technology, `V2TXLivePusher` supports animated widgets and fine-tuning of facial features, such as eye enlarging, face slimming, and nose reshaping. You need to purchase a **YouTu license** to use these live streaming effects.

### Basic SDK APIs

| API                          | Description           |
| ----------- | ---------------- |
| [addListener](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/addListener.html) | Sets publisher callbacks. |

### Basic publishing APIs

| API | Description |
| ------------------ | --------------- |
| [setRenderViewID](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setRenderViewID.html)      | Sets the rendering view for local camera preview. |
| [startPush](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/startPush.html)    | Starts publishing audio/video data.            |
| [stopPush](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/stopPush.html)     | Stops publishing audio/video data.            |
| [isPushing](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/isPushing.html)    | Gets whether publishing is ongoing.      |

### Video APIs

| API | Description |
| --------------- | --------------------------------------------------- |
| [setVideoQuality](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setVideoQuality.html) | Sets video encoding parameters for publishing. |
| [setRenderRotation](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setRenderRotation.html) | Sets video rotation for local camera preview.      |
| [setRenderMirror](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setRenderMirror.html) | Sets the mirror mode for local camera preview.     |
| [startCamera](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/startCamera.html)                     | Turns the local camera on.       |
| [stopCamera](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/stopCamera.html) | Turns the local camera off.       |
| [startVirtualCamera](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/startVirtualCamera.html) | Starts image publishing.                  |
| [stopVirtualCamera](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/startVirtualCamera.html)  | Stops image publishing.                  |
| [startScreenCapture](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/startScreenCapture.html) | Starts screen capturing.                  |
| [stopScreenCapture](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/stopScreenCapture.html)  | Stops screen capturing.                  |
| [snapshot](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/snapshot.html) | Takes a screenshot of the published video.   |
| [setWatermark](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setWatermark.html)                    | Sets watermarks for the publisher. Watermarking is disabled by default. |
| [setEncoderMirror](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setEncoderMirror.html) | Sets the mirror mode for encoded video.     |
|[enableCustomVideoCapture](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/enableCustomVideoCapture.html) | Enables/Disables custom video capturing. |
|[sendCustomVideoFrame](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/sendCustomVideoFrame.html) |  Sends the captured video data to the SDK in the custom video capturing mode.|
|[enableCustomVideoProcess](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/enableCustomVideoProcess.html) | Enables/Disables custom video processing. |
|[sendSeiMessage](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/sendSeiMessage.html) | Sends an SEI message. |

### Beauty filter APIs

| API | Description |
| --------------- | --------------- |
| [getBeautyManager](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/getBeautyManager.html) | Gets the beauty filter management object `TXBeautyManager`, which is used to set beauty filters. |

### Audio APIs

| API                          | Description           |
| --------------- | ---------------------- |
| [startMicrophone](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/startMicrophone.html) | Turns the mic on.     |
| [stopMicrophone](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/stopMicrophone.html) | Turns the mic off.     |
| [setAudioQuality](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setAudioQuality.html) | Sets the quality of published audio.     |
| [enableVolumeEvaluation](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/enableVolumeEvaluation.html) | Enables the volume reminder for capturing. |

### Audio effect APIs
| API                                             | Description                                                         |
| --------------- | ------------------ |
| [getAudioEffectManager](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/getAudioEffectManager.html) | Gets the audio effect management object. |

### Device management APIs
| API                                             | Description                                                         |
| --------------- | ------------------ |
| [getDeviceManager](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/getDeviceManager.html) | Gets the device management object. |

### Other APIs

| API                                             | Description                                                         |
| --------------- | ------------------------------------- |
| [setProperty](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setProperty.html) | Calls an advanced API of `V2TXLivePusher`. |
| [setMixTranscodingConfig](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setMixTranscodingConfig.html) | Sets On-Cloud MixTranscoding parameters.  |
| [showDebugView](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/showDebugView.html) | Sets whether to display the dashboard.   |


## V2TXLivePusherObserver

### Basic SDK callback APIs

| API | Description |
| --------------- | --------------- |
| [onError](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback for error. This callback is returned when the publisher encounters an error. |
| [onWarning](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback for warning    |

### Video callback APIs
| API | Description |
| --------------- | ---------------------------------- |
| [onPushStatusUpdate](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback of the publisher’s connection status     |
| [onSnapshotComplete](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback for a screenshot taken  |
| [onProcessVideoFrame](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback for custom video processing |
| [onGLContextDestroyed](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback for destroying the OpenGL context in the SDK |
| [onCaptureFirstVideoFrame](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback for capturing the first video frame |

### Audio callback APIs
| API | Description |
| --------------- | ---------------------------- |
| [onCaptureFirstAudioFrame](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback for capturing the first audio frame|
| [onMicrophoneVolumeUpdate](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback of mic capturing volume |

### Mixtranscoding callback APIs
| API                                             | Description                                                         |
| --------------- | ------------------------------ |
| [onSetMixTranscodingConfig](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback for setting On-Cloud MixTranscoding parameters |

### Statistics callback APIs
| API                                             | Description                                                         |
| --------------- | ------------------------ |
| [onStatisticsUpdate](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) | Callback of publisher statistics |
