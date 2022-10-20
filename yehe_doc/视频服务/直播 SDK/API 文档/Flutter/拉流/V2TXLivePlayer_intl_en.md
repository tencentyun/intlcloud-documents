
__Overview__

Tencent Cloud’s live stream player
The player pulls audio/video data from the specified live streaming URL and plays the data after decoding and local rendering.

__Features__

The player has the following capabilities:

- Playing over protocols including RTMP, HTTP-FLV, TRTC, and WebRTC
- Taking screenshots of streamed video
- Delay adjustment. You can set the minimum and maximum cache time for auto adjustment by the player.
- Custom video processing. You can process live video based on your project requirements before rendering and playback.


## Basic SDK APIs
### addListener

This API is used to set the callbacks of the player. After setting, you can listen for callback events of `V2TXLivePlayer`, including player status, playback volume, first audio/video frame, statistics, warning and error messages, etc.

```dart
  void addListener(V2TXLivePlayerObserver func)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| observer | V2TXLivePlayerObserver | The target object for the player’s callbacks. For details, see [V2TXLivePlayerObserver](https://www.tencentcloud.com/document/product/1071/41272). |


## Basic Playback APIs
### setRenderViewID

This API is used to set the rendering view to display video.
```dart
  Future<V2TXLiveCode> setRenderViewID(int viewID)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| viewID | int | The rendering view ID, which is returned by `V2TXLiveVideoWidget.onViewCreated`. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful


### startLivePlay

This API is used to start playing audio/video streams.
```dart
  Future<V2TXLiveCode> startLivePlay(String url)
```

>? Since v10.7, `startPlay` has been replaced by `startLivePlay`, and you need to call `V2TXLivePremier#setLicence` or `TXLiveBase#setLicence` to set the license to use the live playback feature (you only need to set the license once). Otherwise, playback will fail (black screen). You can use a live stream publishing license, UGSV license, or video playback license to activate the live playback feature. If you don’t have any of the licenses, you can [buy one](https://www.tencentcloud.com/document/product/1071/38546) or [apply for a trial license for free](https://console.tencentcloud.com/live/license) to use the feature.

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| url |  String | The playback URL, which supports RTMP, HTTP-FLV, TRTC, and WebRTC.|

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: Successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Operation failed because the URL is invalid.
- `V2TXLIVE_ERROR_REFUSED`: RTC does not support using the same stream ID for publishing and playback on the same device.


### stopPlay

This API is used to stop playing audio/video streams.
```dart
  Future<V2TXLiveCode> stopPlay()
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful


### isPlaying

This API is used to get whether the player is playing streams.
```dart
  Future<int> isPlaying()
```

#### Response

Whether streams are being played
- `1`: yes
- `0`: no


## Video APIs
### setRenderRotation

This API is used to set the rotation of images displayed by the player.
```dart
  Future<V2TXLiveCode> setRenderRotation(V2TXLiveRotation rotation)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| rotation | [V2TXLiveRotation](#V2TXLiveRotation) | The degrees by which images are rotated. Default value: 0. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful

[](id:V2TXLiveRotation)

#### `V2TXLiveRotation` enumerated values

| Value                             | Description               |
| ------------------- | --------------- |
| v2TXLiveRotation0 | No rotation |
| v2TXLiveRotation90 | Rotate 90 degrees clockwise |
| v2TXLiveRotation180 | Rotate 180 degrees clockwise |
| v2TXLiveRotation270 | Rotate 270 degrees clockwise |


### setRenderFillMode

This API is used to set the image fill mode.
```dart
  Future<V2TXLiveCode> setRenderFillMode(V2TXLiveFillMode mode) 
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| mode | [V2TXLiveFillMode](#V2TXLiveFillMode) | The image fill mode. Default value: `V2TXLiveFillModeFit`. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful

[](id:V2TXLiveFillMode)

#### `V2TXLiveFillMode` enumerated values

| Value                 | Description                                                         |
| -------------------- | ------------------------------------------------------------ |
| v2TXLiveFillModeFit | The image fits the screen without cropping. If the aspect ratio of the image and the screen do not match, there will be black bars. |
| v2TXLiveFillModeFill | The image fills the entire screen, without black bars. If the aspect ratio of the image and screen do not match, the parts of the image that don’t fit will be cropped. |


### pauseVideo

This API is used to pause playing video streams.
```dart
  Future<V2TXLiveCode> pauseVideo()
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful


### resumeVideo

This API is used to resume playing video streams.
```dart
  Future<V2TXLiveCode> resumeVideo()
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful

### snapshot

This API is used to take a screenshot of streamed video.

>? After `V2TXLIVE_OK` is returned, you can get the screenshot taken in the `V2TXLivePlayerObserver.onSnapshotComplete` callback.

```dart
  Future<V2TXLiveCode> snapshot()
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful
- `V2TXLIVE_ERROR_REFUSED`: Failed to take a screenshot because playback has stopped.

## Audio APIs
### pauseAudio

 This API is used to pause playing audio streams.
```dart
  Future<V2TXLiveCode> pauseAudio()
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful

### resumeAudio

 This API is used to resume playing audio streams.
```dart
  Future<V2TXLiveCode> resumeAudio()
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful

### setPlayoutVolume

This API is used to set the volume.
```dart
  Future<V2TXLiveCode> setPlayoutVolume(int volume) 
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | The volume. Value range: 0-100. Default value: `100`. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful

### enableVolumeEvaluation

This API is used to enable the volume reminder for playback.
>? After enabling the volume reminder, you can get the SDK’s volume evaluation through the `V2TXLivePlayerObserver.onPlayoutVolumeUpdate` callback.
```dart
  Future<V2TXLiveCode> enableVolumeEvaluation(int intervalMs)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| intervalMs | int | The interval (ms) for triggering the `onPlayoutVolumeUpdate` callback. The minimum interval allowed is 100 ms. If the value is `0` (default) or smaller, the callback is disabled. `300` is recommended.|

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: Successful

## Other APIs
### setCacheParams

This API is used to set the minimum and maximum cache time (seconds) for auto adjustment by the player.
```dart
  Future<V2TXLiveCode> setCacheParams(double minTime, double maxTime)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| minTime | double | The minimum cache time for auto adjustment by the player. The value must be greater than `0`. Default value: `1`. |
| maxTime | double | The maximum cache time for auto adjustment by the player. The value must be greater than `0`. Default value: `5`. |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: Successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Operation failed. `minTime` and `maxTime` must be greater than `0`.
- `V2TXLIVE_ERROR_REFUSED`: You cannot change the cache policy while streams are being played.

### showDebugView

This API is used to set whether to show the debug view for the player status information.
```dart
  Future<void> showDebugView(bool isShow)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| isShow | bool | Whether to show the debug view. Default value: `false`. |
