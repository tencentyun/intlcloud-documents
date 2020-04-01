This document describes how to get started with the GME APIs for Windows.


This document only describes the most important APIs to help you get started with GME. For more information on APIs, please see the [API documentation](https://intl.cloud.tencent.com/document/product/607/15210).


| Important API | Description |
| ------------- |:-------------:|
|Init    		| Initializes GME 	|
|Poll    		| Triggers event callback	|
|EnterRoom	 	| Enters room  		|
|EnableMic	 	| Enables mic 	|
|EnableSpeaker		| Enables speaker 	|

>
- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `AV_OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For GME callback messages, please see the callback message list.
- Operation on devices should be performed after successful room entry.
- For detailed error codes, please see [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173).


## Directions for Quick Access
### 1. Get a singleton
To use the voice feature, get the `ITMGContext` object first.

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->SetTMGDelegate(this);
```



### 2. Initialize the SDK
For more information on how to get parameters, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/10782).
This API requires the `AppID` from the Tencent Cloud Console and the `openID` as parameters. The `openID` uniquely identifies a user with the rules stipulated by the application developer and must be unique in the application (currently, only INT64 is supported).
>The SDK must be initialized so that a room can be entered.
#### Function prototype

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId    	|char*   	| `AppId` from the Tencent Cloud Console 					|
| openId    	|char*   	| `OpenID` can only be in Int64 type (converted to char*) with a value greater than 10,000, which is used to identify the user 	|


| Returned Value | Description |
|----|----|
|QAVError.OK| Initialized SDK successfully. |
|7015 AV_ERR_SDK_NOT_FULL_UPDATE| Check whether the SDK file is complete. You are recommended to delete it and then import the SDK again. |

#### Sample code 


```
#define SDKAPPID3RD "1400089356"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```
### 3. Trigger event callback
Event callbacks can be triggered by periodically calling the `Poll` API in `update`.
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


### 4. Authenticate
Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    
To get authentication for voice messaging and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype
```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| dwSdkAppID    			|int   		| `AppId` from the Tencent Cloud Console.		|
| strRoomID    		|char*     | Room ID, which can contain up to 127 characters (for voice messaging and speech-to-text feature, enter `null`). |
| strOpenID  		|char*     	| User ID, which is the same as `openID` during initialization. |
| strKey    			|char*	    	| Permission key from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme).					|
|strAuthBuffer		|char*	    	| Returned `authbuff`.							|
| bufferLength   		|int    		| Length of the `authbuff` passed in. 500 is recommended. 						|




#### Sample code  
```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```


### 5. Enter a room
When a client enters a room with the generated authentication information, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` message will be received as a callback. Mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates a success.


#### Function prototype
```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomID			| char*    		| Room ID, which can contain up to 127 characters	|
| roomType 			|ITMG_ROOM_TYPE	| Room audio type		|
| authBuffer    		|char*     	| Authentication key			|
| buffLen   			|int   		| Authentication key length		|

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code  
```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### 6. Receive callback for room entry
After the client enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function.

#### Sample code  
```

void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		// Process
		break;
		}
	}
}
```

### 7. Enable/Disable the mic
This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.

#### Function prototype  
```
ITMGAudioCtrl virtual int EnableMic(bool bEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| bEnabled    |bool     | To enable the mic, set this parameter to `true`; otherwise, set it to `false`.		|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```


### 8. Enable/Disable the speaker
This API is used to enable/disable the speaker.

#### Function prototype  
```
ITMGAudioCtrl virtual int EnableSpeaker(bool enabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable   		|bool       	| To disable the speaker, set this parameter to `false`; otherwise, set it to `true`.	|

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```



