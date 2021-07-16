__Feature__

Live stream publisher

__Overview__

`V2TXLivePusher` encodes local audio and video and publishes the encoded data to a specified URL. It supports any publishing server.
`V2TXLivePusher` has the following capabilities:

- Custom video capturing. You can customize audio and video data sources based on your project requirements.
- Retouching, filters, and stickers. `V2TXLivePusher` integrates multiple retouching algorithms (natural & smooth) and color space filters (custom filters are supported).
- QoS control technology. `V2TXLivePusher` can adapt automatically to different upstream network conditions by controlling audio/video traffic in real time based on the network conditions of hosts.
- Facial feature adjustment and animated widgets. Powered by YouTu’s AI face recognition technology, `V2TXLivePusher` supports animated widgets and fine-tuning of facial features, such as eye enlarging, face slimming, and nose reshaping. You need to purchase a **YouTu license** to use these live streaming effects.

## Basic SDK APIs
### initWithLiveMode


```
- (instancetype)initWithLiveMode:(V2TXLiveMode)liveMode;
```

#### Parameters 

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|


***

### setObserver

*        By setting the callback, you can listen to some callback events of TXLivePusherV2, including the pusher status, volume callback, statistics, warnings, and error messages.

```
- (void)setObserver:(id<V2TXLivePusherObserver>)observer;
```

#### Parameters 

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| observer | V2TXLivePusherObserver | Target object for the publisher’s callbacks. For more information, please see [V2TXLivePusherObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html). |

***

## Basic Publishing APIs
### setRenderView

This API is used to set the view for local camera preview. Images collected by the local camera are displayed on the view passed in after retouching, facial feature adjustments, and filter application.
```
- (V2TXLiveCode)setRenderView:(TXView *)view;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| view | TextureView | View for local camera preview |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### startPush

This API is used to start publishing audio/video data.
```
- (V2TXLiveCode)startPush:(NSString *)url;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| url |  String | URL to which data is published. Any publishing server is supported. |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: failed to publish streams because the URL is invalid.
- `V2TXLIVE_ERROR_REFUSED`: you cannot use the same stream ID for push and pull on the same device.

***

### stopPush

This API is used to stop publishing audio/video data.
```
- (V2TXLiveCode)stopPush;
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### isPushing

This API is used to get whether the publisher is publishing streams.
```
- (int)isPushing;
```

#### Response

Whether streams are being published
- `1`: yes
- `0`: no

***

### startScreenCapture
This API is used to start screen sharing.

*       iOS Broadcast Upload Extension must be used to enable video capture.
 

```
- (V2TXLiveCode)startScreenCapture:(NSString *)appGroup;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
* @param appGroup The `Application Group Identifier` shared by the main application and Broadcast, which can be set to nil, but setting it as instructed in the documentation will make the feature more reliable.

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### stopScreenCapture
This API is used to stop screen sharing.
```
- (V2TXLiveCode)stopScreenCapture;
```
#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

