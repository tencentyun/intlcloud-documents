__Overview__

Callbacks of Tencent Cloud’s live stream publisher

**Features**

You can use `V2TXLivePusherObserver` to receive callbacks of [V2TXLivePusher](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/v2_tx_live_pusher-library.html), including the publisher status, first audio/video frame, statistics, and warning and error messages.


## Basic Callback APIs
### onError

Callback for error. This callback is triggered when the publisher encounters an error.
```dart
V2TXLivePusherListenerType.onError
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| code | V2TXLiveCode |  Error code |
| msg  | String | Error message |
| extraInfo | Map |  Extra information |


### onWarning

Callback for warning.
```dart
V2TXLivePusherListenerType.onWarning
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| code | V2TXLiveCode |  Warning code |
| msg | String |  Warning message |
| extraInfo | Map |  Extra information |


## Video Callback APIs
### onPushStatusUpdate

Callback of the publisher’s connection status.
```dart
V2TXLivePusherListenerType.onPushStatusUpdate
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| status    | V2TXLivePushStatus | Status code       |
| msg       | String             | Status message |
| extraInfo | Map |  Extra information |

[](id:V2TXLivePushStatus)

#### `V2TXLivePushStatus` enumerated values

| Value | Description |
|---------|---------|
| V2TXLivePushStatusDisconnected: 0 | Disconnected from the server |
| V2TXLivePushStatusConnecting: 1 | Connecting to the server   |
| V2TXLivePushStatusConnectSuccess: 2 | Connected to the server   |
| V2TXLivePushStatusReconnecting:  3| Reconnecting to the server      |


### onSnapshotComplete

Callback for a screenshot taken
```dart
V2TXLivePusherListenerType.onSnapshotComplete
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| image | Uint8List | Screenshot taken |


### onProcessVideoFrame

Callback for custom video processing.
>? You will receive this callback after you call `V2TXLivePusher.enableCustomVideoProcess(bool enable, V2TXLivePixelFormat pixelFormat, V2TXLiveBufferType bufferType)` to enable custom video processing.

```dart
V2TXLivePusherListenerType.onProcessVideoFrame
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| srcFrame | Map | For images before processing |
| dstFrame | Map | For images after processing |


### onGLContextDestroyed
Callback for a GL context for custom video processing being destroyed.
```dart
V2TXLivePusherListenerType.onGLContextDestroyed
```


### onCaptureFirstVideoFrame
Callback for capturing the first video frame.
```dart
V2TXLivePusherListenerType.onCaptureFirstVideoFrame
```

## Audio Callback APIs
### onCaptureFirstAudioFrame
Callback for capturing the first audio frame.
```dart
V2TXLivePusherListenerType.onCaptureFirstAudioFrame
```


### onMicrophoneVolumeUpdate
Callback of mic capturing volume.
```dart
V2TXLivePusherListenerType.onMicrophoneVolumeUpdate
```


## Statistics Callback API
### onStatisticsUpdate
Callback of publisher statistics.
```dart
V2TXLivePusherListenerType.onStatisticsUpdate
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| statistics | Map | Publisher statistics |

## MixTranscoding Callback API
### onSetMixTranscodingConfig
Callback for setting On-Cloud MixTranscoding parameters.

>? You will receive this callback after you call `V2TXLivePusher.setMixTranscodingConfig(V2TXLiveTranscodingConfig config)` to set On-Cloud MixTranscoding parameters.

```dart
V2TXLivePusherListenerType.onSetMixTranscodingConfig
```

| Parameter | Type | Description |
|-----|-----|-----|
| code | V2TXLiveCode | `0`: successful; other values: failed |
| msg  | String | Error message               |