## Overview
Thank you for using Tencent Cloud Game Multimedia Engine SDK. This document provides a detailed description that makes it easy for Nintendo Switch developers to debug and integrate the APIs of Game Multimedia Engine.

### Key considerations for using GME

| Important API | Description |
| ------------- |:-------------:|
|Init    		|Initializes GME 	|
|Poll    		|Triggers event callback	|
|EnterRoom	 	|Enters a room  		|
|EnableMic	 	|Enables the microphone 	|
|EnableSpeaker	|Enables the speaker 	|

**Notes:**

**When a GME API is called successfully, AV_OK is returned, and the value is 0.**

**GME APIs should be called in the same thread.**

**Authentication is needed before entering a room. Refer to the authentication section in relevant documentation for more information.**

**The Poll API should be called for GME to trigger event callback.**

**Refer to the callback message list for callback related information.**

**Device related operations can only be done after entering a room.**


## Initialization-related APIs
GME should be initialized with the authentication data before entering a room.

| API | Description |
| ------------- |:-------------:|
|Init    	|Initializes GME 	| 
|Poll    	|Triggers event callback	|
|Pause   	|Pauses the system	|
|Resume 	|Resumes the system	|
|Uninit    	|Deinitializes GME 	|


### Get a singleton

Get ITMGContext single instance first and all calls should be done accroding to this instance. ITMGDelegate is defined in the Application which is used to receive and process the callback from this instance.    
#### Function prototype 

```
QAVSDK_API ITMGContext* QAVSDK_CALL ITMGContextGetInstance();
```
#### Sample code  

```
ITMGContext* m_pTmgContext;
m_pTmgContext = ITMGContextGetInstance();
```


### Message passing
With the API class, the Delegate method is used to send callback notifications to your application. ITMG_MAIN_EVENT_TYPE indicates the message type. The parameter data is in json string format. See the relevant documentation for the key-value pairs.

#### Sample code 

```
//Function implementation:
class Callback : public SetTMGDelegate 
{
	virtual void OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data)
	{
  		switch(eventType)
  		{
   			//Determine the message type and process the message
  		}
 	}
}

Callback*  p = new Callback ();
m_pTmgContext->SetTMGDelegate(p);

```

### Initialize the SDK

For more information on how to obtain parameters, please see [GME Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).
This API call needs SdkAppId and openId. The SdkAppId is obtained from Tencent Cloud console, and the openId is used to uniquely identify a user. The setting rule for openId can be customized by App developers, and this ID must be unique in an App (only INT64 is supported).
SDK must be initialized before a user can enter a room.
#### Function prototype 

```
ITMGContext virtual void Init(const char* sdkAppId, const char* openId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId    	|char*   	|The sdkAppId obtained from Tencent Cloud console					|
| openId    	|char*   	|The openId supports Int64 type (which is passed after being converted to a string) only. It is used to identify users and must be greater than 10000. 	|

#### Sample code  

```
#define SDKAPPID3RD "1400035750"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```


### Trigger event callback

This API is used to trigger the event callback via periodic Poll call in update.
#### Function prototype

```
class ITMGContext {
protected:
    virtual ~ITMGContext() {}
    
public:    	
	virtual void Poll()= 0;
}

```
#### Sample code
```
void TMGTestScene::update(float delta)
{
    ITMGContextGetInstance()->Poll();
}
```


### Pause the system

This API is used to notify the engine for Pause when the system Pause occurs.
#### Function prototype

```
ITMGContext int Pause()
```

### Resume the system
This API is used to notify the engine for Resume when the system Resume occurs.
#### Function prototype

```
ITMGContext  int Resume()
```



### Deinitialize the SDK
This API is used to deinitialize SDK to make it uninitialized.

#### Function prototype 
```
ITMGContext int Uninit()

```
#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
context->Uninit();
```


## Voice Chat Room-Related APIs
After the initialization, API for entering a room should be called before Voice Chat can start.

| API | Description |
| ------------- |:-------------:|
|GenAuthBuffer    	|Generates authentication data |
|EnterRoom   		|Enters a room |
|IsRoomEntered   	|Indicates whether the room is entered successfully |
|ExitRoom 		|Exits the room |




### Authentication information
AuthBuffer is generated for the purpose of encryption and authentication. For more information about the authentication data, refer to  [GME Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### Function prototype
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| dwSdkAppID | int | The SdkAppId obtained from the Tencent Cloud console |
| strRoomID |char* | Room ID, maximum to 127 characters |
| strOpenID | char*   | User ID |
| strKey | char* | The key obtained from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme) |
| strAuthBuffer | char* | Returned authbuff |
| bufferLength | int | Length of returned authbuff |



#### Sample code  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,strAuthBuffer,&bufferLength);
```

### Join a room
This API is used to enter a room with the generated authentication data, and the ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received as a callback. Microphone and speaker are not enabled by default after a user enters the room.


#### Function prototype

