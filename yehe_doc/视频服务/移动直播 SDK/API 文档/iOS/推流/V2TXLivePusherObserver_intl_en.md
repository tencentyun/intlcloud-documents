__Overview__

Callback notifications for live stream publishing

**Features**

You can use `V2TXLivePusherObserver` to receive notifications about [V2TXLivePusher](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html), including publisher connection status, first audio/video frame, statistics, and warning and error messages.


## Basic Callback APIs
### onError

Callback for error. This callback is triggered when the publisher encounters an error.
```
- (void)onError:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| code | V2TXLiveCode |  Error code |
| msg | NSString * | Error message |
| extraInfo | NSDictionary * |  Extra information |

***

### onWarning

Callback for warning.
```
- (void)onWarning:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo
```
 
#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| code | V2TXLiveCode |  Warning code |
| msg | NSString * |  Warning message |
| extraInfo | NSDictionary * |  Extra information |

***

## Video Callback APIs
### onPushStatusUpdate

Callback of the publisher’s connection status.
```
- (void)onPushStatusUpdate:(V2TXLivePushStatus)status
                   message:(NSString *)msg
                 extraInfo:(NSDictionary *)extraInfo
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| status    | V2TXLivePushStatus | Status code       |
| msg       | NSString *         | Status message |
| extraInfo | NSDictionary * |  Extra information |

[](id:V2TXLivePushStatus)

#### `V2TXLivePushStatus` enumerated values

| Value | Description |
|---------|---------|
| V2TXLivePushStatusDisconnected   | Disconnected from the server |
| V2TXLivePushStatusConnecting     | Connecting to the server   |
| V2TXLivePushStatusConnectSuccess | Connected to the server   |
| V2TXLivePushStatusReconnecting   | Reconnecting to the server      |

***

### onSnapshotComplete

Callback for a screenshot taken.
```
- (void)onSnapshotComplete:(TXImage *)image
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| image | TXImage * | The video image captured |

***

### onProcessVideoFrame

Callback for custom video processing.
>? You will receive this callback after you call `V2TXLivePusher#enableCustomVideoProcess:(BOOL)enable pixelFormat:(V2TXLivePixelFormat)pixelFormat bufferType:(V2TXLiveBufferType)bufferType` to enable custom video processing.

```
- (void)onProcessVideoFrame:(V2TXLiveVideoFrame * _Nonnull)srcFrame dstFrame:(V2TXLiveVideoFrame * _Nonnull)dstFrame
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| srcFrame | V2TXLiveVideoFrame * | Images before processing |
| dstFrame | V2TXLiveVideoFrame * | Images after processing |

***

### onGLContextDestroyed
Callback for a GL context for custom video processing being destroyed.
```
- (void)onGLContextDestroyed
```
***

### onCaptureFirstVideoFrame
Callback for capturing the first video frame.
```
- (void)onCaptureFirstVideoFrame
```

***
## Audio Callback APIs
### onCaptureFirstAudioFrame
Callback for capturing the first audio frame.
```
- (void)onCaptureFirstAudioFrame
```

***

### onMicrophoneVolumeUpdate
Callback of mic capturing volume.
```
- (void)onMicrophoneVolumeUpdate:(NSInteger)volume
```

***

## Statistics Callback API
### onStatisticsUpdate
Callback of publisher statistics.
```
- (void)onStatisticsUpdate:(V2TXLivePusherStatistics *)statistics
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| statistics | V2TXLivePusherStatistics * | Publisher statistics |

***

## MixTranscoding Callback API
### onSetMixTranscodingConfig
Callback for setting On-Cloud MixTranscoding parameters.

>? You will receive this callback after you call `V2TXLivePusher#setMixTranscodingConfig:(V2TXLiveTranscodingConfig *)config` to set On-Cloud MixTranscoding parameters.

```
- (void)onSetMixTranscodingConfig:(V2TXLiveCode)code message:(NSString *)msg
```
| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| code | V2TXLiveCode | `0`: successful; other values: failed |
| msg | NSString * | Error message               |

