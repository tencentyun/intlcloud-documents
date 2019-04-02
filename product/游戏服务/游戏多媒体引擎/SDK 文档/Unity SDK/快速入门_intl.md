		
This article is a detailed description with the purpose of helping Unity developers debug and access APIs for Tencent Cloud's Game Multimedia Engine (GME).		
		
		
## How to Use		
![](https://main.qcloudimg.com/raw/810d0404638c494d9d5514eb5037cd37.png)		
		
						
This document only describes the most important APIs to help you get started with GME. For more APIs, see [API Documentation](https://intl.cloud.tencent.com/document/product/607/15228).			


| Important API | Description |
| ------------- |:-------------:|
| Init | Initializes GME |
|Poll    		| Triggers event callback	|
|EnterRoom	 	| Enters a room  		|
| EnableMic | Enables the microphone |
| EnableSpeaker | Enables the speaker |

>**Notes:**			
- For a successful GME API call, QAVError.OK is returned with a value of 0.		
- GME APIs are called in the same thread.
- The request for entering a room via GME API should be authenticated. For more information, see authentication section in relevant documentation.		
- The Poll API should be called periodically to trigger event callback.
- See the callback message list for GME callback information.
- The operation on devices shall be carried out after successful entry into a room.
## Procedure for Quick Integration


### 1. Initialize the SDK
For more information on how to obtain parameters, see [Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).		
This API should contain SdkAppId and openId. The SdkAppId is obtained from the Tencent Cloud console, and the openId is used to uniquely identify a user. The setting rule for openId can be customized by App developers, and this ID must be unique in an App (only INT64 is supported).
SDK must be initialized before a user can enter a room.

#### Function prototype
```
ITMGContext Init(string sdkAppID, string openID)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId    	|String  | The SdkAppId obtained from the Tencent Cloud Console				|
| openID |String | The OpenID only supports Int64 type(should be converted to String type for passing the api argument). It is used to identify the user and the value should be greater than 10000.|

#### Sample code  
```
int ret = ITMGContext.GetInstance().Init(str_appId, str_userId);
	if (ret != QAVError.OK) {
		return;
	}
```

### 2. Trigger event callback
The Poll API should be called periodically to trigger event callback.
#### Function prototype

```
ITMGContext public abstract int Poll();
```

### 3. Enter a room
This API is used to enter a room with the generated authentication information. Microphone and speaker are not enabled by default after a user enters the room.


#### Function prototype
```
ITMGContext EnterRoom(string roomID, int roomType, byte[] authBuffer)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomID | string | Room ID, which is limited to 127 characters |
| roomType | ITMGRoomType | Audio type of the room |
| authBuffer | Byte[] | Authentication key |

For more information about room's audio types, see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).
  
#### Sample code  
```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

### 4. Callback for entering a room
A callback with a delegate function is required after a user enters a room. The callback is composed of result and error_info.
#### Function prototype
```
Delegate function:
public delegate void QAVEnterRoomComplete(int result, string error_info);
Event function:
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

#### Sample code
```
Listen for an event:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

Process the event after listening:
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
	    ShowWarnning (string.Format ("join room failed, err:{0}, errInfo:{1}", err, errInfo));
	    return;
	}else{
	    ShowWarnning (string.Format ("The current room id:{0}. Enter this room from another device for a chat.",roomId ));
    }
}
```

### 5. Enable/Disable the microphone
This API is used to enable/disable the microphone. Microphone and speaker are not enabled by default after a user enters a room.

#### Function prototype  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | true: enable microphone; false: disable microphone. |

#### Sample code  
```
Enable the microphone
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```


### 6. Enable/Disable the speaker
This API is used to enable/disable the speaker.
#### Function prototype  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | true: enable speaker; false: disable speaker. |

#### Sample code  
```
Enable the speaker
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

## Authentication
### Authentication information

This API is used to generate AuthBuffer for encryption and authentication. For more information on deployment at backend, see [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).          
To obtain authentication for voice message, enter "null" for the room ID parameter.
A value of Byte[] type is returned for this API.
#### Function prototype

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId    		|int   		| The SdkAppId obtained from the Tencent Cloud Console |
| roomId | string | Room ID, which is limited to 127 characters |
| openId | String | User ID |
| key    		|string 	| The key obtained from the Tencent Cloud [Console](https://intl.cloud.tencent.com/login) 				|

#### Sample code  

```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId, userId, "a495dca2482589e9");
}
```


