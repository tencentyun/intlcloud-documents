This document describes how to use the third-party player accompaniment feature for Windows.


## Prerequisites
- You have created a GME application and obtained the `AppID` and `Key` of the SDK as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- You have **activated the real-time voice service of GME** as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- Configure your project before using GME; otherwise, the SDK will not take effect.

## Configuring the Header File
1. Configure the GME project as instructed in [Project Configuration](https://intl.cloud.tencent.com/document/product/607/19068).
2. Put the `tmg_adv_win.h` file in the same directory as other header files in the GME SDK for Windows.
3. Click [here](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GME_Accompany_Plugin.zip) to download two DLL files. Their paths are the same as those of other library files. After the executable files are exported, the DLL files should be in the same directory as the executable files.



## Calling APIs
### Starting playback
This API is used to hook the audio of the entire system or a player.

#### Function prototype
```
virtual int StartAccompany(const char* playerPath, int playerPathLength, const char* mediaFilePath, int mediaFilePathLenght, GMEAccompany_SourceType sourceType) = 0
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| playerPath|const char*| Player path |
| playerPathLength|int| Player path length |
| mediaFilePath|const char*| Audio resource path, which can be a file path, folder path, or `NULL`. |
| mediaFilePathLenght|int| Audio resource path length |
| sourceType|GMEAccompany_SourceType| Capturing object type. For more information, see the [table below](#sourceType). |

[](id:sourceType)
`sourceType` description:

| Parameter | Type |
| ------------- |:-------------:|
|AV_ACCOMPANY_SOURCE_TYPE_NONE = 0| The feature is not enabled |
|AV_ACCOMPANY_SOURCE_TYPE_SYSTEM = 1| The audio of the entire system is hooked. You don't have to pass in the audio resource path but need to pass in a known file path as the player path parameter. |
|AV_ACCOMPANY_SOURCE_TYPE_PROCESS = 2| The audio of a process, such as QQ Music, is hooked |

#### Sample code
```
const char* file = "C:\\1.txt";// When hooking the system audio, you need to pass in a known file path. Make sure that the file exists.
int ret = ITMGAdcanceGetInstance()->StartAccompany(file, strlen(file), NULL, 0, AV_ACCOMPANY_SOURCE_TYPE_SYSTEM);
```

### Stopping playback
This API is used to stop hooking.

#### Function prototype
```
virtual int StopAccompany() = 0
```

### Setting the audio volume level
This API is used to set the volume level of the hooked audio. `100` indicates that the volume level remains unchanged. The value range is 0–200.

#### Function prototype
```
virtual int SetAccompanyVolume(int value) = 0;
```
### Getting the audio volume level
This API is used to get the volume level of the hooked audio.

#### Function prototype
```
virtual int GetAccompanyVolume(int* pVolume) = 0;
```
### Getting the real-time audio volume level
This API is used to get the volume level of the real-time audio, which can be used to display the real-time volume bar.

#### Function prototype
```
virtual int GetAccompanyVolumeDynamic(int* pVolume) = 0;
```
### Setting the capturing device's volume level
This API is used to set the volume level of the capturing device. The default value is `100`, the value range is 0–100, and `0` indicates that the device is mute.

#### Function prototype
```
virtual int SetMicDeviceVolume(int vol) = 0;
```
### Getting the capturing device's volume level
This API is used to get the volume level of the capturing device.

#### Function prototype
```
virtual int GetMicDeviceVolume() = 0;
```

### Setting the playback device's volume level
This API is used to set the volume level of the playback device. The default value is `100`, the value range is 0–100, and `0` indicates that the device is mute.

#### Function prototype
```
virtual int SetSpeakerDeviceVolume(int vol) = 0;
```

### Getting the playback device's volume level
This API is used to get the volume level of the playback device.

#### Function prototype
```
virtual int GetSpeakerDeviceVolume() = 0;
```
