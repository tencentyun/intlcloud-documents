
__Feature__




__Overview__




## Basic Callback APIs
### onError

* @brief live player error notification, which is called back when the player encounters an error
```
- (void)onError:(id<TXLivePlayerV2>)player
            
         message:(NSString *)msg
       extraInfo:(NSDictionary *)extraInfo {
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|


| msg | NSString * | Error information |


***

### onWarning

Warning.
```
- (void)onWarning:(id<TXLivePlayerV2>)player
              
           message:(NSString *)msg
         extraInfo:(NSDictionary *)extraInfo {
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|


| msg       | String | Warning message |


***

## Video Callback APIs



```

                          
                          
                       extraInfo:(NSDictionary *)extraInfo {
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|










| ------------------------- | ------------------------------------------- |




***

### onSnapshotComplete

A screenshot was taken.
```
- (void)onSnapshotComplete:(id<V2TXLivePlayer>)player image:(TXImage *)image {
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|



***

### onRenderVideoFrame

Callback of custom video rendering.

```
- (void)onRecvFirstVideoFrame:(id<TXLivePlayerV2>)player;
                      
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|

| videoFrame | V2TXLiveVideoFrame | Video frame sent to the SDK |

***


## Audio Callback APIs



```
- (void)onConnectionStateUpdate:(id<TXLivePlayerV2>)player
                          
                          
                       extraInfo:(NSDictionary *)extraInfo {
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|





***



Player volume callback.
```
- (void)onPlayoutVolumeUpdate:(id<TXLivePlayerV2>)player
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|

| volume | NSInteger | Volume level. 100 indicates normal volume level. Value range: 0–100. |

***

## Statistics Callback API

### onStatisticsUpdate

Publisher statistics.
```
- (void)onStatisticsUpdate:(id<TXLivePlayerV2>)player
                 statistics:(TXLivePlayerStatistics *)statistics;
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|

| statistics | V2TXLivePusherStatistics | Publisher statistics |
