This document helps Unity developers debug and access APIs for Tencent Cloud's Game Multimedia Engine (GME).

This document only provides the most important APIs to help you get started with GME. For more APIs, see [API Documentation](https://intl.cloud.tencent.com/document/product/607/15228).
			
|Important API     | Description|
| ------------- |:-------------:|
|Init    		|Initializes GME 	|
|Poll    		|Triggers event callback	|
|EnterRoom	 	|Enters a room  		|
|EnableMic	 	|Enables the microphone 	|
|EnableSpeaker		|Enables the speaker 	|

>**Notes:**			
- Configure the project before using GME, otherwise the SDK is not valid.
- After a GME API is called successfully, QAVError.OK will be returned with a value of 0.
- GME APIs should be called in the same thread.
- Authentication is needed before entering a room. Refer to the authentication section in relevant documentation for more information.
- The Poll API should be called periodically to trigger event callback.
- Refer to the callback message list for callback information.
- Device related operations can only be done after entering a room.
- For error code details, see [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173)

## Quick Integration Directions
### 1. Initialize the SDK
For more information about getting parameters, see [Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).
SdkAppId and openId are the required parameters for requesting this API, where openId is for identifying a user and must be unique in an Application (only INT64 value type is supported). You can get SdkAppId from Tencent Cloud Console, and set rules for creating openId as a developer.
You must initialize the SDK before entering a room.
#### Function prototype

```
ITMGContext Init(string sdkAppID, string openID)
```

|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| sdkAppId    	|String  |The SdkAppId obtained from Tencent Cloud console				|
| openID    		|String  |The value type of OpenID only accepts Int64 (the value is converted and passed to the function as a string). OpenID is for identifying users and its value must be greater than 10000.|

#### Sample code 

```
int ret = ITMGContext.GetInstance().Init(str_appId, str_userId);
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

### 3. Authentication information
AuthBuffer is generated for the purpose of encryption and authentication. For more information about the authentication data, refer to [GME Key](https://intl.cloud.tencent.com/document/product/607/12218).    
The room ID parameter for voice message must be set to "null".

#### Function prototype
```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| appId    		|int   		|The SdkAppId obtained from Tencent Cloud console		|
| roomId    		|string   		|Room ID, maximum to 127 characters (The room ID parameter for voice message must be set to "null").|
| openID    	|string 	|User ID					|
| key    		|string 	|The key obtained from the Tencent Cloud [Console](https://intl.cloud.tencent.com/login)				|


#### Sample code  
```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId, userId, "a495dca2482589e9");
}
```
### 4. Enter a room
This API is used to enter a room with the generated authentication credentials. By default, microphone and speaker will not be enabled after you enter the room.


#### Function prototype
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| roomId		|string    	|Room ID, maximum to 127 characters					|
| roomType 	|ITMGRoomType		|Audio type of the room		|
| authBuffer 	|Byte[] 	|Authentication key					|

For the room audio type definition, refer to [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code  
```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

### 5. Callback for entering a room
The delegate function is used for callback after a user enters a room. The passed parameter includes result and error_info.
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
	    ShowWarnning (string.Format ("The current audio room id:{0}. Please enter this room from another device for an audio chat.",roomId ));
    }
}
```

### 6. Enable/disable the microphone
This API is used to enable/disable the microphone. By default, microphone and speaker will not be enabled after a user enters a room.

#### Function prototype  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |To enable the microphone, set this parameter to true, otherwise, set it to false.|

#### Sample code  
```
Enable the microphone
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```


### 7. Enable/disable the speaker
This API is used to enable/disable the speaker.
#### Function prototype  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|Parameter     |Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |To disable the speaker, set this parameter to false, otherwise set it to true.|

#### Sample code  
```
Enable the speaker
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```


