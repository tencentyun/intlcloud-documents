This document describes the upgrade of GME from v2.2 to v2.3.5, making it easier for you to debug and access the APIs of GME.

## Changes in the SDK
### New Features
- Offline voice can be used during voice chat now.
- Voice chat can be filtered for terrorism, pornographic, and politically sensitive information now.
- HTML5-based voice chat is supported now, making voice chat available across all operating systems.
- Android v8a architecture is supported now.
- Low-latency capture and playback is adaptive to Android now.

### Optimizations
- Optimized the range voice APIs of the SDK to lower the access threshold.
- Optimized noise reduction for voice.
- Greatly reduced memory usage by the SDK.

## Changes in Major APIs
### EnterRoom 
The room entering operation has been changed from sync to async. If the return value is 0, the async delivery is successful and waiting to be processed by the callback function; otherwise, the async delivery fails.

```
public abstract int EnterRoom();
```

### ExitRoom 
The room exiting operation has been changed from sync to async. It is handled in the same way as the RoomExitComplete callback function. If the return value is AV_OK, the async delivery is successful.

>If there is a scenario in the application where room entering is performed immediately after room exiting, you don't need to wait for the RoomExitComplete callback notification from the ExitRoom API during API call; instead, you can directly call the API.

```
public abstract int ExitRoom();
```

## Changes in Error Codes
If you need to handle all error codes uniformly, use !AV_OK; 

If you need to handle each type of errors separately, pay attention to the error type returned by the API. Error code "1" has no specific meaning and will no longer be returned since v2.3.5, so it has been deleted.


## Changes in Other APIs
### PauseAudio/ResumeAudio 

```
public int PauseAudio()
public int ResumeAudio()
```

If the ITMGAudioCtrl::PauseAudio or ResumeAudio API is called in an SDK before v2.3, see the table below for version comparison.


| Version Before 2.3 | Version 2.3 |
|---|---|
| For mutual exclusivity with other modules | Change PauseAudio to Pause and change ResumeAudio to Resume |
| For using offline voice in voice chat | Delete PauseAudio and ResumeAudio |


### Changes in the Parameters of the SetLogLevel API

#### Legacy API
```
ITMGContext virtual void SetLogLevel(int logLevel, bool enableWrite, bool enablePrint)
```

#### New API
```
ITMGContext virtual void SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### Parameter Meanings

| Parameter | Type | Description |
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL| Sets the level of logs to be written. TMG_LOG_LEVEL_NONE indicates not to write |
|levelPrint|ITMG_LOG_LEVEL| Sets the level of logs to be printed. TMG_LOG_LEVEL_NONE indicates not to print |

#### ITMG_LOG_LEVEL Type

|ITMG_LOG_LEVEL| Description |
|-------------------------------|-------------|
|TMG_LOG_LEVEL_NONE=0		| Does not print logs			|
|TMG_LOG_LEVEL_ERROR=1		| Prints error logs (default)	|
|TMG_LOG_LEVEL_INFO=2			| Prints info logs		|
|TMG_LOG_LEVEL_DEBUG=3		| Prints debug logs	|
|TMG_LOG_LEVEL_VERBOSE=4		| Prints verbose logs		|
