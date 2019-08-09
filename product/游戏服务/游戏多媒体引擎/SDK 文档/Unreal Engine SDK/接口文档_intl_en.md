This document describes the integration for Unreal Engine in details to help Unreal Engine developers debug and integrate APIs for Tencent Cloud's Game Multimedia Engine (GME).



## Key Considerations for Using GME

|Important API     | Description|
| ------------- |:-------------:|
|Init    		|Initializes GME 	|
|Poll    		|Triggers event callback	|
|EnterRoom	 	|Enters a room  		|
|EnableMic	 	|Enables the microphone 	|
|EnableSpeaker		|Enables the speaker 	|

>**Notes:**
- Configure the project before using GME, otherwise the SDK will not be valid.
- After a GME API is called successfully, AV_OK will be returned with a value of 0.
- GME APIs should be called in the same thread.
- Authentication is needed before entering a room. Refer to the authentication section in relevant documentation for more information.
- The Poll API should be called periodically to trigger event callback.
- Refer to the callback message list for callback information.
- Device related operations can only be done after entering a room.
- For error code details, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173)

## How to Use
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)


## Initialization-related APIs
The SDK should be initialized before using real-time voice and offline voice.
For usage problems, see [General Problems](https://intl.cloud.tencent.com/document/product/607/30254).

| API     | Description   |
| ------------- |:-------------:|
|Init    	|Initializes GME	|
|Poll    	|Triggers event callback	|
|Pause   	|Pauses the system	|
|Resume 	|Resumes the system	|
|Uninit    	|Uninitializes GME 	|


### Preparations
You need to import the header file tmg_sdk before you can integrate GME. The classes in the header file inherit ITMGDelegate for message delivery and callback.
#### Sample code  

```
#include "tmg_sdk.h"

class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public ITMGDelegate
{
public:
...
private:
...
｝
```


### Get a singleton
Get ITMGContext single instance first and all calls should be done according to this instance. ITMGDelegate is defined in the Application which is used to receive and process the callback from this instance.
#### Sample code 
```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```


### Message passing
With the API class, the Delegate method is used to send callback notifications to your application. ITMG_MAIN_EVENT_TYPE indicates the message type. The data under Windows is in json string format. See the relevant documentation for the key-value pairs.

#### Sample code  
```
//Function implementation:
//UEDemoLevelScriptActor.h:
class UEDEMO1_API AUEDemoLevelScriptActor : public ALevelScriptActor, public SetTMGDelegate
{
public:
	void OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data);
｝

//UEDemoLevelScriptActor.cpp:
void AUEDemoLevelScriptActor::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data){
	//Identify and work with eventType here
}
```

### Initialize the SDK

For more information on getting parameters, see [Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).
SdkAppId and openId are the required parameters for requesting this API, where openId is for identifying a user and must be unique in an Application (only INT64 value type is supported). You can get SdkAppId from Tencent Cloud Console, and set rules for creating openId as a developer.
You must initialize the SDK before entering a room.
#### Function prototype

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| sdkAppId    	|char*   	|The SdkAppId obtained from Tencent Cloud console					|
| openId    	|char*   	|The value type of OpenID only accepts Int64 (the value is converted and passed to the function as a char*). OpenID is for identifying users and its value must be greater than 10000. 	|

#### Sample code 


```
std::string appid = TCHAR_TO_UTF8(CurrentWidget->editAppID->GetText().ToString().operator*());
std::string userId = TCHAR_TO_UTF8(CurrentWidget->editUserID->GetText().ToString().operator*());
ITMGContextGetInstance()->Init(appid.c_str(), userId.c_str());
```
### Trigger event callback
The Poll API should be called periodically to trigger event callback.
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
//Declaration in the header file
virtual void Tick(float DeltaSeconds);

//Code implementation
void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) 
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
This API is used to notify the engine for Resume when the system Resume occurs. The Resume API is only used to resume real-time voice.
#### Function prototype

```
ITMGContext int Resume()
```



### Uninitialize the SDK
This API is used to uninitialize the SDK. Uninitialization is needed when switching accounts.
#### Function prototype

```
ITMGContext int Uninit()
```
#### Sample code
```
ITMGContext* context = ITMGContextGetInstance();
context->Uninit();
```

