
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
### setObserver

This API is used to set the callbacks of the player. After setting, you can listen for callback events of `V2TXLivePlayer`, including player status, playback volume, first audio/video frame, statistics, and warning and error messages.

```
- (void)setObserver:(id<V2TXLivePlayerObserver>)observer
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| observer | V2TXLivePlayerObserver | Target object for the player’s callbacks. For details, please see [V2TXLivePlayerObserver](https://www.tencentcloud.com/document/product/1071/41272). |


## Basic Playback APIs
### setRenderView

This API is used to set the rendering view to display video.
```
- (V2TXLiveCode)setRenderView:(TXView *)view
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| view | TXView * | The player’s rendering view |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

### startLivePlay

This API is used to start playing audio/video streams.
```
- (V2TXLiveCode)startLivePlay:(NSString *)url
```

>? Since v10.7, `startPlay` has been replaced by `startLivePlay`, and you need to call `V2TXLivePremier#setLicence` or `TXLiveBase#setLicence` to set the license to use the live playback feature (you only need to set the license once). Otherwise, playback will fail (black screen). You can use a live stream publishing license, UGSV license, or video playback license to activate the live playback feature. If you don’t have any of the licenses, you can [buy one](https://www.tencentcloud.com/document/product/1071/38546) or [apply for a trial license for free](https://console.tencentcloud.com/live/license).

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| url | NSString * | Playback URL of audio/video streams, which supports RTMP, HTTP-FLV, TRTC, and WebRTC|

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed because the URL is invalid.
- `V2TXLIVE_ERROR_REFUSED`: RTC does not support using the same stream ID for publishing and playback on the same device.


### stopPlay

This API is used to stop playing audio/video streams.
```
- (V2TXLiveCode)stopPlay;
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful


### isPlaying

This API is used to get whether the player is playing streams.
```
- (int)isPlaying
```

#### Response

Whether streams are being played
- `1`: yes
- `0`: no


## Video APIs
### setRenderRotation

This API is used to set the rotation of images displayed by the player.
```
- (V2TXLiveCode)setRenderRotation:(V2TXLiveRotation)rotation 
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| rotation | [V2TXLiveRotation](#V2TXLiveRotation) | The degrees by which images are rotated. Default value: 0. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

[](id:V2TXLiveRotation)

#### `V2TXLiveRotation` enumerated values

| Value                             | Description               |
| ------------------- | --------------- |
| V2TXLiveRotation0 | No rotation |
| V2TXLiveRotation90 | Rotate 90 degrees clockwise |
| V2TXLiveRotation180 | Rotate 180 degrees clockwise |
| V2TXLiveRotation270 | Rotate 270 degrees clockwise |


### setRenderFillMode

This API is used to set the image fill mode.
```
- (V2TXLiveCode)setRenderFillMode:(V2TXLiveFillMode)mode
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| mode | [V2TXLiveFillMode](#V2TXLiveFillMode) | The image fill mode. Default value: `V2TXLiveFillModeFit`. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

[](id:V2TXLiveFillMode)

#### `V2TXLiveFillMode` enumerated values

| Value                 | Description                                                         |
| -------------------- | ------------------------------------------------------------ |
| V2TXLiveFillModeFit | The image fits the screen without cropping. If the aspect ratio of the image and the screen do not match, there will be black bars. |
| V2TXLiveFillModeFill | The image fills the entire screen, without black bars. If the aspect ratio of the image and screen do not match, the parts of the image that don’t fit will be cropped. |


### pauseVideo

This API is used to pause playing video streams.
```
- (V2TXLiveCode)pauseVideo
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful



### resumeVideo

This API is used to resume playing video streams.
```
- (V2TXLiveCode)resumeVideo
```

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful


### snapshot

This API is used to take a screenshot of streamed video.

>? After `V2TXLIVE_OK` is returned, you can get the screenshot taken in the `[V2TXLivePlayerObserver onSnapshotComplete: image:]` callback.

```
- (V2TXLiveCode)snapshot
```

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_REFUSED`: failed to take a screenshot because playback has stopped.


### enableCustomRendering

This API is used to set custom video rendering.
You can use this API to obtain each frame of decoded video for custom rendering.

>? After custom rendering is enabled, you can get video frames in the `[V2TXLivePlayerObserver onRenderVideoFrame:frame:]` callback.
```
- (V2TXLiveCode)enableCustomRendering:(BOOL)enable
                           pixelFormat:(V2TXLivePixelFormat)pixelFormat
                            bufferType:(V2TXLiveBufferType)bufferType
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| enable | BOOL | Whether to enable custom rendering. Default value: `NO`. |
| pixelFormat | V2TXLivePixelFormat | Pixel format of the video called back for custom rendering |
| bufferType | V2TXLiveBufferType | Buffer type of the video called back for custom rendering |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_NOT_SUPPORTED`: unsupported pixel format or data format.

[](id:V2TXLiveFillMode)

#### `V2TXLivePixelFormat` enumerated values

| Value                             | Description               |
| ---------------------------- | ---------------- |
|  V2TXLivePixelFormatUnknown | Unknown |
|  V2TXLivePixelFormatI420|  YUV420P (I420) |
| V2TXLivePixelFormatNV12      | YUV420SP (NV12)  |
| V2TXLivePixelFormatBGRA32    | BGRA8888       |
| V2TXLivePixelFormatTexture2D | OpenGL 2D texture |

[](id:V2TXLiveFillMode)

#### `V2TXLiveBufferType` enumerated values

| Value                          | Description                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| V2TXLiveBufferTypeUnknown     | Unknown                                                       |
| V2TXLiveBufferTypePixelBuffer | This type can be used directly and is the most efficient. The iOS system provides various APIs to get or process pixel buffers.|
| V2TXLiveBufferTypeNSData      | This type affects performance to some extent because the process of converting `NSData` to `PixelBuffer` (the format the SDK can handle directly) involves memory copying. |
| V2TXLiveBufferTypeTexture     | Texture ID, which allows direct operation and delivers the best performance.                                  |


## Audio APIs
### pauseAudio

 This API is used to pause playing audio streams.
```
- (V2TXLiveCode)pauseAudio 
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

### resumeAudio

 This API is used to resume playing audio streams.
```
- (V2TXLiveCode)resumeAudio 
```
#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful


### setPlayoutVolume

This API is used to set volume.
```
- (V2TXLiveCode)setPlayoutVolume:(NSUInteger)volume;
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| volume | NSUInteger | Volume. Value range: 0-100. Default value: `100`. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

### enableVolumeEvaluation

This API is used to enable the volume reminder for playback.
>? After enabling the volume reminder, you can get the SDK’s volume evaluation through the `[V2TXLivePlayerObserver onPlayoutVolumeUpdate:volume:]` callback.
```
- (V2TXLiveCode)enableVolumeEvaluation:(NSUInteger)intervalMs
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| intervalMs | NSUInteger | Interval (ms) for triggering the `onPlayoutVolumeUpdate` callback. The minimum interval allowed is 100 ms. If the value is `0` (default) or smaller, the callback is disabled. `300` is recommended. |

#### Response

V2TXLiveCode:
`V2TXLIVE_OK`: successful

## Other APIs
### setCacheParams

This API is used to set the minimum and maximum cache time (seconds) for auto adjustment by the player.
```
- (V2TXLiveCode)setCacheParams:(CGFloat)minTime maxTime:(CGFloat)maxTime
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| minTime | CGFloat | The minimum cache time for auto adjustment by the player. The value must be greater than `0`. Default value: `1` |
| maxTime | CGFloat | The maximum cache time for auto adjustment by the player. The value must be greater than `0`. Default value: `5` |

#### Response

V2TXLiveCode:
- `V2TXLIVE_OK`: successful
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: operation failed. `minTime` and `maxTime` must be greater than `0`.
- `V2TXLIVE_ERROR_REFUSED`: you cannot change the cache policy while streams are being played.

### showDebugView

This API is used to set whether to show the debug view for the player status information.
```
- (void)showDebugView:(BOOL)isShow 
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| isShow | BOOL | Whether to show the debug view. Default value: `NO`. |
