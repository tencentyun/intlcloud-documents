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

```
- (instancetype)initWithLiveMode:(V2TXLiveMode)liveMode
```

#### Parameters 

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| liveMode | V2TXLiveMode | Publishing protocol: RTMP (default) or ROOM |

***

### setObserver

This API is used to set the callbacks of the publisher. After the setting, you can listen for callback events of `V2TXLivePusher`, including publisher status, volume, statistics, warning and error messages, etc.

```
- (void)setObserver:(id<V2TXLivePusherObserver>)observer
```

#### Parameters 

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| observer | V2TXLivePusherObserver | Target object for the publisher’s callbacks. For more information, please see [V2TXLivePusherObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html). |

***

## Basic Publishing APIs
### setRenderView

This API is used to set the view for local camera preview. Images captured by the local camera are displayed on the view passed in after retouching, facial feature adjustments, and filter application.
```
- (V2TXLiveCode)setRenderView:(TXView *)view
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| view | TXView * | View for local camera preview |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### startPush

This API is used to start publishing audio/video data.
```
- (V2TXLiveCode)startPush:(NSString *)url
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| url |  NSString * | Publishing URL. Any publishing server is supported. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed because the URL is invalid.
- `V2TXLIVE_ERROR_REFUSED`: RTC does not support using the same stream ID for publishing and playback on the same device.

***

### stopPush

