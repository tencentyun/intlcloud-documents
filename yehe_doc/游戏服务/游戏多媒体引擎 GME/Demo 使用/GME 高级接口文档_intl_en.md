

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
