This document describes how to access and debug the advanced APIs of GME SDK.

<dx-alert infotype="alarm" title="Note">
This document describes advanced APIs that don't need to be called unless necessary. Consult GME developers before calling them.
</dx-alert>

## Audio Advanced APIs

## iOS Audio APIs

The SetAdvanceParams API is used to enable/disable the following audio options before a user enters a room. 

```
[[ITMGContext GetInstance] SetAdvanceParams:keyString value:_value]
```

| Parameter | Description |
| --------- | ------------------------------- |
| keyString | Different keys represent different features |
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

### Checking whether the Ring/Silent switch of iPhone is on

<dx-alert infotype="explain" title="Description">
This API takes effect on GME SDK 2.8.4 or above.
</dx-alert>

#### Function prototype

```
CheckDeviceMuteState();
```

The returned value of 0 means that the Ring/Silent switch is off, while 1 means on.

### Checking mic status

<dx-alert infotype="explain" title="Description">
This API takes effect on GME SDK 2.8.4 or above.
</dx-alert>

#### Function prototype

```
TestMic();
```

#### Returned value handling

| Returned Value | Description | Handling |
| ------------------------------------ | ------------------- | ------------------------------------------------------------ |
| ITMG_TEST_MIC_STATUS_AVAILABLE = 0   | Normally available | No handling required |
| ITMG_TEST_MIC_STATUS_NO_GRANTED = 2 | Access not obtained/denied | The access permission needs to be obtained before the mic is enabled |
| ITMG_TEST_MIC_STATUS_INVALID_MIC = 3 | No device available | Generally, this error will be reported on PCs with no available mics. Please prompt the user to insert earphones or mic |
| ITMG_TEST_MIC_STATUS_NOT_INIT = 5 | Not initialized | Call `EnableMic` after `Init` |

### Setting Android Bluetooth device adaptation

<dx-alert infotype="explain" title="Description">
This API takes effect on GME SDK 2.8.4 or above.
</dx-alert>

Calling this API can solve the problem of sound leak when the mic on Bluetooth earphones is switched on/off, as well as the problem of playing back audio with the speaker after the connection status is changed after an Android device is connected to the Bluetooth earphones.

```
SetAdvanceParams("BluetoothUseMedia", "1");
```

### Setting the maximum number of the mix audio channels

The SetRecvMixStreamCount API is used to set the maximum number of the mix audio channels before a user enters a room. Take the SetRecvMixStreamCount API on PCs as an example.

```
virtual int SetRecvMixStreamCount(int nCount) = 0;
```

**Parameter description** 

| Parameter | Description |
| ------ | ------------------ |
| nCount | The number of mix audio channels, up to 20 channels |



## Room Advanced APIs

### Setting the audio type of the room

If SetForceUseMediaVol is used before a user enters the room, the room with smooth sound quality or standard sound quality can use the media volume.

```
[[ITMGContext GetInstance] SetAdvanceParams:SetForceUseMediaVol value:1]
```

#### Value

Different values represent different options:

- **1**: room 1 can use the media volume after the mic is enabled. (call volume is used before)
- **2**: room 2 can use the media volume after the mic is enabled. (call volume is used before)
- **3**: room 1 and room 2 still use the call volume after the mic enabled.

### Obtaining the speaking volume of a member in the room

After the TrackingVolume API is called, it will monitor the `TIMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_USER_VOLUMES` event where the key-value pair is uin-volume. Through this API, the corresponding energy histogram can be generated based on the volume of a uin speaking in the room.

If you no longer need to obtain the speaking volume of the member in the room, please call the StopTrackingVolume API.

```
//TMGAudioCtrl
public int TrackingVolume(float fTrackingTimeS)
public int StopTrackingVolume();
```

| Parameter | Type | Description |
| -------------- | ----- | --------------------------- |
| fTrackingTimeS | float | The number of seconds of the monitoring. 0.5f is recommended. |

## General Advanced APIs

### Fixing print log size

<dx-alert infotype="explain" title="Description">
This API takes effect on GME SDK 2.8.4 or above.
</dx-alert>

Call this API before the GME `Init` API to modify the default log file size. Currently, a single log file is 50 MB, and there can be up to 3 log files.

#### Function prototype

```
SetAdvanceParams(const char* key, const char* object)
```

| Parameter | Type | Description |
| ------ | ----------- | ------------------------------------------------------------ |
| key    | const char* | `MAX_LOG_FILE_SIZE_MB` and `MAX_LOG_FILE_COUNT` represent the size of a single log and the number of logs, respectively |
| object | const char* | When `key` is `MAX_LOG_FILE_SIZE_MB`, `object` is the default log file size, which can be 5 to 50 MB. When `key` is `MAX_LOG_FILE_COUNT`, `object` is the default number of log files, which can be 1 to 3. |

<dx-alert infotype="notice" title="Value range">
If the entered `object` value exceeds the upper limit of the value range, it will be set as the upper limit; if it is below the lower limit of the value range, it will be set as the lower limit.
</dx-alert>

#### Sample code

```
SetAdvanceParams("MAX_LOG_FILE_SIZE_MB", "5");
SetAdvanceParams("MAX_LOG_FILE_COUNT", "1");
```

