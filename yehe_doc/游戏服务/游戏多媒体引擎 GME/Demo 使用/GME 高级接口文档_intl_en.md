

## iOS Audio API

The `SetAdvanceParams` API is used to enable/disable the following audio options before a user enters a room. 
```
[[ITMGContext GetInstance] SetAdvanceParams:keyString value:_value]
```

| Parameter | Description |
| --------- | -------------------------------- |
| keyString | Different keys represent different options      |
| value     |<li> 0: disable<li>1: enable|

### Key 
The key can be replaced by one of the following parameters to represent different audio options:
- **OptionMixWithOthers**
to mix audio. Once enabled, GME can run background music and voice chat at the same time.

- **OptionDuckOthers**
to duck background music. If both this option and `OptionMixWithOthers` are enabled, the speaker will be enabled to broadcast audio while the background music volume is ducked.

- **ReleaseAudioFoucus**
to release audio focus.
 - If enabled, audio focus is released when you exit a room, so that other audio apps can continue running, e.g. QQ Music.
 - If disabled, other audio apps cannot continue running when you exit a room.
 
 ## Setting Maximum Number of Mixing Channels

The `SetRecvMixStreamCount` API is used to set the maximum number of mixing channels before entering a chat room. This API is available for all platforms. Here, we take PC as an example:
```
public abstract int SetRecvMixStreamCount(int nCount);
```
**Parameters** 

| Parameter | Description |
| --------- | -------------------------------- |
| nCount | Specifies the number of mixing channels. The maximum is 20 |


## Setting Room Audio Type

The `SetForceUseMediaVol` API is used to enable/disable media volume for a chat room in Fluency (room type 1) or Standard (room type 2) mode.

```
[[ITMGContext GetInstance] SetAdvanceParams:SetForceUseMediaVol value:1]
```

#### Values
Different values are used for different features, and described as follows:
-**1**: sets the microphone for room type 1 from call volume (default) to media volume.
-**2**: sets the microphone for room type 2 from call volume (default) to media volume.
-**3**: sets the microphone back to call volume for both room types 1 and 2.