```
ITMGContext virtual void EnterRoom(const char*  roomId, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)//Common API for entering a room
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId			|char*   		| Room ID. maximum to 127 characters.	|
| roomType 			|ITMG_ROOM_TYPE	|Audio type of the room,must be set to "ITMG_ROOM_TYPE_FLUENCY"	|
| authBuffer    		|char*     	| Authentication key			|
| buffLen   			|int   		| Length of the authentication key		|



#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, (char*)retAuthBuff,bufferLen);
```


### Callback for entering a room
ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received after a user enters a room, the action of this event should be implemented in the OnEvent function.
#### Code Description
```

void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//Process
		break;
		}
	}
}
```

### Identify whether the room is entered successfully
This API is called to identify whether the room is entered successfully. A bool value is returned.
#### Function prototype  
```
ITMGContext virtual bool IsRoomEntered()
```
#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
context->IsRoomEntered();
```

### Exit a room
This API is called to exit the current room.
#### Function prototype  

```
ITMGContext virtual void ExitRoom()
```
#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
```

### Callback for exiting a room
ITMG_MAIN_EVENT_TYPE_EXIT_ROOM message is received after a user exits a room, the action of this event should be implemented in the OnEvent function.
#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
		{
		//Process
		break;
		}
	}
}
```


### Callback after the room type is set
ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE message is received after a user change the room type. The returned parameters include result, error_info, and new_room_type. new_room_type represents the following information and the action of each event should be implemented in the OnEvent function.

| Event Sub-type | Parameters | Description |
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM		|1 	|Indicates that the audio type is inconsistent with that of the room to be entered and it is changed to that of the room.	|
| ITMG_ROOM_CHANGE_EVENT_START			|2	|Indicates that the room is entered and the audio type starts changing (e.g., the audio type is changed after the ChangeRoomType API is called.) |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE		|3	|Indicates that the room is entered and the audio type has changed |
| ITMG_ROOM_CHANGE_EVENT_REQUEST			|4	|Indicates that a room member calls the ChangeRoomType API to request a change in the audio type |	


#### Sample code  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		//Work with room type events
	 }
}
```

### Member status change
Notification about this event is sent only when the member status changes. To obtain the member status in real time, cache the notification when receiving it at a higher layer. The event message ITMG_MAIN_EVNET_TYPE_USER_UPDATE is returned. The "data" includes event_id and user_list, and the action of event_id should be implemented in the OnEvent function.
These events will only be sent when exceeding a certain threshold. For example, when audio data of a user is not received for more than two seconds, the ITMG_EVENT_ID_USER_NO_AUDIO will be sent.

