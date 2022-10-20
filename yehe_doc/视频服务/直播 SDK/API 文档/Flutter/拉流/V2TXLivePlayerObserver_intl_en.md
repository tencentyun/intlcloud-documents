__Overview__

Callbacks of Tencent Cloud’s live stream player.


__Features__

You can use `V2TXLivePlayerObserver` to receive callbacks of [V2TXLivePlayer](https://pub.dev/documentation/live_flutter_plugin/latest/v2_tx_live_player/v2_tx_live_player-library.html), including the player status, playback volume, first audio/video frame, statistics, and warning and error messages.


## Basic Callback APIs
### onError

Callback for error
```dart
V2TXLivePlayerListenerType.onError
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| code | V2TXLiveCode |  Error code |
| msg  | String | Error message |
| extraInfo | Map |  Extra information |

### onWarning

Callback for warning
```dart
V2TXLivePlayerListenerType.onWarning
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| code | V2TXLiveCode |  Warning code |
| msg       | String | Warning message |
| extraInfo | Map |  Extra information |

### onConnected

Callback for successfully connecting to the server
```dart
V2TXLivePlayerListenerType.onConnected
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| extraInfo | Map |  Extra information |

## Video Callback APIs
### onVideoPlaying

Callback for video playback
```dart
V2TXLivePlayerListenerType.onVideoPlaying
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| firstPlay | bool |  Whether it is the first playback |
| extraInfo | Map |  Extra information |

### onVideoLoading

Callback for loading video
```dart
V2TXLivePlayerListenerType.onVideoLoading
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| extraInfo | Map |  Extra information |

### onVideoResolutionChanged

Callback for change of player resolution
```dart
V2TXLivePlayerListenerType.onVideoResolutionChanged
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| width | int |  Video width |
| height | int | Video height |

### onSnapshotComplete

Callback for a screenshot taken
```dart
V2TXLivePlayerListenerType.onSnapshotComplete
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| image | Uint8List | Screenshot taken |

### onRenderVideoFrame

Callback for custom video rendering
>? You will receive this callback after calling `V2TXLivePlayer.enableCustomRendering(pixelFormat:bufferType:)` to enable custom video rendering.

```dart
V2TXLivePlayerListenerType.onRenderVideoFrame
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| videoFrame | Map | Video frames |


## Audio Callback APIs

### onAudioPlaying

Callback for audio playback
```dart
V2TXLivePlayerListenerType.onAudioPlaying
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| firstPlay | bool |  Whether it is the first playback |
| extraInfo | Map |  Extra information |

### onAudioLoading

Callback for loading audio
```dart
V2TXLivePlayerListenerType.onAudioLoading
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| extraInfo | Map |  Extra information |


### onPlayoutVolumeUpdate

Callback of the player’s volume
```dart
V2TXLivePlayerListenerType.onPlayoutVolumeUpdate
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume. Value range: 0-100. |

## Statistics Callback API

### onStatisticsUpdate

Callback of the player’s statistics
```dart
V2TXLivePlayerListenerType.onStatisticsUpdate
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| statistics | Map | Player statistics |
