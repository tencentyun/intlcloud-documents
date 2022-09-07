

This document describes the upgrade of GME.
## Upgrade from GME 2.x to 2.9

### SDK updates
- Dynamic library split
- Rename Android package

The GME SDK is updated with the following new library files in addition to libgmesdk.

### Library files' corresponding features

The new version of GME splits the dynamic libraries to reduce the package size. You can only import the library files you need. For example, if you only need the voice changing feature, to import `libgme_soundtouch` is good.

| Library File | Feature |
|----|-----|
|libgmefdkaac| 1. Used to enter an SD or HD voice room. 2. Used to play back accompaniment files in ACC format |
|libgmefaad2| Used to play back accompaniment files in MP4 format |
|libgmeogg| Used to play back accompaniment files in OGG format |
|libgmelamemp3| Used to play back accompaniment files in MP3 format |
|libgmesoundtouch| Used for voice changing and pitch changing |

### Upgrade Notice

For iOS upgrade, please see [iOS Project Upgrade guide](https://intl.cloud.tencent.com/document/product/607/46015).
For Android upgrade, you need to rename package(change Tencent into GME) and modify obfuscation configuration. Please see [Project Export](https://intl.cloud.tencent.com/document/product/607/40862).
For Unity upgrade, if you used SD or HD sound quality, or accompaniment, please see [Using HD Sound Quality](https://intl.cloud.tencent.com/document/product/607/46016).


## Upgrade from GME 2.2 to 2.3.5 
### SDK updates
**New features**
- Offline voice can be used during voice chat now.
- Voice chat can filter offensive, insecure, or inappropriate information.
- HTML5-based voice chat is supported now, making voice chat available across all operating systems.
- Android v8a architecture is supported now.
- Low-latency capture and playback is adaptive to Android now.

**Optimizations**
- Optimized the range voice APIs of the SDK to lower the access threshold.
- Optimized noise reduction for voice.
- Greatly reduced memory usage by the SDK.

### Changes in Major APIs
#### EnterRoom 
The room entering operation has been changed from sync to async. If the return value is 0, the async delivery is successful and waiting to be processed by the callback function; otherwise, the async delivery fails.

```
public abstract int EnterRoom();
```

#### ExitRoom 
The room exiting operation has been changed from sync to async. It is handled in the same way as the RoomExitComplete callback function. If the return value is AV_OK, the async delivery is successful.

>! If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.

```
public abstract int ExitRoom();
```

### Changes in Error Codes
- For uniform processing of all error codes, use !AV_OK. 
- To handle the errors separately, focus on the type of error returned by the API.

>? Error code "1" has no specific meaning and will no longer be returned since v2.3.5, so it has been deleted. 


### Changes in Other APIs
#### PauseAudio/ResumeAudio 

```
public int PauseAudio()
public int ResumeAudio()
```

If the `ITMGAudioCtrl::PauseAudio` or `ResumeAudio` API is called in an SDK before v2.3, please see the table below for version comparison.


| Before v2.3 | v2.3 |
|---|---|
| For mutual exclusivity with other modules | Change PauseAudio to Pause and change ResumeAudio to Resume |
| For using offline voice in voice chat | Delete PauseAudio and ResumeAudio |


#### Changes in the Parameters of the SetLogLevel API

**Original API**
```
ITMGContext virtual void SetLogLevel(int logLevel, bool enableWrite, bool enablePrint)
```

**New API**
```
ITMGContext virtual void SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

**Parameter description**

| Parameter | Type | Description |
|---|---|---|
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written, TMG_LOG_LEVEL_NONE means not to write |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed, TMG_LOG_LEVEL_NONE means not to print |

**ITMG_LOG_LEVEL Type**

|ITMG_LOG_LEVEL| Description |
|-------------------------------|-------------|
|TMG_LOG_LEVEL_NONE=0		| Do not print logs			|
|TMG_LOG_LEVEL_ERROR=1		| Prints error logs (default)	|
|TMG_LOG_LEVEL_INFO=2			| Prints prompt logs		|
|TMG_LOG_LEVEL_DEBUG=3		| Prints development and debugging logs	|
|TMG_LOG_LEVEL_VERBOSE=4		| Prints high-frequency logs		|

## Upgrade from GME 2.3.5 to 2.5.1 
### New APIs
#### GetSendStreamLevel 
This API is used to get the real-time audio upstreaming volume level. An int-type value will be returned. Value range: 0–100.

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSendStreamLevel();
```

#### GetRecvStreamLevel 
This API is used to get the real-time audio downstreaming volume levels of other members in the room. An int-type value will be returned. Value range: 0–100.

```
iter->second.level = ITMGContextGetInstance()->GetAudioCtrl()->GetRecvStreamLevel(iter->second.openid.c_str());
```

### API changes
#### Type change for returned values of voice messaging and speech-to-text APIs

The type of returned values of the following APIs has been changed to `int`.

```
StartRecording
UploadRecordedFile
DownloadRecordedFile
PlayRecordedFile
SpeechToText
```

## Upgrade from GME 2.5 to 2.7 
### New APIs
#### PlayRecordedFile(const char* filePath, ITMG_VOICE_TYPE voiceType)
This API is used to playback voice message with voice changing effects.

## SetAccompanyKey(int nKey)
This API is used to set the voice chat accompaniment up and down.

