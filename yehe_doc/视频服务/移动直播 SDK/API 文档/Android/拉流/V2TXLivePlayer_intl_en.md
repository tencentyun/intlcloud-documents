
__Feature__


/// This player pulls audio and video data from the specified live streaming URL and plays the data after decoding and local rendering.

__Overview__

/// The player has the following capabilities:


/// - View capturing, which allows you to capture the video images of the current live stream.
/// - Delay adjustment, which allows you to set the minimum time and maximum time for auto adjustment of the player cache.
/// - Custom video data processing, which allows you to perform rendering and play video data after processing video data in the live stream based on the project requirements.


## Basic SDK APIs
### setObserver



```
public abstract void setObserver(V2TXLivePusherObserver observer);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|


***

## Basic Playback APIs
### setRenderView


```
public abstract int setRenderView(TXCloudVideoView view);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| view | TXCloudVideoView | Views rendered by player screen |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### setRenderView


```
public abstract int setRenderView(SurfaceView view);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|


#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### setRenderView


```
public abstract int setRenderView(TextureView view);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|


#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### startPlay

This API is used to stop playing back audio/video streams.
```
public abstract int startPush(String url);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|


#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: failed to publish streams because the URL is invalid.
- `V2TXLIVE_ERROR_REFUSED`: you cannot use the same stream ID for push and pull on the same device.

***

### stopPlay

This API is used to stop playing back audio/video streams.
```
public abstract int StopPlayFile();
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### isPlaying


```
public abstract int isPushing();
```

#### Response

Whether streams are being published
*         - 1: yes
*         - 0: no

***

## Video APIs
### setRenderRotation


```
public abstract int setRenderRotation(V2TXLiveRotation rotation);
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




```

```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|


#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful




| Value | Description |
|---------|---------|
| TXLiveFillMode_Fit | Make the view fit the screen without cropping. If the aspect ratio of the view is different from that of the screen, black edges will appear |
| TXLiveFillMode_Fill | Fill the image on the screen without leaving any black edges. If the aspect ratio of the view is different from that of the screen, part of the view content will be cropped |

***

### pauseVideo


```
public abstract int Pause();
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***





```
public abstract int Resume();
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### snapshot



>? After `V2TXLIVE_OK` is returned, you can get the screenshot taken in the `V2TXLivePusherObserver.onSnapshotComplete` callback.

```
public abstract int snapshot();
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_REFUSED`: failed to take a screenshot because publishing has stopped

***



*        Using this method, you can obtain every frame of the video view after decoding, perform custom rendering, and add custom display effects.

```

        
         
        
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| enable | Boolean | Whether to enable custom video capturing. Default value: `false`. |
| pixelFormat | [V2TXLivePixelFormat](#V2TXLivePixelFormat) | Pixel format of video frames |
| bufferType | [V2TXLiveBufferType](#V2TXLiveBufferType) | Video data buffer type |

#### Response
V2TXLiveCode:
- `V2TXLIVE_OK`: successful
*         - TXLIVE_ERROR_NOT_SUPPORTED: the pixel format or data format is not supported.

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

## Audio APIs


 
```
public abstract int Pause();
```
#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***


 
```
public abstract int Resume();
```
#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***



This API is used to set volume.
```
public abstract int SetMicVolume(int volume);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| volume | int | Volume level. Value range: 0–100. Default value: 100. |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***

### enableVolumeEvaluation

This API is used to enable the volume reminder.
>? After enabling the volume reminder, you can get the volume measured by the SDK in the `V2TXLivePusherObserver#onMicrophoneVolumeUpdate(int)` callback.
```
public abstract int enableVolumeEvaluation(int intervalMs);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| intervalMs | int | Interval (ms) for volume callbacks. The minimum interval allowed is 100 ms. If the value is `0` (default) or smaller, the callback is disabled. `300` is recommended.

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful

***


## Other APIs


* @brief Set the minimum time and maximum time (unit: ms) for auto adjustment of the player cache.
```

```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|



#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
*         - TXLIVE_ERROR_INVALID_PARAMETER: operation failed. minTime and maxTime must be greater than 0.


***

### showDebugView


```
public abstract void showDebugView(boolean isShow);
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| isShow | boolean | Whether to display the dashboard. Default value: `false` |


