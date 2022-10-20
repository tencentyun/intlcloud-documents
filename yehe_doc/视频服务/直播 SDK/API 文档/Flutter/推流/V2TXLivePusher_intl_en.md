__Overview__

Tencent Cloud’s live stream publisher

__Features__

`V2TXLivePusher` encodes local audio/video and publishes the encoded data to a specified URL. It supports any publishing server.
It has the following capabilities:

- Custom video capturing. You can customize audio/video data sources based on your project requirements.
- Retouching, filters, and stickers. `V2TXLivePusher` integrates multiple retouching algorithms (natural & smooth) and color space filters (custom filters are supported).
- QoS control technology. `V2TXLivePusher` can adapt automatically to different upstream network conditions by controlling audio/video traffic in real time based on the network conditions of hosts.
- Facial feature adjustment and animated widgets. Powered by YouTu’s AI facial recognition technology, `V2TXLivePusher` supports animated widgets and fine-tuning of facial features, such as eye enlarging, face slimming, and nose reshaping. You need to purchase a **YouTu license** to use these live streaming effects.

## Basic SDK APIs
### initWithLiveMode
This API is used to initialize the publisher.

```dart
  V2TXLivePusher(V2TXLiveMode liveMode)
```

#### Parameters 

| Parameter | Type | Description |
|-----|-----|-----|
| liveMode | V2TXLiveMode | Publishing protocol: RTMP (default) or ROOM |

### addListener

This API is used to set the callbacks of the publisher. After the setting, you can listen for callback events of `V2TXLivePusher`, including publisher status, volume, statistics, warning and error messages, etc.

```dart
  void addListener(V2TXLivePusherObserver func)
```

#### Parameters 

| Parameter | Type | Description |
|-----|-----|-----|
| observer | V2TXLivePusherObserver | Target object for the publisher’s callbacks. For details, see [V2TXLivePusherObserver](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html). |


## Basic Publishing APIs
### setRenderViewID

This API is used to set the view for local camera preview. Images captured by the local camera are displayed on the view passed in after retouching, facial feature adjustments, and filter application.
```dart
  Future<V2TXLiveCode> setRenderViewID(int viewID) 
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| viewID | int | The view ID, which is returned by `V2TXLiveVideoWidget.onViewCreated(int viewID)`. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

### startPush

This API is used to start publishing audio/video data.
```dart
  Future<V2TXLiveCode> startPush(String url)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| url |  String | The URL to which data is published. Any publishing server is supported. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed because the URL is invalid.
- `V2TXLIVE_ERROR_REFUSED`: you cannot use the same stream ID for publishing and playback on the same device.

### stopPush

This API is used to stop publishing audio/video data.
```dart
  Future<V2TXLiveCode> stopPush()
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

### isPushing

This API is used to get whether the publisher is publishing streams.
```dart
  Future<V2TXLiveCode> isPushing()
```

#### Response

Whether streams are being played
- `1`: yes
- `0`: no

## Video APIs
### setVideoQuality
This API is used to set the video encoding parameters for publishing.
```dart
  Future<V2TXLiveCode> setVideoQuality(V2TXLiveVideoEncoderParam param)