## Video APIs
### setVideoQuality
This API is used to set the resolution and orientation (portrait/landscape) of published video.
```
- (V2TXLiveCode)setVideoQuality:(V2TXLiveVideoResolution)resolution
                 resolutionMode:(V2TXLiveVideoResolutionMode)resolutionMode;
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|

| resolutionMode | [V2TXLiveVideoResolutionMode](#V2TXLiveVideoResolutionMode) | Orientation (portrait/landscape) |

#### `V2TXLiveVideoResolution` enumerated values

| Value | Description |
|---------|---------|
| V2TXLiveVideoResolution160x160 | Resolution: 160 x 160; bitrate: 100-150 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution270x270 | Resolution: 270 x 270; bitrate: 200-300 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution480x480 | Resolution: 480 x 480; bitrate: 350-525 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution320x240 | Resolution: 320 x 240; bitrate: 250-375 Kbps; frame rate: 15 FPS|
| V2TXLiveVideoResolution480x360 | Resolution: 480 x 360; bitrate: 400-600 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution640x480 | Resolution: 640 x 480; bitrate: 600-900 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution320x180 | Resolution: 320 x 180: bitrate: 250-400 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution480x270 | Resolution: 480 x 270; bitrate: 350-550 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution640x360 | Resolution: 640 x 360; bitrate: 500-900 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution960x540 | Resolution: 960 x 540; bitrate: 800-1500 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution1280x720 | Resolution: 1280 x 720; bitrate: 1000-1800 Kbps; frame rate: 15 FPS |
| V2TXLiveVideoResolution1920x1080 | Resolution: 1920 x 1080; bitrate: 2500-3000 Kbps; frame rate: 15 FPS |

#### `V2TXLiveVideoResolutionMode` enumerated values

| Value | Description |
|---------|---------|
| V2TXLiveVideoResolutionModeLandscape | Resolution in the landscape mode: V2TXLiveVideoResolution640_360 + V2TXLiveVideoResolutionModeLandscape = 640 x 360 |
| V2TXLiveVideoResolutionModePortrait | Resolution in the portrait mode: V2TXLiveVideoResolution640_360 + V2TXLiveVideoResolutionModePortrait = 360 x 640 |

***

### setRenderRotation

This API is used to set the rotation of local camera preview.
```
- (V2TXLiveCode)setRenderRotation:(V2TXLiveRotation)rotation;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| rotation | [V2TXLiveRotation](#V2TXLiveRotation) | Degrees by which the image is rotated. Default value: `V2TXLiveRotation0` |

#### Response
V2TXLiveCode:
- `V2TXLIVE_OK`: successful


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
- (V2TXLiveCode)setRenderMirror:(V2TXLiveMirrorType)mirrorType;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| mirrorType | [V2TXLiveMirrorType](#V2TXLiveMirrorType) | Mirror mode of the camera. Default value: `V2TXLiveMirrorTypeAuto` |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

#### `V2TXLiveMirrorType` enumerated values

#### `V2TXLiveMirrorType` enumerated values

| Value | Description |
|---------|---------|
| V2TXLiveMirrorTypeAuto | The default value. In this mode, the front camera is mirrored, but the rear camera is not. |
| V2TXLiveMirrorTypeEnable | Both the front and rear cameras are mirrored. |
| V2TXLiveMirrorTypeDisable | Neither the front nor rear camera is mirrored. |

***

### startCamera

This API is used to turn on the local camera.
```
- (V2TXLiveCode)startCamera:(BOOL)frontCamera;
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### stopCamera

This API is used to turn off the local camera.
```
- (V2TXLiveCode)stopCamera;
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### snapshot

This API is used to take a screenshot of the local video while it is being published.

>? After `V2TXLIVE_OK` is returned, you can get the screenshot taken in the `V2TXLivePusherObserver.onSnapshotComplete` callback.

```
- (V2TXLiveCode)snapshot;
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_REFUSED`: failed to take a screenshot because publishing has stopped

***

### setWatermark
This API is used to set a watermark for the publisher. Watermarks are disabled by default.
```
- (V2TXLiveCode)setWatermark:(TXImage *)image x:(float)x y:(float)y scale:(float)scale;
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| image | Bitmap | Watermark image. If this parameter is `null`, it means watermarks are disabled. |
| x | float | Horizontal coordinate of the watermark |
| y | float | Vertical coordinate of the watermark |
| scale | float | The ratio by which the watermark image is resized |

***

### setEncoderMirror
This API is used to set the mirror mode of encoded images.
```
- (V2TXLiveCode)setEncoderMirror:(BOOL)mirror;
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|


***

### enableCustomVideoCapture

This API is used to enable/disable custom video capturing. In the custom video capturing mode, the SDK stops capturing images from the camera, but continues to encode and send images.
```
- (V2TXLiveCode)enableCustomVideoCapture:(BOOL)enable;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| enable | BOOL | Whether to enable small image encoding. Default value: NO. |

***

### sendCustomVideoFrame
This API is used to send the custom video data captured to the SDK.
```
- (V2TXLiveCode)sendCustomVideoFrame:(V2TXLiveVideoFrame *)videoFrame;
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| videoFrame | V2TXLiveVideoFrame | Video frame sent to the SDK |

#### Response
V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `TXLIVE_ERROR_INVALID_PARAMETER`: failed to send the video frame because it is invalid.
- `V2TXLIVE_ERROR_REFUSED`: failed to send the video frame. You must call `enableCustomVideoCapture` to enable custom video capturing first.

***

### enableCustomVideoProcess
This API is used to enable/disable custom video processing.
```
- (V2TXLiveCode)enableCustomVideoProcess:(BOOL)enable pixelFormat:(V2TXLivePixelFormat)pixelFormat bufferType:(V2TXLiveBufferType)bufferType;
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|

| pixelFormat | [V2TXLivePixelFormat](#V2TXLivePixelFormat) | Pixel format of video frames |
| bufferType | [V2TXLiveBufferType](#V2TXLiveBufferType) | Video data buffer type |

#### `V2TXLivePixelFormat` enumerated values
#### `V2TXLivePixelFormat` enumerated values
| Value | Description |
|---------|---------|
|  V2TXLivePixelFormatUnknown | Unknown |
|  V2TXLivePixelFormatI420|  YUV420P/I420 |
|  V2TXLivePixelFormatTexture2D | OpenGL 2D texture |

#### `V2TXLiveBufferType` enumerated values
#### `V2TXLiveBufferType` enumerated values
| Value | Description |
|---------|---------|
| V2TXLiveBufferTypeUnknown | Unknown |
| V2TXLiveBufferTypeByteBuffer| `DirectBuffer`, which carries buffers in the format of I420 and others and is used at the native layer. |
|  V2TXLiveBufferTypeByteArray| `byte[]`, which carries buffers in the format of I420 and others and is used at the Java layer. |
|  V2TXLiveBufferTypeTexture| Direct operation texture ID. This buffer type delivers the best performance and has the smallest impact on video quality. |

***

## Beauty Filter APIs
### getBeautyManager
This API is used to get the beauty filter management object [TXBeautyManager](https://intl.cloud.tencent.com/zh/document/product/1071/38569).
You can do the following using `TXBeautyManager`:

- Set beauty effects such as the beauty filter style, skin whitening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening or shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
- Adjust the hairline, eye spacing, eye corners, mouth shape, nose wings, nose position, lip thickness, and face shape.
- Set animated effects such as face widgets (materials).
- Add makeup effects.
- Recognize gestures.

```
- (TXBeautyManager *)getBeautyManager
```

***

## Audio APIs
### startMicrophone

This API is used to turn on the mic.
```
- (V2TXLiveCode)startMicrophone;
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***
### stopMicrophone

This API is used turn off the mic.
```
- (V2TXLiveCode)stopMicrophone;
```
#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### setAudioQuality

This API is used to set audio quality.
```
- (V2TXLiveCode)setAudioQuality:(V2TXLiveAudioQuality)quality;
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
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_REFUSED`: you cannot change audio quality settings when streams are being published.
***

### enableVolumeEvaluation

This API is used to enable the volume reminder.
>? After enabling the volume reminder, you can get the volume measured by the SDK in the `V2TXLivePusherObserver#onMicrophoneVolumeUpdate(int)` callback.
```
- (V2TXLiveCode)enableVolumeEvaluation:(NSUInteger)intervalMs;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| intervalMs | int | Interval (ms) for volume callbacks. The minimum interval allowed is 100 ms. If the value is `0` (default) or smaller, the callback is disabled. `300` is recommended.

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

## Audio Effect APIs
### getAudioEffectManager


This API is used to get the audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html).
You can do the following using `TXAudioEffectManager`:

- Set the volume of audio captured by the mic
- Set reverb and voice changing effects
- Enable in-ear monitoring and set its volume
- Add background music and specify how to play it

```
- (TXAudioEffectManager *)getAudioEffectManager;
```

***

## Device Management APIs
### getDeviceManager

This API is used to get the device management object [TXDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__android.html).
You can do the following using `TXDeviceManager`:

- Switch between the front and rear cameras
- Enable autofocus
- Set camera zoom level
- Enable/Disable flashlight

```
- (TXDeviceManager *)getDeviceManager;
```

***
## Other APIs
### setProperty

This API is used to call the advanced APIs of `V2TXLivePusher`.
```
- (V2TXLiveCode)setProperty:(NSString *)key value:(NSObject *)value;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| key | String | Key of the advanced API to call |
| value | Object | Parameters required by the advanced API |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: failed because `key` is empty.

***

### setMixTranscodingConfig
This API is used to set On-Cloud MixTranscoding parameters. If you have enabled relayed push on the **Function Configuration** page of the [TRTC console](https://intl.cloud.tencent.com/register/), then each channel of image will have a default [CDN live streaming address](https://intl.cloud.tencent.com/document/product/647/35242). There may be multiple hosts in a room, each sending their own video and audio, but CDN audience needs only one live stream. Therefore, you need to mix multiple audio/video streams into one standard live stream, which requires MixTranscoding.
```
- (V2TXLiveCode)setMixTranscodingConfig:(V2TXLiveTranscodingConfig *)config;
```
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|


#### V2TXLiveTranscodingConfig 
| Value | Description |
|---------|---------|
| V2TXLiveBufferTypeUnknown | Unknown |
| V2TXLiveBufferTypeByteBuffer| `DirectBuffer`, which carries buffers in the format of I420 and others and is used at the native layer. |
|  V2TXLiveBufferTypeByteArray| `byte[]`, which carries buffers in the format of I420 and others and is used at the Java layer. |
|  V2TXLiveBufferTypeTexture| Direct operation texture ID. This buffer type delivers the best performance and has the smallest impact on video quality. |

***

### showDebugView

This API is used to display the dashboard.
```
- (void)showDebugView:(BOOL)isShow;
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|

