**Overview**

Callbacks of Tencent Cloud’s publisher

**Features**

You can use `V2TXLivePusherObserver` to receive callbacks of [V2TXLivePusher](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html) including publisher connection status, first audio/video frame, statistics, warning and error messages, etc.


## Basic Callback APIs
### onError

Callback of error.
```
public void onError(int code, String msg, Bundle extraInfo)
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
| --------- | ------ | ---------- |
| code    | int    | Error code   |
| msg  | String | Error message |
| extraInfo | Bundle | Extra information |

***

### onWarning

Callback of warning.
```
public void onWarning(int code, String msg, Bundle extraInfo)
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
| --------- | ------ | ------------ |
| code      | int    | Warning code     |
| msg       | String | Warning message |
| extraInfo | Bundle | Extra information   |

***

## Video Callback APIs
### onPushStatusUpdate

Callback of the publisher’s connection status.
```
public void onPushStatusUpdate(V2TXLivePushStatus status, String msg, Bundle extraInfo)
```

#### Parameters

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------------------ | -------------- |
| status    | V2TXLivePushStatus | Status code       |
| msg       | String             | Status message |
| extraInfo | Bundle             | Extra information     |

#### `V2TXLivePushStatus` enumerated values

| Value                             | Description               |
| -------------------------------- | ------------------ |
| V2TXLivePushStatusDisconnected   | Disconnected from the server |
| V2TXLivePushStatusConnecting     | Connecting to the server   |
| V2TXLivePushStatusConnectSuccess | Connected to the server   |
| V2TXLivePushStatusReconnecting   | Reconnecting to the server      |

***

### onSnapshotComplete

Callback of a screenshot taken.
```
public void onSnapshotComplete(Bitmap image)
```

#### Parameters

| Parameter    | Type   | Description                                                                                                                    |
| ----- | -------- | ------------------ |
| image | Bitmap * | The video image captured |

***

### onProcessVideoFrame

Callback of custom video processing.
>? You will receive this callback after you call `V2TXLivePusher#enableCustomVideoProcess(boolean, V2TXLiveDef.V2TXLivePixelFormat, V2TXLiveDef.V2TXLiveBufferType)` to enable custom video processing.
```
public void onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame)
```

#### Parameters

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ------------------ | -------------------------- |
| srcFrame | V2TXLiveVideoFrame | Images before processing |
| dstFrame | V2TXLiveVideoFrame | Images after processing |

***
### onGLContextCreated
Callback of creating an OpenGL context for custom video processing.
```
public void onGLContextCreated()
```
***

### onGLContextDestroyed
Callback of destroying the OpenGL context for custom video processing.
```
public void onGLContextDestroyed()
```

***

### onCaptureFirstVideoFrame
Callback of capturing the first video frame.
```
public void onCaptureFirstVideoFrame()
```

***

## Audio Callback APIs
### onCaptureFirstAudioFrame
Callback of capturing the first audio frame.
```
public void onCaptureFirstAudioFrame()
```

***

### onMicrophoneVolumeUpdate
Callback of mic volume.
```
public void onMicrophoneVolumeUpdate(int volume)
```

***

## Statistics Callback API
### onStatisticsUpdate
Callback of the publisher’s statistics.
```
public void onStatisticsUpdate(V2TXLivePusherStatistics statistics)
```

#### Parameters

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------------------------ | ---------------- |
| statistics | V2TXLivePusherStatistics | Publisher statistics |

***

## MixTranscoding Callback API
### onSetMixTranscodingConfig
Callback of setting On-Cloud MixTranscoding parameters.

>? You will receive this callback after you call `V2TXLivePusher#setMixTranscodingConfig(V2TXLiveDef.V2TXLiveTranscodingConfig)` to set On-Cloud MixTranscoding parameters.

```
public void onSetMixTranscodingConfig(int code, String msg)
```
| Parameter        | Type    | Description                                                                                                      |
| ---- | ------ | ---------------------------- |
| code | int    | `0`: successful; other values: failed |
| msg  | String | Error message               |