```
#### Parameters

| Parameter | Type | Description |
| ---- | ----  | ----  |
| param | [V2TXLiveVideoEncoderParam](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_def/V2TXLiveVideoEncoderParam-class.html) | Video encoding parameters |


### setRenderRotation

This API is used to set the rotation of local camera preview.
```dart
  Future<V2TXLiveCode> setRenderRotation(V2TXLiveRotation rotation)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| rotation | [V2TXLiveRotation](#V2TXLiveRotation) | The degrees by which the image is rotated. Default value: `v2TXLiveRotation0`. |

#### Response
V2TXLiveCode:
`V2TXLIVE_OK`: successful

[](id:V2TXLiveRotation)
#### `V2TXLiveRotation` enumerated values

| Value | Description |
|---------|---------|
| v2TXLiveRotation0 | No rotation |
| v2TXLiveRotation90 | Rotate 90 degrees clockwise |
| v2TXLiveRotation180 | Rotate 180 degrees clockwise |
| v2TXLiveRotation270 | Rotate 270 degrees clockwise |

### setRenderMirror

This API is used to set the mirror mode of local camera preview.
```dart
  Future<V2TXLiveCode> setRenderMirror(V2TXLiveMirrorType mirrorType)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| mirrorType | [V2TXLiveMirrorType](#V2TXLiveMirrorType) | The mirror mode of the camera. Default value: `v2TXLiveMirrorTypeAuto`. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

[](id:V2TXLiveMirrorType)

#### `V2TXLiveMirrorType` enumerated values

| Value | Description |
|---------|---------|
| v2TXLiveMirrorTypeAuto | The default value. In this mode, the front camera is mirrored, but the rear camera is not. |
| v2TXLiveMirrorTypeEnable | Both the front and rear cameras are mirrored. |
| v2TXLiveMirrorTypeDisable | Neither the front nor rear camera is mirrored. |

### startCamera

This API is used to turn the local camera on.

>? The `startVirtualCamera`, `startCamera`, and `startScreenCapture` APIs are mutually exclusive when you use them with the same pusher instance. For example, if you call `startCamera` first and then call `startVirtualCamera`, the SDK will stop publishing camera data and publish an image instead.

```dart
  Future<V2TXLiveCode> startCamera(bool frontCamera)
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

### stopCamera

This API is used to turn the local camera off.
```dart
  Future<void> stopCamera() 
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful


### startVirtualCamera

This API is used to publish an image.

>? The `startVirtualCamera`, `startCamera`, and `startScreenCapture` APIs are mutually exclusive when you use them with the same pusher instance. For example, if you call `startCamera` first and then call `startVirtualCamera`, the SDK will stop publishing camera data and publish an image instead.

```dart
  Future<V2TXLiveCode> startVirtualCamera(String type, String imageUrl)
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

| Parameter | Type | Description |
|-----|-----|-----|
| type | String | Valid values: `network` (an image from the internet), `file` (a local image). |
| imageUrl | String | Image URL |

### stopVirtualCamera

This API is used to stop publishing images.

```dart
  Future<V2TXLiveCode> stopVirtualCamera()
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful


### startScreenCapture
This API is used to start screen recording.
>? 
>- To start screen recording on iOS, instead of using this API, you need to do the following.
>- The `startVirtualCamera`, `startCamera`, and `startScreenCapture` APIs are mutually exclusive when you use them with the same pusher instance. For example, if you call `startCamera` first and then call `startVirtualCamera`, the SDK will stop publishing camera data and publish an image instead.

1. First, use Broadcast Upload Extension to start screen recording.
2. Then, call `enableCustomVideoCapture` to enable custom capturing. 
3. At last, call `sendCustomVideoFrame` to send the screen images captured by Broadcast Upload Extension.

```dart
  Future<V2TXLiveCode> startScreenCapture(String appGroup)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| appGroup |  String | The App Group ID shared by the host app and Broadcast Upload Extension. You can set it to `nil`, but for better reliability, we recommend you set it as instructed in our documentation.|

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

### stopScreenCapture
This API is used to stop screen recording.
```dart
  Future<V2TXLiveCode> stopScreenCapture()
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

### snapshot

This API is used to take a screenshot of the local video while it is being published.

>? After `V2TXLIVE_OK` is returned, you can get the screenshot taken in the `V2TXLivePusherObserver.onSnapshotComplete` callback.

```dart
  Future<V2TXLiveCode> snapshot()
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_REFUSED`: failed to take a screenshot because publishing has stopped.

### setWatermark
This API is used to set a watermark for the publisher. Watermarking is disabled by default.
```dart
  Future<V2TXLiveCode> setWatermark(String type, String image, double x,
      double y, double scale)
```
#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| type | String | Valid values: `network` (an image from the internet), `file` (a local image). |
| image | String | Image URL |
| x | double | Watermark coordinate |
| y | double | Watermark coordinate |
| scale | double | Percentage by which the image is resized |

### setEncoderMirror
This API is used to set the mirror mode of encoded images.
```dart
  Future<V2TXLiveCode> setEncoderMirror(bool mirror)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| mirror | Boolean | Whether to mirror encoded images. Default value: `false`. |

### enableCustomVideoCapture

This API is used to enable/disable custom video capturing. In the custom video capturing mode, the SDK stops capturing images from the camera, but continues to encode and send images.
```dart
  Future<V2TXLiveCode> enableCustomVideoCapture(bool enable)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| enable | bool | Whether to enable custom video capturing. Default value: `false`. |

### sendCustomVideoFrame
This API is used to send the captured custom video data to the SDK.
```dart
  Future<V2TXLiveCode> sendCustomVideoFrame(V2TXLiveVideoFrame videoFrame)
```
#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| videoFrame | V2TXLiveVideoFrame | Video frames sent to the SDK |

#### Response
V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed because the video data is invalid.
- `V2TXLIVE_ERROR_REFUSED`: failed. You must call `enableCustomVideoCapture` to enable custom video capturing first.

### enableCustomVideoProcess
This API is used to enable/disable custom video processing.
```dart
  Future<V2TXLiveCode> enableCustomVideoProcess(bool enable,
      V2TXLivePixelFormat pixelFormat, V2TXLiveBufferType bufferType)
```
#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| enable | bool | Whether to enable custom video processing. Default value: `false`. |
| pixelFormat | V2TXLivePixelFormat | Pixel format of video frames |
| bufferType | V2TXLiveBufferType | Buffer type of video data |

[](id:V2TXLivePixelFormat)
#### `V2TXLivePixelFormat` enumerated values
| Value | Description |
|---------|---------|
|  v2TXLivePixelFormatUnknown | Unknown |
|  v2TXLivePixelFormatI420|  YUV420P (I420) |
|  v2TXLivePixelFormatTexture2D | OpenGL 2D texture |

[](id:V2TXLiveBufferType)
#### `V2TXLiveBufferType` enumerated values
| Value | Description |
|---------|---------|
| v2TXLiveBufferTypeUnknown | Unknown |
| v2TXLiveBufferTypeByteBuffer| Direct buffers. This type is for I420 and other buffers and is used at the native layer. |
|  v2TXLiveBufferTypeByteArray| Byte arrays. This type is for I420 and other buffers and is used at the Java layer. |
|  v2TXLiveBufferTypeTexture| Texture ID, which allows direct operation. It delivers the best performance and has the smallest impact on video quality. |


### sendSeiMessage
This API is used to send an SEI message. [V2TXLivePlayer](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/V2TXLivePlayer-class.html) can receive SEI messages via the `onReceiveSeiMessage` callback of [V2TXLivePlayerObserver](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/v2_tx_live_player_observer-library.html).
```dart
  Future<V2TXLiveCode> sendSeiMessage(int payloadType, Uint8List data)
```
#### Parameters
| Parameter | Type | Description |
|-----|-----|-----|
| payloadType | int | Data type. Valid values: `5`, `242` (recommended). |
| data | Uint8List | Data to be sent |

 #### Response
 V2TXLiveCode:
 `V2TXLIVE_OK`: successful

## Beauty Filter APIs
### getBeautyManager
This API is used to get the beauty filter manager [TXBeautyManager](https://pub.dev/documentation/live_flutter_plugin/latest/manager_tx_beauty_manager/manager_tx_beauty_manager-library.html).
You can do the following using the beauty filter manger:

- Set the beauty filter style and apply effects including skin brightening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening/shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
- Adjust the hairline, eye spacing, eye corners, lip shape, nose wings, nose position, lip thickness, and face shape.
- Apply animated effects such as face widgets (resources).
- Add makeup effects.
- Recognize gestures.

```dart
  TXBeautyManager getBeautyManager()
```

## Audio APIs
### startMicrophone

This API is used to turn the mic on.
```dart
  Future<V2TXLiveCode> startMicrophone()
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

### stopMicrophone

This API is used to turn the mic off.
```dart
  Future<V2TXLiveCode> stopMicrophone()
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful


### setAudioQuality

This API is used to set audio quality.
```dart
  Future<V2TXLiveCode> setAudioQuality(V2TXLiveAudioQuality quality)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| quality | V2TXLiveAudioQuality | Audio quality |

#### `V2TXLiveAudioQuality` enumerated values
| Value | Description |
|---------|---------|
|  v2TXLiveAudioQualitySpeech | Speech. Audio sample rate: 16 kHz; sound channel: mono; bitrate: 16 Kbps<br>This is designed for call scenarios such as online conferencing and audio calls. |
|  v2TXLiveAudioQualityDefault|  Default. Audio sample rate: 48 kHz; sound channel: mono; bitrate: 50 Kbps<br>This is the default audio quality of the SDK and is recommended. |
|  v2TXLiveAudioQualityMusic | Music. Audio sample rate: 48 kHz; sound channel: dual; bitrate: 128 Kbps<br>This is designed for music-oriented scenarios with hi-fi requirements, such as karaoke and live music streaming. |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_REFUSED`: you cannot change audio quality settings when streams are being published.

### enableVolumeEvaluation

This API is used to enable the volume reminder for audio capturing.
>? After enabling the volume reminder, you can get the volume measured by the SDK in the `V2TXLivePusherObserver.onMicrophoneVolumeUpdate` callback.

```dart
  Future<V2TXLiveCode> enableVolumeEvaluation(int intervalMs)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| intervalMs | int | Interval (ms) for volume callbacks. The minimum interval allowed is 100 ms. If the value is `0` (default) or smaller, the callback is disabled. `300` is recommended.

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

## Audio Effect APIs
### getAudioEffectManager


This API is used to get the audio effect manager [TXAudioEffectManager](https://pub.dev/documentation/live_flutter_plugin/latest/manager_tx_audio_effect_manager/manager_tx_audio_effect_manager-library.html).
You can do the following using `TXAudioEffectManager`:

- Set the volume of audio captured by the mic.
- Set reverb and voice changing effects.
- Enable in-ear monitoring and set its volume.
- Add background music and specify how to play it.

```dart
  TXAudioEffectManager getAudioEffectManager()
```

## Device Management APIs
### getDeviceManager

This API is used to get the device manager [TXDeviceManager](https://pub.dev/documentation/live_flutter_plugin/latest/manager_tx_device_manager/manager_tx_device_manager-library.html).
You can do the following using `TXDeviceManager`:

- Switch between the front and rear cameras.
- Enable autofocus.
- Set camera zoom level.
- Enable/Disable flashlight.

```dart
  TXDeviceManager getDeviceManager()
```

## Other APIs
### setProperty

This API is used to call the advanced APIs of `V2TXLivePusher`.
```dart
  Future<V2TXLiveCode> setProperty(String key, String value)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| key | String | Key of the advanced API to call |
| value | String | Parameters required by the advanced API |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed because `key` is empty.

### setMixTranscodingConfig
This API is used to set On-Cloud MixTranscoding parameters. If you have enabled relay to CDN on the **Function Configuration** page of the [TRTC console](https://intl.cloud.tencent.com/register/), each anchor will have a default [CDN address](https://intl.cloud.tencent.com/document/product/647/35242). There may be multiple anchors in a room, each sending their own video and audio, but the audience needs only one live stream. Therefore, you need to mix multiple audio/video streams into one standard live stream. This is MixTranscoding.
```dart
  Future<V2TXLiveCode> setMixTranscodingConfig(V2TXLiveTranscodingConfig? config)
```
#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| config | V2TXLiveTranscodingConfig | On-Cloud MixTranscoding configuration |

#### V2TXLiveTranscodingConfig 
| Value | Description |
|---------|---------|
| v2TXLiveBufferTypeUnknown | Unknown |
| v2TXLiveBufferTypeByteBuffer| Direct buffers. This type is for I420 and other buffers and is used at the native layer. |
|  v2TXLiveBufferTypeByteArray| Byte arrays. This type is for I420 and other buffers and is used at the Java layer. |
| v2TXLiveBufferTypeTexture| Texture ID, which allows direct operation. It delivers the best performance and has the smallest impact on video quality. |

### showDebugView

This API is used to set whether to display the dashboard.
```dart
  Future<V2TXLiveCode> showDebugView(bool isShow)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| isShow | bool | Whether to display the dashboard. Default value: `false`. |
