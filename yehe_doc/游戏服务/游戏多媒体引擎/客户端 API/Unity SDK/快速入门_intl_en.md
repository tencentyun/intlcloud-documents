## Operation Scenarios	
This document describes how to access and debug the GME APIs for Unity.		
		
This document only describes the most important APIs to help you get started with GME. For more information on APIs, please see the [API documentation](https://intl.cloud.tencent.com/document/product/607/15228).
			
| Important API | Description |
| ------------- |:-------------:|
|Init    		| Initializes GME 	|
|Poll    		| Triggers event callback	|
|EnterRoom	 	| Enters room  		|
|EnableMic	 	| Enables mic 	|
|EnableSpeaker		| Enables speaker 	|

>?
>- Configure your project before using GME; otherwise, the SDK will not take effect.
>- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
>- GME APIs should be called in the same thread.
>- The `Poll` API should be called periodically for GME to trigger event callbacks.
>- For GME callback messages, please see the callback message list.
>- Operation on devices should be performed after successful room entry.
>- For detailed error codes, please see [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173).

## Access Steps
### 1. Initialize the SDK

For more information on how to get parameters, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/39698).

This API requires the `SDKAppID` from the Tencent Cloud Console and the `openID` as parameters. The `openID` uniquely identifies a user with the rules stipulated by the application developer and must be unique in the application (currently, only INT64 is supported).
>!The SDK must be initialized before a client can enter a room.
#### Function prototype

```
ITMGContext Init(string sdkAppID, string openID)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId    	|String  | `AppId` from the Tencent Cloud Console.				|
| openID    		|String  | `OpenID` can only be in Int64 type (converted to string) with a value greater than 10,000, which is used to identify the user. |

#### Sample code 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
// Determine whether the initialization is successful by the returned value
if (ret != QAVError.OK)
    {
        Debug.Log("SDK initialization failed:"+ret);
        return;
    }
```

### 2. Trigger event callback
The `Poll` API should be called periodically in `update` for GME to trigger event callbacks.
#### Function prototype

```
ITMGContext public abstract int Poll();
```
#### Sample code 

```
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### 3. Authenticate
Generate `AuthBuffer` for encryption and authentication of relevant features.  

>?To get authentication for voice messaging and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype
```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId    		|int   		| `AppId` from the Tencent Cloud Console.		|
| roomId    		|string   		| Room ID, which can contain up to 127 characters (for the voice messaging and speech-to-text feature, enter `null`). |
| openId    	|string 	| User ID, which is the same as `openID` during initialization.					|
| key    		|string 	| Permission key from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme).				|



#### Sample code  
```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}
```

### 4. Enter a room
This API is used to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry.

#### Function prototype
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId		|string    	| Room ID, which can contain up to 127 characters.					|
| roomType 	|ITMGRoomType		| Room audio type.		|
| authBuffer 	|Byte[] 	| Authentication key.					|

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code  
```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);
```

### 5. Receive callback for room entry
A callback will be required through a delegate function after room entry, which is composed of `result` and `error_info`.
#### Function prototype
```
Delegate function:
public delegate void QAVEnterRoomComplete(int result, string error_info);
Event function:
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

#### Sample code  
```
Listen on an event:
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

Process the event listened on:
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
  			ShowLoginPanel("error code:" + err + " error message:" + errInfo);
            return;
	}else{
		// Entered room successfully
    }
}
```


### 6. Enable/Disable the mic
This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.

>?
>- Please make sure that the mic permission has been granted in the project when executable files are exported for each platform and is enabled during use.
>- On a mobile device, you can use the `CheckMicPermission` API to check whether the mic permission is granted.

#### Function prototype  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | To enable the mic, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  
```
// Enable the mic
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```


### 7. Enable/Disable the speaker
This API is used to enable/disable the speaker.
#### Function prototype  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |bool       | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  
```
// Enable the speaker
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```
