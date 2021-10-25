**Overview**

Callback notifications for live stream publishing

**Features**

You can use `V2TXLivePusherObserver` to receive notifications about [V2TXLivePusher](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html), including publisher connection status, first audio/video frame, statistics, and warning and error messages.


## Basic Callback APIs
### onError

Callback for error. This callback is triggered when the publisher encounters an error.
```
public void onError(int code, String msg, Bundle extraInfo)
```

#### Parameters

| Parameter | Type | Description |
| --------- | ------ | ---------- |
| code    | int    | Error code   |
| msg  | String | Error message |
| extraInfo | Bundle |  Extra information |

***

### onWarning

Callback for warning.
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

| Parameter | Type | Description |
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

Callback for a screenshot taken.
```
public void onSnapshotComplete(Bitmap image)
```

#### Parameters

| Parameter    | Type   | Description                                                                                                                    |
| ----- | -------- | ------------------ |
| image | Bitmap * | The video image captured |

***

### onProcessVideoFrame

Callback for custom video processing.
>? You will receive this callback after you call `V2TXLivePusher#enableCustomVideoProcess(boolean, V2TXLiveDef.V2TXLivePixelFormat, V2TXLiveDef.V2TXLiveBufferType)` to enable custom video processing.

```
public void onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame)
```

#### Parameters

| Parameter | Type | Description |
| -------- | ------------------ | -------------------------- |
| srcFrame | V2TXLiveVideoFrame | Images before processing |
| dstFrame | V2TXLiveVideoFrame | Images after processing |

***
### onGLContextCreated
Callback for a GL context for custom video processing being created.
```
public void onGLContextCreated()
```
***

### onGLContextDestroyed
Callback for a GL context for custom video processing being destroyed.
```
public void onGLContextDestroyed()
```

***

### onCaptureFirstVideoFrame
Callback for capturing the first video frame.
```
public void onCaptureFirstVideoFrame()
```

***

## Audio Callback APIs
### onCaptureFirstAudioFrame
Callback for capturing the first audio frame.
```
public void onCaptureFirstAudioFrame()
```

***

### onMicrophoneVolumeUpdate
Callback of mic capturing volume.
```
public void onMicrophoneVolumeUpdate(int volume)
```

***

## Statistics Callback API
### onStatisticsUpdate
Callback of publisher statistics.
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
Callback for setting On-Cloud MixTranscoding parameters.

>? You will receive this callback after you call `V2TXLivePusher#setMixTranscodingConfig(V2TXLiveDef.V2TXLiveTranscodingConfig)` to set On-Cloud MixTranscoding parameters.

```
public void onSetMixTranscodingConfig(int code, String msg)
```
| Parameter    | Type   | Description                                                                                                                    |
| ---- | ------ | ---------------------------- |
| code | int    | `0`: successful; other values: failed |
| msg  | String | Error message               |