|event_id     | Description | What is maintained at the App side |
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				|A member enters the room			| Member list		|
|ITMG_EVENT_ID_USER_EXIT    				|A member exits the room			| Member list		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		|A member sends audio packages		| Chat member list	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			|A member stops sending audio packages		| Chat member list	|

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		//Process
		//The developer parses the parameter to obtain eventID and user_list.
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    //A member enters the room
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    //A member exits the room
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    //A member sends audio packages
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //A member stops sending audio packages
			    break;
 		    default:
			    break;
		    }
		break;
		}
	}
}
```

### Quality monitoring events
The message for quality monitoring event is ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY. The returned parameters include weight, floss, and delay, which represent the following information and the action of this event should be implemented in the OnEvent function.

| Parameter | Description |
| ------------- |-------------|
|weight    				| Its value ranges from 1 to 5. The value of 5 indicates excellent quality of audio packets, and the value of 1 indicates poor quality of audio packets, which can barely be used; and "0" represents an initial value and is meaningless. |
|floss    				| Packet loss |
|delay    		| Voice chat delay (ms) |

### Message details

| Message | Description of message |   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				       |Enters the room |
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				         	|Exits the room |
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		       |Room disconnection due to network or other reasons |
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE				|Room type change event |

### Details of Data corresponding to the message
| Message | Data         | Example |
| ------------- |:-------------:| ------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		|result; error_info  					|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


## Audio APIs for Voice Chat
The audio APIs for Voice Chat can only be called after the SDK is initialized and the room is entered successfully.
Call scenario examples:

When a user click the UI button to enable or disable the microphone or speaker:
- For most game Apps, it's recommended to call EnableMic and EnableSpeaker APIs. Because calling EnableMic is equivalent to calling EnableAudioCaptureDevice and EnableAudioSend at the same time, and calling EnableSpeaker is equivalent to calling EnableAudioPlayDevice and EnableAudioRecv at the same time.
  
- If you do not need to enable both the microphone and the speaker (releasing the recording permission to other modules), it is recommended to call PauseAudio/ResumeAudio.


| API | Description |
| ------------- |:-------------:|
|EnableMic    						|Enables/disables the microphone |
|GetMicState    						|Obtains the microphone status |
|GetMicLevel    						|Obtains real-time microphone volume |
|SetMicVolume    					|Sets microphone volume |
|GetMicVolume    					|Obtains microphone volume |
|EnableSpeaker    					|Enables/disables the speaker |
|GetSpeakerState    					|Obtains the speaker status |
|GetSpeakerLevel    					|Obtains real-time speaker volume |
|SetSpeakerVolume    				|Sets speaker volume |
|GetSpeakerVolume    				|Obtains speaker volume |
|EnableLoopBack    					|Enables/disables in-ear monitoring |





### Enable/disable the microphone
This API is used to enable/disable the microphone. Microphone and speaker are not enabled by default after a user enters a room.

#### Function prototype  
```
ITMGAudioCtrl virtual void EnableMic(bool bEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |To enable the microphone, set this parameter to true, otherwise, set it to false. |

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```

### Obtain the microphone status
This API is used to obtain the microphone status. "0" means microphone is enabled, "1" means microphone is disabled, "2" means microphone is under working.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetMicState()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();
```



### Obtain real-time microphone volume
This API is used to obtain real time microphone volume. An int value is returned.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetMicLevel()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicLevel();
```

### Set software volume for the microphone
This API is used to set software volume for the microphone. The value "0" means Mute, and "100" means the volume remains unchanged. Default value is 100.
#### Function prototype  
```
ITMGAudioCtrl virtual void SetMicVolume(int vol)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| vol    |int      | Sets the volume, value range: 0 to 200 |

#### Sample code  
```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetMicVolume(vol);
```

### Obtain software volume for the microphone
This API is used to obtain the software volume for the microphone. An int value is returned to indicate the software volume for the microphone. Returned value of 101 means SetMicVolume() has not been called.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetMicVolume()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicVolume();
```



### Enable/disable the speaker
This API is used to enable/disable the speaker.

#### Function prototype  
```
ITMGAudioCtrl virtual void EnableSpeaker(bool enabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable   		|bool       	| To disable the speaker, set this parameter to false, otherwise, set it to true.	|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```

### Obtain the speaker status
This API is used to obtain the speaker status. "0" means speaker is enabled, "1" means speaker is disabled, "2" means speaker is under working.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetSpeakerState()
```

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();
```





### Obtain real-time speaker volume
This API is used to obtain real time speaker volume. An int value is returned to indicate the real-time speaker volume.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetSpeakerLevel()
```

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerLevel();
```

### Set software volume for the speaker
This API is used to set the software volume for the speaker.
The value "0" means Mute, and "100" means the volume remains unchanged. Default value is 100.


#### Function prototype  
```
ITMGAudioCtrl virtual void SetSpeakerVolume(int vol)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| vol    |int        | Sets the volume, value range: 0 to 200 |

#### Sample code  
```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);
```

### Obtain software volume for the speaker
This API is used to obtain the software volume for the speaker. An int value is returned to indicate the software volume for the speaker. Returned value of 101 means SetSpeakerVolume() has not been called.
"Level" indicates the real-time volume, and "Volume" is the software volume for the speaker. The ultimate volume equals to Level*Volume%. For example, if the value for "Level" is 100 and the one for "Volume" is 60, the ultimate volume will be "60".

#### Function prototype  
```
ITMGAudioCtrl virtual int GetSpeakerVolume()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerVolume();
```


### Enable in-ear monitoring
This API is used to enable in-ear monitoring.
#### Function prototype  
``` 
ITMGAudioCtrl virtual int EnableLoopBack(bool enable)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable    |bool         | Specifies whether to enable in-ear monitoring |

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableLoopBack(true);
```



## Advanced APIs

### Obtain diagnostic messages
This API is used to obtain information about the quality of real-time audio/video calls. This API is mainly used to check the quality of real-time calls and troubleshoot problems, and can be ignored at the business side.
#### Function prototype  

```
ITMGRoom virtual const char* GetQualityTips()
```
#### Sample code  

```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();
```




## Callback Messages

#### Message list:

| Message | Description of message |   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		| Enters the audio room |
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		| Exits the audio room |
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT		| Room disconnection due to network or other reasons |
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE		|Room type change event |
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH		|The accompaniment is over |
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE		|The room members are updated |
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE	|PTT recording is completed |
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE	|PTT is successfully uploaded |
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|PTT is successfully downloaded |
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE		|The playback of PTT is completed |
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|The voice-to-text conversion is completed |

#### Data list

| Message | Data         | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|result; error_info			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|result; error_info  			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    	|result; error_info  			|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    	|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE    		|user_list;  event_id			|{"event_id":1,"user_list":["0"]}|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE 	|result; file_path  			|{"filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE 	|result; file_path;file_id  		|{"file_id":"","filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|result; file_path;file_id  		|{"file_id":"","filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE 	|result; file_path  			|{"filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|result; file_path;file_id		|{"file_id":"","filepath":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE	|result; text; file_path;file_id		|{"file_id":"","filepath":","text":"","result":0}|