## APIs For Voice Chat Room
After the initialization, API for entering a room should be called before Voice Chat can start.
For usage problems, see [Real-time Voice Problems](https://intl.cloud.tencent.com/document/product/607/30257).

| API     | Description   |
| ------------- |:-------------:|
|GenAuthBuffer    	|Initialization authentication|
|EnterRoom   		|Enters a room|
|IsRoomEntered   	|Indicates whether the room is entered successfully|
|ExitRoom 		|Exits the room|
|ChangeRoomType 	|Modifies the audio type of the user's room|
|GetRoomType 		|Obtains the audio type of the user's room|


### Authentication information
AuthBuffer is generated for the purpose of encryption and authentication. For more information on the authentication data, refer to [GME Key](https://intl.cloud.tencent.com/document/product/607/12218).    
The room ID parameter for voice message must be set to "null".

#### Function prototype
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| dwSdkAppID    			|int   		|The SdkAppId obtained from the Tencent Cloud console		|
| strRoomID    		|char*     |Room ID; 127 characters maximum (The room ID parameter for voice message must be set to "null").|
| strOpenID  		|char*     	|User ID|
| strKey    			|char*	    	|The key obtained from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme)					|
|strAuthBuffer		|char*	    	|Returned authbuff							|
| bufferLength   		|int    		|Length of returned authbuff. It is recommended to set it to 600.|


#### Sample code  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```



### Enter a room
When you enter a room with the generated authentication credentials, you receive a callback indicating ITMG_MAIN_EVENT_TYPE_ENTER_ROOM. By default, microphone and speaker will not be enabled after you enter the room. If AV_OK is returned, it indicates the callback is successful.
For entering a common voice chat room that does not involve team voice chat, use the common API for entering a room. For more information, see the [Range Voice](https://intl.cloud.tencent.com/document/product/607/17972).

#### Function prototype
```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| roomID			| char*    		|Room ID; 127 characters maximum 	|
| roomType 			|ITMG_ROOM_TYPE	|Audio type of the room		|
| authBuffer    		|char*     	|Authentication key			|
| buffLen   			|int   		|Length of the authentication key		|

For the room audio type definition, refer to [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### Callback for entering a room
ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received after a user enters a room. The action of this event should be implemented in the OnEvent function.

#### Sample code  
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

#### Data detail
|Message     | Data         |Example|
| ------------- |:-------------:|-------------|
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|


### Identify whether the user has entered the room successfully
This API is called to identify whether the user has entered the room successfully, and returns a boolean value.
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
This API is called to exit the current room. It is an async API. The returned value of AV_OK indicates a successful async delivery.

>If a user enters the room immediately after exiting a room in the application, the developer does not have to wait for the RoomExitComplete notification as a callback of ExitRoom in the API call process, but just needs to call the API directly.

#### Function prototype  
```
ITMGContext virtual int ExitRoom()
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

#### Data detail
|Message     | Data         |Example|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|


### Modify the audio type of the user's room
This API is used to modify the audio type of the user's room. A ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE callback event will be sent.
#### Function prototype  
```
IITMGContext TMGRoom public void ChangeRoomType((ITMG_ROOM_TYPE roomType)
```


|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| roomType    |ITMG_ROOM_TYPE    |The room type to be switched to. See the API EnterRoom for the audio type definition.|

#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```


### Obtain the audio type of the user's room
This API is used to obtain the audio type of the user's room. The returned value is the audio type of the room. Returned value of 0 means an error occurred. The audio type definition can be found in the API EnterRoom.

#### Function prototype  
```
IITMGContext TMGRoom public  int GetRoomType()
```

#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->GetRoomType();
```


### Callback after the room type is set
ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE message is received after a user changes the room type. The returned parameters include result, error_info, and new_room_type. new_room_type represents the following information and the action of each event should be implemented in the OnEvent function.

|Event Sub-type     | Parameters   |Description|
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM		|1 	|Indicates that the audio type is inconsistent with that of the room to be entered and it is changed to that of the room.	|
| ITMG_ROOM_CHANGE_EVENT_START			|2	|Indicates that the room is entered and the audio type starts changing (e.g., the audio type is changed after the ChangeRoomType API is called.)|
| ITMG_ROOM_CHANGE_EVENT_COMPLETE		|3	|Indicates that the room is entered and the audio type has changed|
| ITMG_ROOM_CHANGE_EVENT_REQUEST			|4	|Indicates that a room member calls the ChangeRoomType API to request a change in the audio type|	


#### Sample code  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
		//Work with room type events
	 }
}
```

#### Data detail
|Message     | Data         |Example|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


### Member status change
Notification about this event is sent only when the member status changes. To obtain the member status in real time, cache the notification when receiving it at a higher layer. The event message ITMG_MAIN_EVNET_TYPE_USER_UPDATE is returned. The "data" includes event_id and user_list, and the action of event_id should be implemented in the OnEvent function.
These events will only be sent when exceeding a certain threshold. For example, when audio data of a user is not received for more than two seconds, the ITMG_EVENT_ID_USER_NO_AUDIO will be sent.

|event_id     | Description         |What is maintained at the App side|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				|A member enters the room			|Member list		|
|ITMG_EVENT_ID_USER_EXIT    				|A member exits the room			|Member list		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		|A member sends audio packages		|Chat member list	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			|A member stops sending audio packages	|Chat member list	|

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
			    //A member sends audio packets
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    //A member stops sending audio packets
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

|Parameter     | Description         |
| ------------- |-------------|
|weight    				|Its value ranges from 1 to 5 The value of 5 indicates excellent quality of audio packets, and the value of 1 indicates poor quality of audio packets, which can barely be used; and 0 represents an initial value and is meaningless.|
|floss    				|Packet loss|
|delay    		|Voice chat delay (ms)|




### Message details

| Message     |Description of message|   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				       |Enters the room|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				         	|Exits the room|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		       |Room disconnection due to network or other reasons|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE				|Room type change event|

### Details of Data corresponding to the message
|Message     | Data         |Example|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		|result; error_info  					|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


## Audio APIs for Voice Chat
The APIs for Voice Chat can only be called after the SDK is initialized and you are in the room.
We recommend the following methods when enabling/disabling the microphone or speaker on the user page:
- For most game apps, call EnableMic and EnableSpeaker APIs. Because calling EnableMic is equivalent to calling EnableAudioCaptureDevice and EnableAudioSend at the same time, and calling EnableSpeaker is equivalent to calling EnableAudioPlayDevice and EnableAudioRecv at the same time.
- For other mobile apps such as social networking apps, enabling/disabling a capturing device will restart both the capturing and the playback devices. If the App is playing background music, it will also be interrupted. But if the microphone is enabled/disabled through control of upstream/downstream, playback will not be interrupted. So the calling method is: Call EnableAudioCaptureDevice(true) and EnableAudioPlayDevice(true) once after entering the room, and call EnableAudioSend/Recv to send/receive audio streams when the microphone button is clicked to enable or disable.
- If you wish to release the capture or the playback device separately, please refer to the EnableAudioCaptureDevice and EnableAudioPlayDevice API.
- Call Pause to pause the audio engine and Resume to resume the audio engine.



| API     | Description   |
| ------------- |:-------------:|
|GetMicListCount    				       	|Obtains the number of microphones|
|GetMicList    				      	|Enumerates microphones|
|GetSpeakerListCount    				      	|Obtains the number of speakers|
|GetSpeakerList    				      	|Enumerates speakers|
|SelectMic    				      	|Select the microphone|
|SelectSpeaker    				|Select speakers|
|EnableMic    						|Enables/disables the microphone|
|GetMicState    						|Obtains the microphone status|
|EnableAudioCaptureDevice    		|Enables audio capture device		|
|IsAudioCaptureDeviceEnabled    	|Indicates if audio capture device is enabled or not	|
|EnableAudioSend    				|Enables the audio sending	|
|IsAudioSendEnabled    				|Indicates if audio is being sent or not	|
|GetMicLevel    						|Obtains real-time microphone volume	|
|GetSendStreamLevel					|Obtain real-time volume of audio sending|
|SetMicVolume    					|Sets microphone volume		|
|GetMicVolume    					|Obtains microphone volume		|
|EnableSpeaker    					|Enables/disables the speaker|
|GetSpeakerState    					|Obtains the speaker status |
|EnableAudioPlayDevice    			|Enables audio playback device		|
|IsAudioPlayDeviceEnabled    		|Indicates if audio playback devices is enabled or not	|
|EnableAudioRecv    					|Enables the audio receiving	|
|IsAudioRecvEnabled    				|Indicates if audio is being received or not	|
|GetSpeakerLevel    					|Obtains real-time speaker volume	|
|GetRecvStreamLevel					|Obtain real-time volume of audio receiving of other members in the room|
|SetSpeakerVolume    				|Sets speaker volume		|
|GetSpeakerVolume    				|Obtains speaker volume		|
|EnableLoopBack    					|Enables/disables in-ear monitoring			|



### Obtain the number of microphones
This API is used to obtain the number of microphones.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetMicListCount()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicListCount();
```

### Enumerate microphones
This API is used together with the GetMicListCount API to enumerate microphones.

#### Function prototype 
```
ITMGAudioCtrl virtual int GetMicList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| ppDeviceInfoList    	|TMGAudioDeviceInfo   	|Device list		|
| nCount    		|int     		|The number of microphones obtained	|

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicList(ppDeviceInfoList,nCount);
```



### Select the microphone
This API is used to select the microphone. If this API is not called or an "DEVICEID_DEFAULT" is passed in, the default microphone is selected. The device ID comes from the GetMicList API return list.

#### Function prototype  

```
ITMGAudioCtrl virtual int SelectMic(const char* pMicID)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| pMicID    |char*      |Microphone ID|

#### Sample code  

```
const char* pMicID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectMic(pMicID);
```

### Enable/disable the microphone
This API is used to enable/disable the microphone. By default, microphone and speaker will not be enabled after a user enters a room.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
#### Function prototype  
```
ITMGAudioCtrl virtual int EnableMic(bool bEnabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |To enable the microphone, set this parameter to true; otherwise, set it to false.|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```

### Obtain the microphone status
This API is used to obtain the microphone status. "0" means microphone is disabled; "1" means microphone is enabled.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetMicState()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();
```

### Enable/disable audio capture device
This API is used to enable/disable the audio capture device. The audio capture device is not enabled by default.
- API can only be called after the room is entered.The device will disabled automatically after exiting the room.
- For mobile use case, permission is normally asked when enabling the capture device.

#### Function prototype  
```
ITMGContext virtual int EnableAudioCaptureDevice(bool enable)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| enable    |bool     |true means enable, false means disable|

#### Sample code

```
Enable a capturing device
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioCaptureDevice(true);
```

### Obtain the audio capture device status
This API is used to obtain the audio capture device status.
#### Function prototype

```
ITMGContext virtual bool IsAudioCaptureDeviceEnabled()
```
#### Sample code

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioCaptureDeviceEnabled();
```

### Enable/disable the audio sending
This API is used to enable/disable the audio sending. If capturing device is open, captured audio will be sent. Otherwise, there will be no audio. See EnableAudioCaptureDevice for turning on/off capturing devices.

#### Function prototype

```
ITMGContext  virtual int EnableAudioSend(bool bEnable)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| enable    |bool     |true means enable audio sending, false means not|

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioSend(true);
```

### Obtain status on if captured audio is being sent
This API is called to obtain the status if captured audio is being sent.
#### Function prototype  
```
ITMGContext virtual bool IsAudioSendEnabled()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioSendEnabled();
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

### Obtain real-time volume of audio sending
This API is used to obtain real-time volume of audio sending. An int value is returned, ranging from 0 to 100.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetSendStreamLevel()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSendStreamLevel();
```

### Set software volume for the microphone
This API is used to set software volume for the microphone. The value "0" means Mute, and "100" means the volume remains unchanged. Default value is 100.

#### Function prototype  
```
ITMGAudioCtrl virtual int SetMicVolume(int vol)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| vol    |int      |Sets the volume, value range: 0 to 200|

#### Sample code  
```
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

### Obtain the number of speakers
This API is used to obtain the number of speakers.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerListCount()
```
#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerListCount();
```

### Enumerate speakers
This API is used together with the GetSpeakerListCount API to enumerate speakers.

#### Function prototype  
```
ITMGAudioCtrl virtual int GetSpeakerList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
public:
	const char* pDeviceID;
	const char* pDeviceName;
};
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| ppDeviceInfoList    	|TMGAudioDeviceInfo    	|Device list		|
| nCount   		|int     		|The number of speakers obtained	|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerList(ppDeviceInfoList,nCount);
```

### Select speakers
This API is used to select the playback device. If this API is not called or an "DEVICEID_DEFAULT" is passed in, the default device is selected. The device ID comes from the GetSpeakerList API return list.

#### Function prototype  
```
ITMGAudioCtrl virtual int SelectSpeaker(const char* pSpeakerID)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| pSpeakerID    |char*      |Speaker ID|

#### Sample code  
```
const char* pSpeakerID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectSpeaker(pSpeakerID);
```

### Enable/disable the speaker
This API is used to enable/disable the speaker.
EnableSpeaker = EnableAudioPlayDevice + EnableAudioRecv.
#### Function prototype  
```
ITMGAudioCtrl virtual int EnableSpeaker(bool enabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| enable   		|bool       	|To disable the speaker, set this parameter to false, otherwise, set it to true.|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```

### Obtain the speaker status
This API is used to obtain the speaker status. "0" means speaker is disabled, "1" means speaker is enabled, "2" means speaker is currently in use.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetSpeakerState()
```

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();
```



### Enable/disable audio playback device
This API is used to enable/disable audio playback device.

#### Function prototype  
```
ITMGContext virtual int EnableAudioPlayDevice(bool enable) 
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| enable    |bool        |true means enable, false means disable|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioPlayDevice(true);
```

### Obtain audio playback device status
This API is used to obtain the status of audio playback device.
#### Function prototype

```
ITMGContext virtual bool IsAudioPlayDeviceEnabled()
```
#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioPlayDeviceEnabled();
```

### Enable/disable the audio receiving
This API is used to enable/disable the audio receiving. If the device has been enabled, the audio of other members in the room will be played. Otherwise, there will be no playback. For enabling/disabling playback device, see the EnableAudioPlayDevice API.

#### Function prototype  

```
ITMGContext virtual int EnableAudioRecv(bool enable)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| enable    |bool     |true means enabling the audio receiving. false means not|

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioRecv(true);
```



### Obtain status on if received audio is being played
This API is called to obtain the status if received audio is being played.
#### Function prototype  
```
ITMGContext virtual bool IsAudioRecvEnabled() 
```

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioRecvEnabled();
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

### Obtain real-time volume of audio receiving of other members in the room
This API is used to obtain real-time volume of audio receiving of other members in the room. The return value is int type, which ranges from 0 to 100.
#### Function prototype  
```
ITMGAudioCtrl virtual int GetRecvStreamLevel(const char* openId)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| openId    |char*       |openId of other members in the room|

#### Sample code  
```
iter->second.level = ITMGContextGetInstance()->GetAudioCtrl()->GetRecvStreamLevel(iter->second.openid.c_str());
```

### Set software volume for the speaker
This API is used to set the software volume for the speaker.
The value "0" means Mute, and "100" means the volume remains unchanged. Default value is 100.

#### Function prototype  
```
ITMGAudioCtrl virtual int SetSpeakerVolume(int vol)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| vol    |int        |Sets the volume, value range: 0 to 200|

#### Sample code  
```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);
```

### Obtain software volume for the speaker

This API is used to obtain the software volume for the speaker. An int value is returned to indicate the software volume for the speaker. Returned value of 101 means SetSpeakerVolume() has not been called.
"Level" indicates the real-time volume, and "Volume" the is software volume for the speaker. The ultimate volume equals to Level*Volume%. For example, if the value for "Level" is 100 and the one for "Volume" is 60, the ultimate volume will be "60".

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
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| enable    |bool         |Specifies whether to enable in-ear monitoring|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableLoopBack(true);
```


