This document provides an overview that makes it easy for Windows developers to debug and integrate the APIs for Game Multimedia Engine.


## How to Use
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)


This document only provides the most important APIs to help you get started with GME. For more APIs, see [API Documentation](https://intl.cloud.tencent.com/document/product/607/15232).


| Important API | Description |
| ------------- |-------------|
| Init | Initializes GME |
| Poll | Triggers event callback |
| EnterRoom | Enters a room |
| EnableMic | Enables the microphone |
| EnableSpeaker | Enables the speaker |

>**Notes:**
- When a GME API is called successfully, QAVError.OK is returned, and the value is 0.
- GME APIs are called in the same thread.
- The request for entering a room via GME API should be authenticated. For more information, see authentication section in relevant documentation.
- The Poll API is called periodically for GME to trigger event callback.
- See the callback message list for GME callback information.
- The operation on devices shall be carried out after successful entry into a room.


## Procedure for Quick Integration

### 1. Get a singleton
To use the voice feature, get the ITMGContext object first.

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```



### 2. Initialize the SDK
For more information on how to obtain parameters, see [Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).
This API need SdkAppId from console as parameter. OpenId is also needed as a unique user identifier. Setting rule for openId can be customized by App developers and must be unique in an app. Currently, only INT64 is supported.
SDK must be initialized before a user can enter a room.
#### Function prototype

```
ITMGContext virtual void Init(const char* sdkAppId, const char* openId)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId | char* | The SdkAppId obtained from the Tencent Cloud Console |
| openID | char* | The OpenID only supports Int64 type(should be converted to String type for passing the api argument). It is used to identify the user and the value should be greater than 10000.|

#### Sample code 
```
#define SDKAPPID3RD "1400035750"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```

### 3. Trigger event callback
Event callbacks can be triggered by periodically calling Poll in "update".
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
ITMGContextGetInstance()->Poll();
```

### 4. Enter a room
When you enter a room with the generated authentication information, the ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received as a callback.
- Microphone and speaker are not enabled by default after a user enters the room.
- The API Init should be called before the API EnterRoom.

#### Function prototype
```
ITMGContext virtual int EnterRoom(const char*  roomId, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)//API for entering a room in team chatting mode
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId | char* | Room ID, which is limited to 127 characters |
| roomType | ITMG_ROOM_TYPE | Audio type of the room |
| authBuffer | char* | Authentication key |
| buffLen | int | Length of the authentication key |

For more information about room's audio types, see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomId, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### 5. Callback for entering a room
The ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is returned after a user enters a room, which is checked in the OnEvent function.
#### Sample code  
```


//Implementation
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

### 6. Enable/Disable the microphone
This API is used to enable/disable the microphone. Microphone and speaker are not enabled by default after a user enters a room.

#### Function prototype  
```
ITMGAudioCtrl virtual void EnableMic(bool bEnabled)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| bEnabled | bool | To enable the microphone, set this parameter to true, otherwise set it to false. |

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```


### 7. Enable/Disable the speaker
This API is used to enable/disable the speaker.

#### Function prototype  
```
ITMGAudioCtrl virtual void EnableSpeaker(bool enabled)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable | bool | To disable the speaker, set this parameter to false, otherwise set it to true. |

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```


## Authentication
### Authentication information
This API is used to generate AuthBuffer for encryption and authentication. For more information on deployment at backend, see [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).  
To obtain authentication for voice message, enter "null" for the room ID parameter.

#### Function prototype
```
QAVSDK_AUTHBUFFER_API int QAVSDK_AUTHBUFFER_CALL QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| dwSdkAppID | int | The sdkAppID obtained from the Tencent Cloud Console |
| strRoomID | char*  | Room ID, which is limited to 127 characters (The room ID parameter for voice message must be set to null.) |
| strOpenID | char*   | User ID |
| strKey | char* | The key obtained from the Tencent Cloud [Console](https://intl.cloud.tencent.com/login) |
| strAuthBuffer | char* | Returned authbuff |
| buffLenght | int   | Length of passed authbuff. 500 is recommended. |



#### Sample code  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```