This API is used to stop publishing audio/video data.
```
- (V2TXLiveCode)stopPush
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### isPushing

This API is used to get whether the publisher is publishing streams.
```
- (int)isPushing
```

#### Response

Whether streams are being played
- `1`: yes
- `0`: no

***


## Video APIs
### setVideoQuality
// Set video encoding parameters for publishing
```
- (V2TXLiveCode)setVideoQuality:(V2TXLiveVideoEncoderParam *)param;
```
#### Parameters

| Parameter | Type | Description |
| ---- | ----  | ----  |
| param | [V2TXLiveVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveDef__ios.html#interfaceV2TXLiveVideoEncoderParam) | Video encoding parameters |


***

### setRenderRotation

This API is used to set the rotation of local camera preview.
```
- (V2TXLiveCode)setRenderRotation:(V2TXLiveRotation)rotation
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| rotation | [V2TXLiveRotation](#V2TXLiveRotation) | Degrees by which the image is rotated. Default value: `V2TXLiveRotation0` |

#### Response
V2TXLiveCode:
`V2TXLIVE_OK`: successful

[](id:V2TXLiveRotation)
#### `V2TXLiveRotation` enumerated values

| Value | Description |
|---------|---------|
| V2TXLiveRotation0 | No rotation |
| V2TXLiveRotation90 | Rotate 90 degrees clockwise |
| V2TXLiveRotation180 | Rotate 180 degrees clockwise |
| V2TXLiveRotation270 | Rotate 270 degrees clockwise |

***

### setRenderMirror

This API is used to set the mirror mode of local camera preview.
```
- (V2TXLiveCode)setRenderMirror:(V2TXLiveMirrorType)mirrorType
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| mirrorType | [V2TXLiveMirrorType](#V2TXLiveMirrorType) | Mirror mode of the camera. Default value: `V2TXLiveMirrorTypeAuto` |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

[](id:V2TXLiveMirrorType)

#### `V2TXLiveMirrorType` enumerated values

| Value | Description |
|---------|---------|
| V2TXLiveMirrorTypeAuto | The default value. In this mode, the front camera is mirrored, but the rear camera is not. |
| V2TXLiveMirrorTypeEnable | Both the front and rear cameras are mirrored. |
| V2TXLiveMirrorTypeDisable | Neither the front nor rear camera is mirrored. |

***

### startCamera

This API is used to turn the local camera on.

>? Among `startVirtualCamera`, `startCamera`, and `startScreenCapture`, only one can be used to publish data under the same pusher instance. If, for example, `startCamera` is called first and then `startVirtualCamera`, the SDK will pause the publishing of camera data and start image publishing.

```
- (V2TXLiveCode)startCamera:(BOOL)frontCamera
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### stopCamera

This API is used to turn the local camera off.
```
- (V2TXLiveCode)stopCamera
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***
### startVirtualCamera

This API is used to start image publishing.

>? Among `startVirtualCamera`, `startCamera`, and `startScreenCapture`, only one can be used to publish data under the same pusher instance. If, for example, `startCamera` is called first and then `startVirtualCamera`, the SDK will pause the publishing of camera data and start image publishing.

```
- (V2TXLiveCode)startVirtualCamera:(TXImage *)image
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### stopVirtualCamera

This API is used to stop image publishing.

```
- (V2TXLiveCode)stopVirtualCamera
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### startScreenCapture
This API is used to start screen recording.
>? 
>- To start screen recording on iOS, instead of using this API, you need to do the following.
>- Among `startVirtualCamera`, `startCamera`, and `startScreenCapture`, only one can be used to publish data under the same pusher instance. If, for example, `startCamera` is called first and then `startVirtualCamera`, the SDK will pause the publishing of camera data and start image publishing.

1. First, use Broadcast Upload Extension to start screen recording.
2. Then, call `enableCustomVideoCapture` to enable custom capturing. 
3. At last, call `sendCustomVideoFrame` to send the screen images captured by Broadcast Upload Extension.

```
- (V2TXLiveCode)startScreenCapture:(NSString *)appGroup
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| appGroup |  NSString * | The App Group ID shared by the host app and Broadcast Upload Extension. It can be set to `nil`, but setting it as instructed in our documentation will make the feature more reliable.|

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### stopScreenCapture
This API is used to stop screen recording.
```
- (V2TXLiveCode)stopScreenCapture
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### snapshot

This API is used to take a screenshot of the local video while it is being published.

>? After `V2TXLIVE_OK` is returned, you can get the screenshot taken in the `V2TXLivePusherObserver#onSnapshotComplete:(TXImage *)image` callback.

```
- (V2TXLiveCode)snapshot
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_REFUSED`: failed to take a screenshot because publishing has stopped.

***

### setWatermark
This API is used to set a watermark for the publisher. Watermarking is disabled by default.
```
- (V2TXLiveCode)setWatermark:(TXImage *)image x:(float)x y:(float)y scale:(float)scale
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| image | TXImage * | Watermark image. If this parameter is `null`, it means watermarking is disabled. |
| x | float | Horizontal coordinate of the watermark |
| y | float | Vertical coordinate of the watermark |
| scale | float | Scale ratio of the watermark image |

***

### setEncoderMirror
This API is used to set the mirror mode of encoded images.
```
- (V2TXLiveCode)setEncoderMirror:(BOOL)mirror
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| mirror | BOOL | Whether to mirror encoded images. Default value: `NO` |

***

### enableCustomVideoCapture

This API is used to enable/disable custom video capturing. In the custom video capturing mode, the SDK stops capturing images from the camera, but continues to encode and send images.
```
- (V2TXLiveCode)enableCustomVideoCapture:(BOOL)enable
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| enable | BOOL | Whether to enable custom capturing. Default value: `NO` |

***

### sendCustomVideoFrame
This API is used to send the custom video data captured to the SDK.
```
- (V2TXLiveCode)sendCustomVideoFrame:(V2TXLiveVideoFrame *)videoFrame
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| videoFrame | V2TXLiveVideoFrame * | Video frames sent to the SDK |

#### Response
V2TXLiveCode:
`V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed because the video data is invalid.
- `V2TXLIVE_ERROR_REFUSED`: failed. You must call `enableCustomVideoCapture` to enable custom video capturing first.

***

### enableCustomVideoProcess
This API is used to enable/disable custom video processing.
```
- (V2TXLiveCode)enableCustomVideoProcess:(BOOL)enable pixelFormat:(V2TXLivePixelFormat)pixelFormat bufferType:(V2TXLiveBufferType)bufferType
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| enable | BOOL | Whether to enable custom video processing. Default value: `NO` |
| pixelFormat | V2TXLivePixelFormat | Pixel format of video frames |
| bufferType | V2TXLiveBufferType | Buffer type of video data |

[](id:V2TXLivePixelFormat)
#### `V2TXLivePixelFormat` enumerated values
| Value | Description |
|---------|---------|
|  V2TXLivePixelFormatUnknown | Unknown |
|  V2TXLivePixelFormatI420|  YUV420P (I420) |
|  V2TXLivePixelFormatTexture2D | OpenGL 2D texture |

[](id:V2TXLiveBufferType)
#### `V2TXLiveBufferType` enumerated values
| Value | Description |
|---------|---------|
| V2TXLiveBufferTypeUnknown | Unknown |
| V2TXLiveBufferTypeByteBuffer| `DirectBuffer`, which carries buffers in the format of I420 and others and is used at the native layer. |
|  V2TXLiveBufferTypeByteArray| `byte[]`, which carries buffers in the format of I420 and others and is used at the Java layer. |
|  V2TXLiveBufferTypeTexture| Texture ID, which allows direct operation. It delivers the best performance and has the smallest impact on video quality. |

***

## Beauty Filter APIs
### getBeautyManager
This API is used to get the beauty filter management object [TXBeautyManager](https://intl.cloud.tencent.com/document/product/1071/41671).
You can do the following using `TXBeautyManager`:

- Set the beauty filter style and apply effects including skin brightening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening/shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
- Adjust the hairline, eye spacing, eye corners, lip shape, nose wings, nose position, lip thickness, and face shape.
- Apply animated effects such as face widgets (materials).
- Add makeup effects.
- Recognize gestures.

```
- (TXBeautyManager *)getBeautyManager
```

***

## Audio APIs
### startMicrophone

This API is used to turn the mic on.
```
- (V2TXLiveCode)startMicrophone
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***
### stopMicrophone

This API is used to turn the mic off.
```
- (V2TXLiveCode)stopMicrophone
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### setAudioQuality

This API is used to set audio quality.
```
- (V2TXLiveCode)setAudioQuality:(V2TXLiveAudioQuality)quality
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| quality | V2TXLiveAudioQuality | Audio quality |

#### `V2TXLiveAudioQuality` enumerated values
| Value | Description |
|---------|---------|
|  V2TXLiveAudioQualitySpeech | Speech. Audio sample rate: 16 kHz; sound channel: mono; bitrate: 16 Kbps<br>This is designed for speech-based call scenarios such as online conferencing and audio call. |
|  V2TXLiveAudioQualityDefault|  Default. Audio sample rate: 48 kHz; sound channel: mono; bitrate: 50 Kbps<br>This is the default audio quality of the SDK and is recommended. |
|  V2TXLiveAudioQualityMusic | Music. Audio sample rate: 48 kHz; sound channel: dual; bitrate: 128 Kbps<br>This is designed for music-oriented scenarios with hi-fi requirements, such as karaoke and live music streaming. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_REFUSED`: you cannot change audio quality settings when streams are being published.
***

### enableVolumeEvaluation

This API is used to enable the volume reminder for audio capturing.
>? After enabling the volume reminder, you can get the SDK’s volume evaluation through the `V2TXLivePusherObserver#onMicrophoneVolumeUpdate:(NSInteger)volume` callback.

```
- (V2TXLiveCode)enableVolumeEvaluation:(NSInteger)intervalMs;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| intervalMs | NSInteger | Interval (ms) for triggering the `onMicrophoneVolumeUpdate` callback. The minimum interval allowed is 100 ms. If the value is `0` (default) or smaller, the callback is disabled. `300` is recommended. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

## Audio Effect APIs
### getAudioEffectManager


This API is used to get the audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__ios.html).
You can do the following using `TXAudioEffectManager`:

- Set the volume of audio captured by the mic.
- Set reverb and voice changing effects.
- Enable in-ear monitoring and set its volume.
- Add background music and specify how to play it.

```
- (TXAudioEffectManager *)getAudioEffectManager
```

***

## Device Management APIs
### getDeviceManager

This API is used to get the device management object [TXDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__ios.html).
You can do the following using `TXDeviceManager`:

- Switch between the front and rear cameras.
- Enable autofocus.
- Set camera zoom level.
- Enable/Disable flashlight.

```
- (TXDeviceManager *)getDeviceManager;
```

***
## Other APIs
### setProperty

This API is used to call the advanced APIs of `V2TXLivePusher`.
```
- (V2TXLiveCode)setProperty:(NSString *)key value:(NSObject *)value
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| key | NSString * | Key of the advanced API to call |
| value | NSObject * | Parameters required by the advanced API |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed because `key` is empty.

***

### setMixTranscodingConfig
This API is used to set On-Cloud MixTranscoding parameters. If you have enabled relayed push on the **Function Configuration** page of the [TRTC console](https://intl.cloud.tencent.com/register/), then each channel of image will have a default [CDN live streaming address](https://intl.cloud.tencent.com/document/product/647/35242). There may be multiple hosts in a room, each sending their own video and audio, but CDN audience needs only one live stream. Therefore, you need to mix multiple audio/video streams into one standard live stream, which requires MixTranscoding.
```
- (V2TXLiveCode)setMixTranscodingConfig:(V2TXLiveTranscodingConfig *)config
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| config | V2TXLiveTranscodingConfig * | On-Cloud MixTranscoding configuration |

#### V2TXLiveTranscodingConfig 
| Value | Description |
|---------|---------|
| V2TXLiveBufferTypeUnknown | Unknown |
| V2TXLiveBufferTypeByteBuffer| `DirectBuffer`, which carries buffers in the format of I420 and others and is used at the native layer. |
|  V2TXLiveBufferTypeByteArray| `byte[]`, which carries buffers in the format of I420 and others and is used at the Java layer. |
|  V2TXLiveBufferTypeTexture| Texture ID, which allows direct operation. It delivers the best performance and has the smallest impact on video quality. |

***

### showDebugView

This API is used to set whether to display the dashboard.
```
- (void)showDebugView:(BOOL)isShow
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| isShow | BOOL | Whether to show the debug view. Default value: `NO` |