## Flow Chart of Offline Voice-to-Text Converting
![](https://main.qcloudimg.com/raw/9ef5e5e4ebc8e63bcd7bfbea6cfb94cc.png)



## Offline Voice
The SDK should be initialized before using real-time voice and offline voice.
For usage problems, please see [Offline Voice Problems](https://intl.cloud.tencent.com/document/product/607/30258).

### Initialization API

| API     | Description   |
| ------------- |:-------------:|
|Init    	|Initializes GME	|
|Poll    	|Triggers event callback	|
|Pause   	|Pauses the system	|
|Resume 	|Resumes the system	|
|Uninit    	|Uninitializes GME 	|


### Offline Voice API
| API     | Description   |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    |authentication	|
|SetMaxMessageLength    |Specifies the maximum length of a voice message	|
|StartRecording		|Starts recording		|
|StartRecordingWithStreamingRecognition		|Starts streaming speech recognition		|
|PauseRecording|Pause recording|
|ResumeRecording|Resume recording|
|StopRecording    	|Stops recording		|
|CancelRecording	|Cancels recording		|
|GetMicLevel|Obtains real-time microphone volume of offline voice|
|SetMicVolume|Sets recording volume of offline voice|
|GetMicVolume|Obtains recording volume of offline voice|
|GetSpeakerLevel|Obtains real-time speaker volume of offline voice  |
|SetSpeakerVolume|Sets playback volume of offline voice|
|GetSpeakerVolume|Obtains playback volume of offline voice|
|UploadRecordedFile 	|Uploads voice files		|
|DownloadRecordedFile	|Downloads voice files		|
|PlayRecordedFile 	|Plays recorded voice files		|
|StopPlayFile		|Stops playing voice files		|
|GetFileSize 		|Obtains the size of a voice fil		|
|GetVoiceFileDuration	|Obtains the duration of a voice file		|
|SpeechToText 		|Converts the voice file into text with Speech Recognition		|

### Authentication
Do the authentication after the SDK is initialized. Please refer to the previous section on how to generate authBuffer.
#### Function prototype  
```
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| authBuffer    |char*                    |Authentication|
| authBufferLen    |int                |Length of the authentication|

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
```

### Specify the maximum length of a voice message
This API is used to specify the maximum length of a voice message. The maximum duration is 60 seconds.

#### Function prototype

```
ITMGPTT virtual int SetMaxMessageLength(int msTime)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| msTime    |int                    |Indicates the length of a voice message in millisecond|

#### Sample code  
```
int msTime = 10;
ITMGContextGetInstance()->GetPTT()->SetMaxMessageLength(msTime);
```


### Start recording
This API is used to start recording.
#### Function prototype  
```
ITMGPTT virtual int StartRecording(const char* fileDir)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| fileDir    |char*                      |Indicates the path for storing the voice file|

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->StartRecording(fileDir);
```

### Callback for starting recordings
The callback function OnEvent is called after the recording is started. The event message ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE is returned, the action of this event should be implemented in OnEvent function.
The passed parameter includes result and file_path.

#### Error codes
|Error Codes |Cause  |Solution        |
|-----|------|------|
|4097   |Empty parameter|Check if the API parameters in the codes are correct|
|4098   |Initialization error|Check if the device is occupied, the permissions is normal, or the initialization is normal.|
|4099   |Recording is in process|Ensure the SDK recording feature is used at the right time|
|4100   |Audio data is not collected|Check if the microphone works properly|
|4101   |File access error while recording|Ensure the file exists and its path is valid|
|4102   |The microphone is not authorized|Microphone permission is required for using SDK. To add the permission, see SDK project configuration document for the applicable engine or platform.|
|4103   |The recording time is too short|The recording time should be in millisecond and longer than 1 second|
|4104   |No recording start operation|Check if the start recording API is called|

#### Sample code  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//Process
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
		{
		//Process
		break;
		}
	}
}
```

### Enable streaming speech recognition
This API is used to start streaming speech recognition. Texts obtained from voice-to-text conversion will be returned in real time in its callback. It can also be used to translate specified information in an audio and return the text.

#### Function prototype  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| filePath    	|char*	|Indicates the path for storing the voice file	|
| speechLanguage    |char*                     |Recognizes specified language. See [language reference list](https://github.com/TencentMediaLab/GME/blob/master/GME%20Developer%20Manual/GME%20SpeechToText.md)|
| translateLanguage    |char*                     |Translates into specified language. See [language reference list](https://github.com/TencentMediaLab/GME/blob/master/GME%20Developer%20Manual/GME%20SpeechToText.md) (This parameter is not available. Enter the value for speechLanguage.) |

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```

### Callback for streaming speech recognition
The callback function OnEvent is called after the recognition is finished. The event message ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE is returned, the action of this event should be implemented in the OnEvent function.

|Message Name     | Description         |
| ------------- |:-------------:|
| result    	|Error code indicating whether streaming speech recognition is successful		|
| text    		|Text obtained from voice-to-text conversion	|
| file_path 	|Local path for the recorded voice file		|
| file_id 		|URL for the recorded voice file uploaded to server	|

#### Error codes

|Error Code     | Description         |Solution|
| ------------- |:-------------:|:-------------:|
|32775	|Recording is successful but streaming voice to text failed	|Call the API UploadRecordedFile to upload the recording, and then call the API SpeechToText to perform voice-to-text conversion.
|32777	|Recording and uploading is successful, but streaming voice to text is failed.	|The message returned includes a URL for successful upload. Call the SpeechToText API to perform voice-to-text conversion.
|32786  |Streaming voice-to-text converting failed|Streaming recording is in process, please wait for the streaming recording API to return execution result.|

#### Sample code  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//Process
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
		{
		//Process
		break;
		}
	}
}
```

### Pause recording
This API is used to pause recording. To resume recording, call the ResumeRecording API.

#### Function prototype  
```
ITMGPTT virtual int PauseRecording()
```
#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->PauseRecording();
```

### Resume recording
This API is used to resume recording.

#### Function prototype  
```
ITMGPTT virtual int ResumeRecording()
```
#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->ResumeRecording();
```

### Stop recording
This API is used to stop recording. This is an async API. There will be a callback after the recording is stopped. Only when the recording is successful can the recorded file be used.
#### Function prototype  
```
ITMGPTT virtual int StopRecording()
```
#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```



### Cancel recording
This API is used to cancel recording. There will not be a callback after the cancellation.
#### Function prototype  
```
ITMGPTT virtual int CancelRecording()
```
#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->CancelRecording();
```

### Obtain real-time microphone volume of offline voice
This API is used to obtain real-time microphone volume of offline voice. An int value is returned, ranging from 0 to 100.

#### Function prototype  
```
ITMGPTT virtual int GetMicLevel()
```
#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->GetMicLevel();
```

### Set recording volume of offline voice
This API is used to set recording volume of offline voice. The value ranges from 0 to 100.

#### Function prototype  
```
ITMGPTT virtual int SetMicVolume(int vol)
```
#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->SetMicVolume(100);
```

### Obtain recording volume of offline voice
This API is used to obtain recording volume of offline voice. An int value is returned, ranging from 0 to 100.

#### Function prototype  
```
ITMGPTT virtual int GetMicVolume()
```

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->GetMicVolume();
```


### Obtain real-time speaker volume
This API is used to obtain real-time speaker volume. An int value is returned, ranging from 0 to 100.

#### Function prototype  
```
ITMGPTT virtual int GetSpeakerLevel()
```

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerLevel();
```

### Set playback volume of offline voice
This API is used to set playback volume of offline voice. The value ranges from 0 to 100.

#### Function prototype  
```
ITMGPTT virtual int SetSpeakerVolume(int vol)
```
#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->SetSpeakerVolume(100);
```

### Obtain playback volume of offline voice
This API is used to obtain playback volume of offline voice. An int value is returned, ranging from 0 to 100.

#### Function prototype  
```
ITMGPTT virtual int GetSpeakerVolume()
```

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->GetSpeakerVolume();
```




### Upload voice files
This API is used to upload voice files.
#### Function prototype  
```
ITMGPTT virtual int UploadRecordedFile(const char* filePath)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |Indicates the path of the voice files to be uploaded|

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->UploadRecordedFile(filePath);
```


### Callback for uploading voice files
After the voice file is uploaded, the event message ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE is returned, the action of this event should be implemented in the OnEvent function.
The passed parameter includes result, file_path and file_id.

#### Error codes

|Error Codes |Cause  |Solution        |
|-----|------|------|
|8193   |File access error while uploading the file|Ensure the file exists and its path is valid|
|8194   |Failed to verify signature|Check if the authentication key is correct, and if the offline voice is initialized.|
|8195   |Network error|Check if the device can be accessed via public network|
|8196   |The network connection failed while getting upload parameters|Check if the authentication is correct, and the device can be accessed via public network.|
|8197   |The response packet is empty while getting upload parameters|Check if the authentication is correct, and the device can be accessed via public network.|
|8198   |Failed to parse the response packet while getting upload parameters|Check if the authentication is correct, and the device can be accessed via public network.|
|8200   |The appinfo is not set|Check if the apply API is called, or the input parameter is empty.|

#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//Process
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
		{
		//Process
		break;
		}
	}
}
```


### Download voice files
This API is used to download voice files.
#### Function prototype  
```
ITMGPTT virtual int DownloadRecordedFile(const char* fileID, const char* filePath) 
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| fileIDfileID  		|char*   	|URL to a file	|
| filePath 	|char*  	|Local path for saving the file	|

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->DownloadRecordedFile(fileID,filePath);
```


### Callback for downloading voice files
After the voice file is downloaded, the event message ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE is returned, the action of this event should be implemented in the OnEvent function.

#### Error codes

|Error Codes |Cause  |Solution        |
|-----|------|------|
|12289  |File access error while downloading the file    |Check if the file path is valid|
|12290  |The signature verification failed    |Check if the authentication key is correct, and if the offline voice is initialized.|
|12291  |Network storage system exception    |The server failed to get voice file. Check if the fileID is correct, network status is normal, and the cos file exists.|
|12292  |An error occurs in the file system of the server    |Check if the device can be accessed via public network, and if the server has this file.|
|12293  |An HTTP network error occurs while getting download parameters|Check if the device can be accessed via public network|
|12294  |The response packet is empty while getting download parameters |Check if the device can be accessed via public network|
|12295  |Failed to parse the response packet while getting download parameters|Check if the device can be accessed via public network|
|12297  |The appinfo is not set|Check if the authentication key is correct, and if the offline voice is initialized.|


#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//Process
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE:
		{
		//Process
		break;
		}
	}
}
```



### Play voice files
This API is used to play voice files.
#### Function prototype  
```
ITMGPTT virtual int PlayRecordedFile(const char* filePath)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| filePath    |char*                       |Indicates the path of the file to be played|

#### Error codes

|Error Codes |Cause  |Solution        |
|-----|------|------|
|20485  |Playback does not start|Ensure the file exists and its path is valid|

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->PlayRecordedFile(filePath);
```


### Callback for playing voice files
After the voice file is played back, the event message ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE is returned, the action of this event should be implemented in the OnEvent function.
The passed parameter includes result and file_path.

#### Error codes

|Error Codes |Cause  |Solution        |
|-----|------|------|
|20481  |Initialization error|Check if the device is occupied, the permissions is normal, or the initialization is normal.|
|20482  |A client fails to stop a video that is being played and play the next one (this can be done normally)|Check if the code logic is correct|
|20483  |Empty parameter|Check if the API parameters in the codes are correct|
|20484  |Internal error|Player initialization failed as decoding failed. Analyze logs for troubleshooting.|

#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//Process
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
		{
		//Process
		break;
		}
	}
}
```




### Stop playing voice files
This API is used to stop playing back voice files.
#### Function prototype  
```
ITMGPTT virtual int StopPlayFile()
```

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->StopPlayFile();
```



### Obtain the size of a voice file
This API is used to get the size of a voice file.
#### Function prototype  
```
ITMGPTT virtual int GetFileSize(const char* filePath)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |Indicates the path to a voice file|

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->GetFileSize(filePath);
```

### Obtain the length of a voice file
This API is used to obtain the duration of a voice file (in milliseconds).
#### Function prototype  
```
ITMGPTT virtual int GetVoiceFileDuration(const char* filePath)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| filePath    |char*                      |Indicates the path to a voice file|

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(filePath);
```


### Convert the specified voice file into text with Speech Recognition
This API is used to convert the specified voice file into text with Speech Recognition.

#### Function prototype  
```
ITMGPTT virtual void SpeechToText(const char* fileID)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| fileID    |char*                      |Indicates the URL to a voice file|

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(fileID);
```



### Translate the specified voice file into text with Speech Recognition (specify language)
This API is used to recognize specified language and translate the recognized information in an audio into specified language.

#### Function prototype  
```
ITMGPTT virtual int SpeechToText(const char* fileID,const char* speechLanguage,const char* translateLanguage)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| fileID    |char*                     |Voice file url|
| speechLanguage    |char*                     |Recognizes specified language. See [language reference list](https://github.com/TencentMediaLab/GME/blob/master/GME%20Developer%20Manual/GME%20SpeechToText.md)|
| translatelanguage    |char*                  |Translates into specified language. See [language reference list](https://github.com/TencentMediaLab/GME/blob/master/GME%20Developer%20Manual/GME%20SpeechToText.md) (This parameter is not available. Enter the value for speechLanguage.)|

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->SpeechToText(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```



### Callback for Speech Recognition
After the specified voice file is converted into text with Speech Recognition, the event message ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE is returned, the action of this event should be implemented in OnEvent function.
The passed parameter includes result, file_path and text (recognized text).

#### Error codes

|Error Codes |Cause  |Solution        |
|-----|------|------|
|32769  |Internal error|Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help.|
|32770  |Network error|Check if the device can be accessed via public network|
|32772  |Failed to parse the response packet|Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help.|
|32774  |The appinfo is not set|Check if the authentication key is correct, and if the offline voice is initialized.|
|32776  |Failed to verify authbuffer|Check if the authbuffer is correct|
|32784  |Voice-to-text converting parameter error|Check if the fileID parameter is empty in the codes|
|32785  |Error returned for voice-to-text conversion|There is an offline voice error in the backend. Analyze logs, obtain the real error code returned from the backend to the client, and ask backend personnel for help.|

#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//Process
		break;
	    }
		...
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
		{
		//Process
		break;
		}
	}
}
```



## Advanced APIs

### Obtain diagnostic messages
This API is used to obtain information about the quality of real-time audio/video calls. This API is mainly used to check the quality of real-time calls and troubleshoot problems, and can be ignored for this service.
#### Function prototype
```
ITMGRoom virtual const char* GetQualityTips()
```
#### Sample code  
```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();
```


### Obtain the version number
#### Function prototype

```
ITMGContext virtual const char* GetSDKVersion()
```



#### Sample code  

```
ITMGContextGetInstance()->GetSDKVersion();
```




### Set the print log level
This API is used to set the print log level. It is recommended to use default level.
#### Function prototype
```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### Parameter description

|Parameter|Type|Description|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|Sets the write log level. TMG_LOG_LEVEL_NONE indicates no write.|
|levelPrint|ITMG_LOG_LEVEL|Sets the print log level. TMG_LOG_LEVEL_NONE indicates no print.|



|ITMG_LOG_LEVEL|Description|
| -------------------------------|----------------------|
|TMG_LOG_LEVEL_NONE=0		|Do not print logs			|
|TMG_LOG_LEVEL_ERROR=1		|Prints error logs (default)	|
|TMG_LOG_LEVEL_INFO=2			|Prints prompt logs		|
|TMG_LOG_LEVEL_DEBUG=3		|Prints development and debugging logs	|
|TMG_LOG_LEVEL_VERBOSE=4		|Prints verbose logs		|

#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
context->SetLogLevel(0,true,true);
```



### Set the print log path
This API is used to set the print log path.
The default path is:

|Platform     |Path        |
| ------------- |:-------------:|
|Windows 	|%appdata%\Tencent\GME\ProcessName|
|iOS    		|Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android	|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    		|/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

#### Function prototype
```
ITMGContext virtual int SetLogPath(const char* logDir) 
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| logDir    		|char*    		|Path|

#### Sample code  

```
cosnt char* logDir = ""//You can set your own path

ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);
```

### Add an ID to the audio data blacklist
This API is used to add an ID to the audio data blacklist. A return value of 0 indicates that the call is successful.
#### Function prototype  

```
ITMGContext ITMGAudioCtrl int AddAudioBlackList(const char* openId)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| openId    |char*       |ID that needs to be added to the blacklist|

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->AddAudioBlackList(openId);
```

### Remove an ID from the audio data blacklist
This API is used to remove an ID from the audio data blacklist. A return value of 0 indicates that the call is successful.
#### Function prototype  

```
ITMGContext ITMGAudioCtrl int RemoveAudioBlackList(const char* openId)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| openId    |char*       |ID that needs to be removed from the blacklist|

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->RemoveAudioBlackList(openId);
```


## Callback Messages

#### Message list:

| Message     |Description of message|   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|Enters the audio room		|
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|Exits the audio room		|
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT		|Room disconnection due to network or other reasons	|
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE		|Room type change event		|
|ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    	|Adds a microphone		|
|ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    	|Loses a microphone		|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE	|Adds a speaker		|
|ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE	|Loses a speaker		|
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH		|The accompaniment is over			|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE		|The room members are updated		|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE	|PTT recording is completed			|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE	|PTT is successfully uploaded			|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|PTT is successfully downloaded			|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE		|The playback of PTT is completed			|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|The voice-to-text conversion is completed			|

#### Data list

|Message     | Data         |Example|
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|result; error_info			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|result; error_info  			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    	|result; error_info  			|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    	|result; error_info; sub_event_type; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"microphone (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    	|result; error_info 			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"microphone (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE    		|user_list;  event_id			|{"event_id":1,"user_list":["0"]}|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE 	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|result; text;file_id		|{"file_id":"","text":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE	|result; file_path; text;file_id		|{"file_id":"","file_path":","text":"","result":0}|
