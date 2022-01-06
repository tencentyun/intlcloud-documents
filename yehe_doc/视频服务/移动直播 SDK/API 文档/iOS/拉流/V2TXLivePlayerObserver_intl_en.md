
**Overview**

Callbacks of Tencent Cloud’s live stream player.


**Features**

You can use `V2TXLivePlayerObserver` to receive callbacks of [V2TXLivePlayer](https://intl.cloud.tencent.com/document/product/1071/41273), including player status, playback volume, first audio/video frame, statistics, warning and error messages, etc.


## Basic Callback APIs
### onError

Callback for error
```
- (void)onError:(id<V2TXLivePlayer>)player
            code:(V2TXLiveCode)code
         message:(NSString *)msg
       extraInfo:(NSDictionary *)extraInfo
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| code | V2TXLiveCode |  Error code |
| msg | NSString * | Error message |
| extraInfo | NSDictionary * |  Extra information |

***

### onWarning

Callback for warning
```
- (void)onWarning:(id<V2TXLivePlayer>)player
              code:(V2TXLiveCode)code
           message:(NSString *)msg
         extraInfo:(NSDictionary *)extraInfo
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| code | V2TXLiveCode |  Warning code |
| msg | NSString * |  Warning message |
| extraInfo | NSDictionary * |  Extra information |


### onConnected

Callback for successfully connecting to the server
```
- (void)onConnected:(id<V2TXLivePlayer>)player 
          extraInfo:(NSDictionary *)extraInfo
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| extraInfo | NSDictionary * |  Extra information |



## Video Callback APIs
### onVideoPlaying

Callback for video playback
```
- (void)onVideoPlaying:(id<V2TXLivePlayer>)player
             firstPlay:(BOOL)firstPlay 
             extraInfo:(NSDictionary *)extraInfo
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| firstPlay | BOOL |  Whether it is the first playback |
| extraInfo | NSDictionary * |  Extra information |



### onVideoLoading

Callback for loading video
```
- (void)onVideoLoading:(id<V2TXLivePlayer>)player
             extraInfo:(NSDictionary *)extraInfo;
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| extraInfo | NSDictionary * |  Extra information |


### onVideoResolutionChanged

Callback for change of player resolution
```
- (void)onVideoResolutionChanged:(id<V2TXLivePlayer>)player 
                           width:(NSInteger)width 
                          height:(NSInteger)height;
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| width | NSInteger | Video width |
| height | NSInteger | Video height |


### onSnapshotComplete

Callback for a screenshot taken
```
- (void)onSnapshotComplete:(id<V2TXLivePlayer>)player image:(TXImage *)image
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| image | TXImage * | The video image captured |


### onRenderVideoFrame

Callback for custom video rendering
> ? You will receive this callback after calling `[V2TXLivePlayer enableCustomRendering:pixelFormat:bufferType:]` to enable custom video rendering.

```
- (void)onRenderVideoFrame:(id<V2TXLivePlayer>)player
                     frame:(V2TXLiveVideoFrame *)videoFrame
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| videoFrame | V2TXLiveVideoFrame * | Video frame |



## Audio Callback APIs

### onAudioPlaying

Callback for audio playback
```
- (void)onAudioPlaying:(id<V2TXLivePlayer>)player 
             firstPlay:(BOOL)firstPlay 
             extraInfo:(NSDictionary *)extraInfo;
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| firstPlay | BOOL |  Whether it is the first playback |
| extraInfo | NSDictionary * |  Extra information |


### onAudioLoading

Callback for loading audio
```
- (void)onAudioLoading:(id<V2TXLivePlayer>)player 
             extraInfo:(NSDictionary *)extraInfo;
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| extraInfo | NSDictionary * |  Extra information |



### onPlayoutVolumeUpdate

Callback of the player’s volume
```
- (void)onPlayoutVolumeUpdate:(id<V2TXLivePlayer>)player volume:(NSInteger)volume
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| volume | NSInteger | Volume. Value range: 0-100 |


## Statistics Callback API

### onStatisticsUpdate

Callback of the player’s statistics
```
- (void)onStatisticsUpdate:(id<V2TXLivePlayer>)player
                statistics:(V2TXLivePlayerStatistics *)statistics
```

**Parameters**

| Parameter | Type | Description |
|-----|-----|-----|
| player | V2TXLivePlayer |  The player object sending the callback |
| statistics | V2TXLivePlayerStatistics | Player statistics |
