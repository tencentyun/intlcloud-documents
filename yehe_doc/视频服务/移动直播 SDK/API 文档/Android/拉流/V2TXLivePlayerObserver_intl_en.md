**Overview**

Callbacks of Tencent Cloud’s live stream player.


**Features**

You can use `V2TXLivePlayerObserver` to receive callbacks of [V2TXLivePlayer](https://intl.cloud.tencent.com/document/product/1071/41276) including player status, playback volume, first audio/video frame, statistics, warning and error messages, etc.


## Basic Callback APIs
### onError

Callback for error
```
public void onError(V2TXLivePlayer player, int code, String msg, Bundle extraInfo)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| code    | int    | Error code   |
| msg  | String | Error message |
| extraInfo | Bundle|  Extra information |


### onWarning

Callback for warning
```
public void onWarning(V2TXLivePlayer player, int code, String msg, Bundle extraInfo)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| code      | int    | Warning code     |
| msg       | String | Warning message |
| extraInfo | Bundle |  Extra information |


## Video Callback APIs
### onVideoResolutionChanged

Callback for change of player resolution

```
public void onVideoResolutionChanged(V2TXLivePlayer player, int width, int height) 
```
#### Parameters
| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| width | int |  Video width |
| height | int | Video height |

### onVideoLoading

Callback for loading video

```
public void onVideoLoading(V2TXLivePlayer player, Bundle extraInfo)
```
#### Parameters
| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| extraInfo | Bundle |  Extra information |

### onVideoPlaying

Callback for video playback

```
public void onVideoPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo)
```
#### Parameters
| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| firstPlay | boolean | Whether it is the first playback |
| extraInfo | Bundle |  Extra information |

### onSnapshotComplete

Callback for a screenshot taken
```
public void onSnapshotComplete(V2TXLivePlayer player, Bitmap image)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| image | Bitmap * | The video image captured |


### onRenderVideoFrame

Callback for custom video rendering
>? You will receive this callback after calling `[V2TXLivePlayer enableCustomRendering:pixelFormat:bufferType:]` to enable custom video rendering.

```
public void onRenderVideoFrame(V2TXLivePlayer player, V2TXLiveVideoFrame videoFrame)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| videoFrame | V2TXLiveVideoFrame | Video frame |


## Audio Callback APIs
### onAudioLoading

Callback for loading audio

```
public void onAudioLoading(V2TXLivePlayer player, Bundle extraInfo)
```
#### Parameters
| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| extraInfo | Bundle |  Extra information |

### onAudioPlaying

Callback for audio playback

```
public void onAudioPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo)
```
#### Parameters
| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| firstPlay | boolean | Whether it is the first playback |
| extraInfo | Bundle |  Extra information |

### onPlayoutVolumeUpdate

Callback of the player’s volume.
```
public void onPlayoutVolumeUpdate(V2TXLivePlayer player, int volume)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| volume | int | Volume. Value range: 0-100 |


## Statistics Callback API
### onStatisticsUpdate
Callback of the player’s statistics.
```
public void onStatisticsUpdate(V2TXLivePlayer player, V2TXLivePlayerStatistics statistics)
```

#### Parameters

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| statistics | V2TXLivePlayerStatistics | Player statistics |


