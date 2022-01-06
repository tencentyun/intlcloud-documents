
### Overview

Tencent Cloud’s live stream player
The player pulls audio/video data from the specified live streaming URL and plays the data after decoding and local rendering.

### Features

The player has the following capabilities:

- Playing over protocols including RTMP, HTTP-FLV, TRTC, and WebRTC
- Taking screenshots of streamed video
- Delay adjustment. You can set the minimum and maximum cache time for auto adjustment by the player.
- Custom video processing. You can process live video based on your project requirements before rendering and playback.


## Basic SDK APIs
### setObserver

This API is used to set the callbacks of the player. After setting, you can listen for callback events of `V2TXLivePlayer`, including player status, playback volume, first audio/video frame, statistics, warning and error messages, etc.

```
public abstract void setObserver(V2TXLivePlayerObserver observer);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| observer | V2TXLivePlayerObserver | Target object for the player’s callbacks. For details, please see [V2TXLivePlayerObserver](https://intl.cloud.tencent.com/zh/document/product/454/56049). |

***

## Basic Playback APIs
### setRenderView

This API is used to set the rendering view to display video.
```
public abstract int setRenderView(TXCloudVideoView view);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| view | TXCloudVideoView | The player’s rendering view |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### setRenderView

This API is used to set the rendering view to display video.
```
public abstract int setRenderView(SurfaceView view);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| view | SurfaceView | The player’s rendering view |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### setRenderView

This API is used to set the rendering view to display video.
```
public abstract int setRenderView(TextureView view);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| view | TextureView | The player’s rendering view |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### startPlay

This API is used to start playing audio/video streams.
```
public abstract int startPlay(String url);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| url |  String | Playback URL of audio/video streams, which supports RTMP, HTTP-FLV, TRTC, and WebRTC |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed because the URL is invalid.
- `V2TXLIVE_ERROR_REFUSED`: RTC does not support using the same stream ID for publishing and playback on the same device.

***

### stopPlay

This API is used to stop playing audio/video streams.
```
public abstract int stopPlay();
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### isPlaying

This API is used to get whether the player is playing streams.
```
public abstract int isPlaying();
```

#### Response

Whether streams are being played
- `1`: yes
- `0`: no

***

## Video APIs
### setRenderRotation

This API is used to set the rotation of images displayed by the player.
```
public abstract int setRenderRotation(V2TXLiveRotation rotation);
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

### setRenderFillMode

This API is used to set the image fill mode.
```
public abstract int setRenderFillMode(V2TXLiveFillMode mode);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| mode | [V2TXLiveFillMode](#V2TXLiveFillMode) | Image fill mode. Default value: `V2TXLiveFillModeFit` |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

[](id:V2TXLiveFillMode)
#### `V2TXLiveFillMode` enumerated values

| Value | Description |
|---------|---------|
| V2TXLiveFillModeFit | The image fits the screen without cropping. If the aspect ratio of the image and the screen do not match, there will be black bars. |
| V2TXLiveFillModeFill | The image fills the entire screen, without black bars. If the aspect ratio of the image and screen do not match, the parts of the image that don’t fit will be cropped. |

***

### pauseVideo

This API is used to pause playing video streams.
```
public abstract int pauseVideo();
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***


### resumeVideo

This API is used to resume playing video streams.
```
public abstract int resumeVideo();
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### snapshot

This API is used to take a screenshot of streamed video.

>? After `V2TXLIVE_OK` is returned, you can get the screenshot taken in the `V2TXLivePlayerObserver.onSnapshotComplete` callback.

```
public abstract int snapshot();
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_REFUSED`: failed to take a screenshot because playback has stopped.

***

### enableCustomRendering

This API is used to set custom video rendering. You can use this API to obtain each frame of decoded video for custom rendering.
>? After custom rendering is enabled, you can get video frames in the `V2TXLivePlayerObserver.onRenderVideoFrame` callback.
```
public abstract int enableCustomRendering(
        boolean enable,
        V2TXLivePixelFormat pixelFormat, 
        V2TXLiveBufferType bufferType);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| enable | Boolean | Whether to enable custom rendering. Default value: `false` |
| pixelFormat | [V2TXLivePixelFormat](#V2TXLivePixelFormat) | Pixel format of the video called back for custom rendering |
| bufferType | [V2TXLiveBufferType](#V2TXLiveBufferType) | Buffer type of the video called back for custom rendering |

#### Response
V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_NOT_SUPPORTED`: unsupported pixel format or data format.

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

## Audio APIs
### pauseAudio

 This API is used to pause playing audio streams.
```
public abstract int pauseAudio();
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***
### resumeAudio

 This API is used to resume playing audio streams.
```
public abstract int resumeAudio();
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### setPlayoutVolume

This API is used to set volume.
```
public abstract int setPlayoutVolume(int volume);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| volume | int | Volume. Value range: 0-100. Default value: `100` |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***

### enableVolumeEvaluation

This API is used to enable the volume reminder for playback.
>? After enabling the volume reminder, you can get the SDK’s volume evaluation through the `V2TXLivePlayerObserver.onPlayoutVolumeUpdate` callback.
```
public abstract int enableVolumeEvaluation(int intervalMs);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| intervalMs | int | Interval (ms) for triggering the `onPlayoutVolumeUpdate` callback. The minimum interval allowed is 100 ms. If the value is `0` (default) or smaller, the callback is disabled. `300` is recommended.|

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

***


## Other APIs
### setCacheParams

This API is used to set the minimum and maximum cache time (s) for auto adjustment by the player.
```
public abstract int setCacheParams(float minTime, float maxTime);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| minTime | float | The minimum cache time for auto adjustment by the player. The value must be greater than `0`. Default value: `1` |
| maxTime | float | The maximum cache time for auto adjustment by the player. The value must be greater than `0`. Default value: `5` |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed. `minTime` and `maxTime` must be greater than `0`.
- `V2TXLIVE_ERROR_REFUSED`: you cannot change the cache policy while streams are being played.

***

### showDebugView

This API is used to set whether to show the debug view for the player status information.
```
public abstract void showDebugView(boolean isShow);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| isShow | boolean | Whether to show the debug view. Default value: `NO` |


