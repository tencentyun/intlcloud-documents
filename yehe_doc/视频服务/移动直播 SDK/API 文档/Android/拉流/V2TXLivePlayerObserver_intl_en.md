**Feature**




**Overview**




## Basic Callback APIs
### onError

* @brief live player error notification, which is called back when the player encounters an error
```
public void onError(int code, String msg, Bundle extraInfo)
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|

| code    | int    | Error code   |
| msg  | String | Error message |
| extraInfo | Bundle             | Extra information     |

***

### onWarning

Warning.
```
public void onWarning(int code, String msg, Bundle extraInfo)
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|

| code      | int    | Warning code     |
| msg       | String | Warning message |
| extraInfo | Bundle             | Extra information     |

***

## Video Callback APIs



```

        
         
        
        
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|



| extraInfo | Bundle             | Extra information     |


#### `V2TXLivePushStatus` enumerated values

| Value | Description |
|---------|---------|




***

### onSnapshotComplete

A screenshot was taken.
```
public void onSnapshotComplete(V2TXLivePlayer v2TXLivePlayer, Bitmap bitmap) {
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|

| image | Bitmap * | The screenshot taken |

***

### onRenderVideoFrame

Callback of custom video rendering.

```

```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|

| videoFrame | V2TXLiveVideoFrame | Video frame sent to the SDK |

***


## Audio Callback APIs



```

        
        
        
        
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|



| extraInfo | Bundle             | Extra information     |

***



Player volume callback.
```
- (void)onPlayoutVolumeUpdate:(id<TXLivePlayerV2>)player
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|

| volume | int | Volume. Value range: 0-100 |

***

## Statistics Callback API
### onStatisticsUpdate
Publisher statistics.
```
public void onStatisticsUpdate(V2TXLivePusherStatistics statistics)
```

#### Parameters

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|

| statistics | V2TXLivePusherStatistics | Publisher statistics |


