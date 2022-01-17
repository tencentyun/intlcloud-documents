
This document describes the upgrade of GME.



## Upgrade from GME 2.2 to 2.3.5 
### SDK updates
**New features**
- Voice messaging and speech-to-text conversion can now be used during voice chat now.
- Voice chat can now be filtered for terrorism, pornographic, and politically sensitive information.
- HTML5-based voice chat is now supported, making voice chat available across all operating systems.
- Android v8a architecture is now supported.
- Low-latency capturing and playback are now adapted to Android.

**Optimizations**
- The range voice APIs of the SDK are optimized to lower the access threshold.
- Noise reduction for voice is optimized.
- Memory usage by the SDK is greatly reduced.

### Changes in major APIs
#### EnterRoom 
The room entry operation has been changed from sync to async. If the returned value is 0, the async delivery is successful and waiting to be processed by the callback function; otherwise, the async delivery fails.

```
public abstract int EnterRoom();
```

#### ExitRoom 
The room exit operation has been changed from sync to async. It is handled in the same way as the `RoomExitComplete` callback function. If the returned value is `AV_OK`, the async delivery is successful.

>If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.

```
public abstract int ExitRoom();
```

### Changes in error codes
- If you need to handle all error codes uniformly, use `!AV_OK`. 
- If you need to handle each type of errors separately, pay attention to the error type returned by the API.

>Error code "1" has no specific meaning and will no longer be returned since v2.3.5, so it has been deleted.


### Changes in other APIs
#### PauseAudio/ResumeAudio 

```
public int PauseAudio()
public int ResumeAudio()
```

If the `ITMGAudioCtrl::PauseAudio` or `ResumeAudio` API is called in an SDK below version 2.3, please see the table below for version comparison.


| Version Below 2.3 | Version 2.3 |
|---|---|
| For mutual exclusivity with other modules | Change `PauseAudio` to `Pause` and change `ResumeAudio` to `Resume` |
| For using voice messaging and speech-to-text in voice chat | Delete `PauseAudio` and `ResumeAudio` |


#### Changes in SetLogLevel API parameters

**Legacy API**
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
|levelWrite|ITMG_LOG_LEVEL| Sets the level of logs to be written. `TMG_LOG_LEVEL_NONE` indicates not to write |
|levelPrint|ITMG_LOG_LEVEL| Sets the level of logs to be printed. `TMG_LOG_LEVEL_NONE` indicates not to print |

**`ITMG_LOG_LEVEL` type**

|ITMG_LOG_LEVEL| Description |
|-------------------------------|-------------|
|TMG_LOG_LEVEL_NONE=0		| Does not print logs			|
|TMG_LOG_LEVEL_ERROR=1		| Prints error logs (default)	|
|TMG_LOG_LEVEL_INFO=2			| Prints info logs		|
|TMG_LOG_LEVEL_DEBUG=3		| Prints debug logs	|
|TMG_LOG_LEVEL_VERBOSE=4		| Prints verbose logs		|

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
This API is used to play voice messages with voice-changing effects.

#### SetAccompanyKey(int nKey)
This API is used to adjust the key for accompaniment in voice chat.