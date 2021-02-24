

## iOS Audio API

The SetAdvanceParams API is used to enable/disable the following audio options before a user enters a room. 
```
[[ITMGContext GetInstance] SetAdvanceParams:keyString value:_value]
```

| Parameter | Description |
| --------- | -------------------------------- |
| keyString | Different keys represent different options      |
| value |<li> 0: disable<li>1: enable |

#### Key 
The key can be replaced by one of the following parameters to represent different audio options:
- **OptionMixWithOthers**
to mix audio. Once enabled, GME can run the background music and voice chat at the same time.

- **OptionDuckOthers**
to duck background music. If both this option and `OptionMixWithOthers` are enabled, the speaker will be enabled to broadcast audio while the background music volume is ducked.

- **ReleaseAudioFoucus**
to release audio focus.
 - If enabled, audio focus will be released when you exit a room so that other audio apps such as QQ Music can continue running.
 - If disabled, other audio apps cannot continue running when you exit a room.

## Setting the Maximum Number of the Mix Audio Channels

The SetRecvMixStreamCount API is used to set the maximum number of the mix audio channels before a user enters a room. Take the SetRecvMixStreamCount API on PCs as an example.
```
virtual int SetRecvMixStreamCount(int nCount) = 0;
```
**Parameters description** 

| Parameter | Description |
| --------- | -------------------------------- |
| nCount | The number of mix audio channels, up to 20 channels |


## Setting the Audio Type of the Room

If SetForceUseMediaVol is used before a user enters the room, the room with smooth sound quality or standard sound quality can use the media volume.

```
[[ITMGContext GetInstance] SetAdvanceParams:SetForceUseMediaVol value:1]
```

#### Value
Different values represent different options:
- **1**: room 1 can use the media volume after the mic is enabled. (call volume is used before)
- **2**: room 2 can use the media volume after the mic is enabled. (call volume is used before)
- **3**: room 1 and room 2 still use the call volume after the mic enabled.


## Obtaining the Speaking Volume of a Member in the Room
After the TrackingVolume API is called, it will monitor the `TIMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_USER_VOLUMES` event where the key-value pair is uin-volume. Through this API, the corresponding energy histogram can be generated based on the volume of a uin speaking in the room.
If you no longer need to obtain the speaking volume of the member in the room, please call the StopTrackingVolume API.
```
//TMGAudioCtrl
public int TrackingVolume(float fTrackingTimeS)
public int StopTrackingVolume();
```
| Parameter | Type | Description |
|----|---|----|
| fTrackingTimeS | float | The number of seconds of the monitoring. 0.5f is recommended. |
