This document helps Unreal developers debug and access APIs for Tencent Cloud's Game Multimedia Engine (GME).


This document only provides the most important APIs to help you get started with GME. For more APIs, see [API Documentation](https://intl.cloud.tencent.com/document/product/607/15231).


|Important API     | Description|
| ------------- |:-------------:|
|Init    		|Initializes GME 	|
|Poll    		|Triggers event callback	|
|EnterRoom	 	|Enters a room  		|
|EnableMic	 	|Enables the microphone 	|
|EnableSpeaker		|Enables the speaker 	|

>**Notes:**
- Configure the project before using GME, otherwise  SDK will not be valid.
- After a GME API is called successfully, AV_OK will be returned with a value of 0.
- GME APIs should be called in the same thread.
- Authentication is needed before entering a room. Refer to the authentication section in relevant documentation for more information.
- The Poll API should be called periodically to trigger event callback.
- Refer to the callback message list for callback information.
- Device related operations can only be done after entering a room.
- For error code details, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173)


## Quick Integration Directions
### 1. Get a singleton
This API is used to get the ITMGContext instance when using the voice feature.

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```



### 2. Initialize the SDK
For more information on getting parameters, see [Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).
SdkAppId is a required parameter and can be obtained from Tencent Cloud Console.  OpenId, which is a unique user identifier, is also required.  Its rules are set by application developers  and should be unique in the application (only INT64 value type is supported). 
>!You must initialize the SDK before entering a room.
#### Function prototype

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openID)
```

|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| sdkAppId    	|char*   	|The SdkAppId obtained from Tencent Cloud console					|
| openID    	|char*   	|The value type of OpenID only accepts Int64 (the value is converted and passed to the function as a string). OpenID is for identifying users and its value must be greater than 10000. 	|

#### Sample code 


```
std::string appid = TCHAR_TO_UTF8(CurrentWidget->editAppID->GetText().ToString().operator*());
std::string userId = TCHAR_TO_UTF8(CurrentWidget->editUserID->GetText().ToString().operator*());
ITMGContextGetInstance()->Init(appid.c_str(), userId.c_str());
```
### 3. Trigger event callback
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


### 4. Authentication information
AuthBuffer is generated for the purpose of encryption and authentication. For more information on the authentication data, refer to [GME Key](https://intl.cloud.tencent.com/document/product/607/12218).  
The room ID parameter for voice message must be set to "null".
#### Function prototype
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| dwSdkAppID    			|int   		|The SdkAppId obtained from the Tencent Cloud console		|
| strRoomID    		|char*     |Room ID; 127 characters maximum (The room ID parameter for voice message must be set to "null").|
| strOpenID  		|char*     	|User ID|
| strKey    			|char*	    	|The key obtained from the Tencent Cloud [Console](https://intl.cloud.tencent.com/login)					|
|strAuthBuffer		|char*	    	|Returned authbuff							|
| bufferLength   		|int    		|Length of returned authbuff. It is recommended to set it to 600.|



#### Sample code  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```


### 5. Enter a room
When you enter a room with the generated authentication credentials, you receive a callback indicating ITMG_MAIN_EVENT_TYPE_ENTER_ROOM. By default, microphone and speaker will not be enabled after you enter the room. If AV_OK is returned, it indicates the callback is successful.
- By default, microphone and speaker will not be enabled after you enter the room.
- The API Init should be called before the API EnterRoom.

#### Function prototype
```
ITMGContext virtual int EnterRoom(const char*  roomId, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)//API for entering a room in team chatting mode
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| roomId			| char*    		|Room ID; 127 characters maximum 	|
| roomType 			|ITMG_ROOM_TYPE	|Audio type of the room		|
| authBuffer    		|char*     	|Authentication key			|
| buffLen   			|int   		|Length of the authentication key		|

For the room audio type definition, refer to [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomId, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### 6. Callback for entering a room
ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received after a user enters a room, the action of this event should be implemented in the OnEvent function.

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

### 6. Enable/disable the microphone
This API is used to enable/disable the microphone. By default, microphone and speaker will not be enabled after a user enters a room.

#### Function prototype  
```
ITMGAudioCtrl virtual void EnableMic(bool bEnabled)
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| bEnabled    |bool     |To enable the microphone, set this parameter to true, otherwise, set it to false.|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```


### 8. Enable/Disable the speaker
This API is used to enable/disable the speaker.

#### Function prototype  
```
ITMGAudioCtrl virtual void EnableSpeaker(bool enabled)
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| enable   		|bool       	|To disable the speaker, set this parameter to false, otherwise, set it to true.|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```




