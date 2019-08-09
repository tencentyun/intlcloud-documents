This document describes the integration for real-time voice accompaniment in details to help developers debug and integrate APIs for Tencent Cloud's Game Multimedia Engine (GME).

## Real-time voice accompaniment APIs
|API     | Description   |
| ------------- |:-------------:|
|StartAccompany    				       |Start accompaniment|
|StopAccompany    				   	|End accompaniment|
|IsAccompanyPlayEnd				|Accompaniment is over or not|
|PauseAccompany    					|Pause accompaniment|
|ResumeAccompany					|Resume accompaniment|
|SetAccompanyVolume 				|Set accompaniment volume|
|GetAccompanyVolume				|Get accompaniment volume|
|SetAccompanyFileCurrentPlayedTimeByMs 				|Set playback progress|


>To use real-time voice accompaniment, it is required to integrate the GME SDK and enable real-time voice chat.

### How to use
Flow chart for social App: 
![](https://main.qcloudimg.com/raw/cdcd069530545ed560f99985b15edcc9.png)


### Start accompaniment
The StartAccompany API is used to start accompaniment. The supported formats include m4a, wav, and mp3. Calling this API will cause volume reset.

####  Function prototype  
```
ITMGAudioEffectCtrl virtual int StartAccompany(const char* filePath, bool loopBack, int loopCount, int msTime) 
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------
| filePath    	|char\* 	|The path of playing accompaniment.						|
| loopBack  	|bool	|Whether the mix is sent or not. It is generally set to true,  so that the other people can also hear the accompaniment.	|
| loopCount	|int    		|The number of loops. The -1 value means an infinite loop.	|
| msTime	|int   	|Delay time.						|

####  Sample code  
```
//Windows codes
ITMGContextGetInstance()->GetAudioEffectCtrl()->StartAccompany(filePath,true,-1,0);
//Android codes
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StartAccompany(filePath,true,loopCount,0);
//iOS codes
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StartAccompany:path loopBack:isLoopBack loopCount:loopCount msTime:0];
```

### Callback for playing accompaniment
The callback function OnEvent is called after the accompaniment is over. The ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH event message is returned, the action of this event should be implemented in OnEvent function.
The passed data includes result and file_path.
####  Sample code  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//Handle the event
		break;
	   	}
		...
        case ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH:
		{
		//Handle the even
		break;
		}
	}
}
```

### Stop accompaniment
The StopAccompany API is used to  stop accompaniment.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int StopAccompany(int duckerTime)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| duckerTime	|int             |Fade-out time.|

####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAccompany(0);
```

### Accompaniment is over or not
If accompaniment is over, the return value is  true; otherwise, it is false.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual bool IsAccompanyPlayEnd()
```
####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->IsAccompanyPlayEnd();
```


### Pause accompaniment
The PauseAccompany API is used to pause accompaniment.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int PauseAccompany()
```
####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAccompany();
```


### Resume accompaniment
The ResumeAccompany API is used to resume accompaniment.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int ResumeAccompany()
```
####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAccompany();
```

### Set if you can hear the accompaniment
This API is used to set if you can hear the accompaniment.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int EnableAccompanyPlay(bool enable)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|--------------|
| enable    |bool             |If accompaniment can be heard.|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->EnableAccompanyPlay(false);
```

### Set if others can hear the accompaniment
This API is used to set if others can hear the accompaniment.
#### Function prototype  
```
ITMGAudioEffectCtrl virtual int EnableAccompanyLoopBack(bool enable)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|--------------|
| enable    |bool             |If accompaniment can be heard.|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->EnableAccompanyLoopBack(false);
```

### Set accompaniment volume
The SetAccompanyVolume API is used to set accompaniment volume. The default value is 100. If the value is larger than 100, the volume is increased. If it is less than 100, the volume is decreased. The value ranges from 0 to 200.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int SetAccompanyVolume(int vol)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| vol    |int             |Volume value.|

####  Sample code  
```
int vol=100;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetAccompanyVolume(vol);
```

### Obtain accompaniment volume
The GetAccompanyVolume API is used to obtain accompaniment volume.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int GetAccompanyVolume()
```
####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyVolume();
```

### Obtain accompaniment playback progress
These two APIs are used to obtain accompaniment playback progress. Current / Total = Current loop count, and Current % Total = Current loop position.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int GetAccompanyFileTotalTimeByMs()
ITMGAudioEffectCtrl virtual int GetAccompanyFileCurrentPlayedTimeByMs()
```
####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyFileTotalTimeByMs();
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyFileCurrentPlayedTimeByMs();
```


### Set playback progress
The SetAccompanyFileCurrentPlayedTimeByMs API is used to set playback progress.
####  Function prototype  
```
ITMGAudioEffectCtrl virtual int SetAccompanyFileCurrentPlayedTimeByMs(unsigned int time)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| time    |int                |Playback progress in milliseconds.|

####  Sample code  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetAccompanyFileCurrentPlayedTimeByMs(time);
```


## Error codes

|Name|Value|Cause|Solution|
|------|------|------|-----|
|QAV_ERR_ACC_OPENFILE_FAILED        |4001|Failed to open file	|Check if the file and its path exists, and if there is permission to access the file.|
|QAV_ERR_ACC_FILE_FORAMT_NOTSUPPORT |4002|Unsupported file format	|Check if the file format is correct.|
|QAV_ERR_ACC_DECODER_FAILED         |4003|Decoding failed		|Check if the file format is correct.|
|QAV_ERR_ACC_BAD_PARAM              |4004|Parameter error		|Check if the parameters in the codes are correct.|
|QAV_ERR_ACC_MEMORY_ALLOC_FAILED    |4005|Memory allocation failed	|System resources are used up. If this error persists, please contact developers for help.|
|QAV_ERR_ACC_CREATE_THREAD_FAILED   |4006|Failed to create thread	|System resources are used up. If this error persists, please contact developers for help.|
|QAV_ERR_ACC_STATE_ILLIGAL          |4007|Invalid status		|This error occurred while calling the API in a status of not allowing to do so.|
