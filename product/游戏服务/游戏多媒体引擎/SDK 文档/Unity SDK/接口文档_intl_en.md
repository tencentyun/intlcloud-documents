This document describes the integration for Unit to help Unity developers debug and integrate APIs for Tencent Cloud's Game Multimedia Engine (GME).


## Key Considerations for Using GME

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

### Obtain the instance
Obtain the Context instance using ITMGContext instead of QAVContext.GetInstance().

### Initialize the SDK

For more information on getting parameters, see [Integration Guide](https://intl.cloud.tencent.com/document/product/607/10782).
SdkAppId and openId are the required parameters for requesting this API, where openId is for identifying a user and must be unique in an Application (only INT64 value type is supported). You can get SdkAppId from Tencent Cloud Console, and set rules for creating openId as a developer.
You must initialize the SDK before entering a room.
#### Function prototype

```
ITMGContext Init(string sdkAppId, string openId)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| sdkAppId    	|String  |The SdkAppId obtained from Tencent Cloud console				|
| openId    		|String  |The value type of OpenID only accepts Int64 (the value is converted and passed to the function as a string). OpenID is for identifying users and its value must be greater than 10000.|

#### Sample code 


```
int ret = ITMGContext.GetInstance().Init(str_appId, str_openID);
	if (ret != QAVError.OK) {
		return;
	}
```
### Trigger event callback
The Poll API should be called periodically to trigger event callback.
#### Function prototype

```
ITMGContext public abstract int Poll();
```
### Pause the system
This API is used to notify the engine for Pause when the system Pause occurs.
#### Function prototype

```
ITMGContext public abstract int Pause()
```

### Resume the system
This API is used to notify the engine for Resume when the system Resume occurs. The Resume API is only used to resume real-time voice.
#### Function prototype

```
ITMGContext  public abstract int Resume()
```



### Uninitialize the SDK
This API is used to uninitialize the SDK. Uninitialization is needed when switching accounts.
#### Function prototype

```
ITMGContext public abstract int Uninit()
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
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| appId    		|int   		|The SdkAppId obtained from Tencent Cloud console		|
| roomId    		|string   		|Room ID; 127 characters maximum (The room ID parameter for voice message must be set to "null").|
| openID    	|string 	|User ID					|
| key    		|string 	|The key obtained from the Tencent Cloud [Console](https://intl.console.cloud.tencent.com/gamegme)				|


#### Sample code  
```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId,openID, "a495dca2482589e9");
}
```



### Enter a room
This API is used to enter a room with the generated authentication credentials. By default, microphone and speaker will not be enabled after you enter the room.

For more information on how to access range voice, see the [Range Voice](https://intl.cloud.tencent.com/document/product/607/17972).


#### Function prototype
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| roomId		|string    	|Room ID; 127 characters maximum					|
| roomType 	|ITMGRoomType		|Audio type of the room		|
| authBuffer 	|Byte[] 	|Authentication key					|

For the room audio type definition, refer to [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code  
```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

### Callback for entering a room
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

### Identify whether the user has entered the room successfully
This API is called to identify whether the user has entered the room successfully, and returns a boolean value.
#### Function prototype  
```
ITMGContext abstract bool IsRoomEntered()
```
#### Sample code  
```
ITMGContext.GetInstance().IsRoomEntered();
```

### Exit a room
This API is called to exit the current room. It is an async API. The returned value of AV_OK indicates a successful async delivery.

>If a user enters the room immediately after exiting a room in the application, the developer does not have to wait for the RoomExitComplete notification as a callback of ExitRoom in the API call process, but just calls the API directly.

#### Function prototype  
```
ITMGContext ExitRoom()
```
#### Sample code  
```
ITMGContext.GetInstance().ExitRoom();
```

### Callback for exiting a room
Callback is executed after a user exits the room, and the delegate function is used to pass the message.
#### Function prototype  
```
Delegate function:
public delegate void QAVExitRoomComplete();
Event function:
public abstract event QAVExitRoomComplete OnExitRoomCompleteEvent; 
```
#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().OnExitRoomCompleteEvent += new QAVExitRoomComplete(OnExitRoomComplete);
Process the event after listening:
void OnExitRoomComplete(){
    //Send a callback after a user exits the room
}
```

### Obtain the audio type of the user's room
This API is used to obtain the audio type of the user's room. The returned value is the audio type of the room. Returned value of 0 means an error occurred. The audio type definition can be found in the API EnterRoom.

#### Function prototype  
```
ITMGContext ITMGRoom public  int GetRoomType()
```

#### Sample code  
```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### Modify the audio type of the user's room
This API is used to modify the audio type of the user's room.
#### Function prototype  
```
ITMGContext ITMGRoom public void ChangeRoomType(ITMGRoomType roomtype)
```


|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| roomtype    |ITMGRoomType    |The room type to be switched to. See the API EnterRoom for the audio type definition.|

#### Sample code  
```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```



### Callback for changing the audio type of the user's room
This API is used to set the room type, and the delegate function is used to pass the message.

|Returned Parameter     | Description  |
| ------------- |:-------------:|
| result    |Value 0 represents success|
| error_info    |In case of failure, an error message will be passed|

```
Delegate function:
public delegate void QAVOnChangeRoomtypeCallback(int result, string error_info);

Event function:
public abstract event QAVCallback OnChangeRoomtypeCallback; 
```

#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().OnChangeRoomtypeCallback += new QAVOnChangeRoomtypeCallback(OnChangeRoomtypeCallback);
Process the event after listening:
void OnChangeRoomtypeCallback(int result, string error_info){
    //Send a callback after the room type has been set
}
```

### Notification of room type change
This API is used to allow you or other users in a room to modify the room type. This callback function is called whenever the room type changes, which is used to notify the App layer of such change. The room type definition can be found in the API EnterRoom.
```
Delegate function:
public delegate void QAVOnRoomTypeChangedEvent(int roomtype);

Event function:
public abstract event QAVOnRoomTypeChangedEvent OnRoomTypeChangedEvent;	
```
#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().OnRoomTypeChangedEvent += new QAVOnRoomTypeChangedEvent(OnRoomTypeChangedEvent);
Process the event after listening:
void OnRoomTypeChangedEvent(int roomtype){
    //Send a callback after the room type has been changed
}
```



### Member status change
Notification about this event is sent only when the member status changes. To obtain the member status in real time, cache the notification when receiving it at a higher layer. The event message ITMG_MAIN_EVNET_TYPE_USER_UPDATE is returned. The "data" includes event_id, count and openIdList. Identify the event message in the OnEvent function.
These events will only be sent when exceeding a certain threshold. For example, when audio data of a user is not received for more than two seconds, the ITMG_EVENT_ID_USER_NO_AUDIO will be sent.

|event_id     | Description         |What is maintained at the App side|
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				|A member enters the room			|Member list		|
|ITMG_EVENT_ID_USER_EXIT    				|A member exits the room			|Member list		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		|A member sends audio packages		|Chat member list	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			|A member stops sending audio packages	|Chat member list	|

#### Sample code
```
Delegate function:
public delegate void QAVEndpointsUpdateInfo(int eventID, int count, [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)]string[] openIdList);
Event function:
public abstract event QAVEndpointsUpdateInfo OnEndpointsUpdateInfoEvent;

Listen for an event:
ITMGContext.GetInstance().OnEndpointsUpdateInfoEvent += new QAVEndpointsUpdateInfo(OnEndpointsUpdateInfo);
Process the event after listening:
void OnEndpointsUpdateInfo(int eventID, int count, string[] openIdList)
{
    //Process

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

```


### Quality monitoring events
The message for quality monitoring event is ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY. The returned parameters include weight, floss, and delay, which represent the following information and the action of this event should be implemented in the OnEvent function.

|Parameter     | Description         |
| ------------- |-------------|
|weight    				|Its value ranges from 1 to 5 The value of 5 indicates excellent quality of audio packets, and the value of 1 indicates poor quality of audio packets, which can barely be used; and 0 represents an initial value and is meaningless.|
|floss    				|Packet loss|
|delay    		|Voice chat delay (ms)|


## Audio APIs for Voice Chat
The APIs for Voice Chat can only be called after the SDK is initialized and you are in the room.
We recommend the following methods when enabling/disabling the microphone or speaker on the user page:
- For most game apps, call EnableMic and EnableSpeaker APIs. Because calling EnableMic is equivalent to calling EnableAudioCaptureDevice and EnableAudioSend at the same time, and calling EnableSpeaker is equivalent to calling EnableAudioPlayDevice and EnableAudioRecv at the same time.
- For other mobile apps such as social networking apps, enabling/disabling a capturing device will restart both the capturing and the playback devices. If the App is playing background music, it will also be interrupted. But if the microphone is enabled/disabled through control of upstream/downstream, playback will not be interrupted. So the calling method is: Call EnableAudioCaptureDevice(true) and EnableAudioPlayDevice(true) once after entering the room, and call EnableAudioSend/Recv to send/receive audio streams when the microphone button is clicked to enable or disable.
- If you wish to release the capture or the playback device separately, please refer to the EnableAudioCaptureDevice and EnableAudioPlayDevice API.
- Call Pause to pause the audio engine and Resume to resume the audio engine.

| API     | Description   |
| ------------- |:-------------:|
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



### Enable/disable the microphone
This API is used to enable/disable the microphone. By default, microphone and speaker will not be enabled after a user enters a room.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
#### Function prototype  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |To enable the microphone, set this parameter to true, otherwise, set it to false.|

#### Sample code  
```
Enable the microphone
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```

### Obtain the microphone status
This API is used to obtain the microphone status. "0" means microphone is disabled, "1" means microphone is enabled.
#### Function prototype  
```
ITMGAudioCtrl GetMicState()
```
#### Sample code  
```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### Enable/disable audio capture device
This API is used to enable/disable the audio capture device. The audio capture device is not enabled by default.
- API can only be called after the room is entered.The device will disabled automatically after exiting the room.
- For mobile use case, permission is normally asked when enabling the capture device.

#### Function prototype  
```
ITMGAudioCtrl int EnableAudioPlayDevice(bool isEnabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |true means enable, false means disable|

#### Sample code

```
Enable a capturing device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### Obtain the audio capture device status
This API is used to obtain the audio capture device status.
#### Function prototype

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```
#### Sample code

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### Enable/disable the audio sending
This API is used to enable/disable the audio sending. Enable means sending the captured voice.

#### Function prototype

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |true means enable audio sending, false means not|

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### Obtain status on if captured audio is being sent
This API is called to obtain the status if captured audio is being sent.
#### Function prototype  
```
ITMGAudioCtrl bool IsAudioSendEnabled()
```
#### Sample code  
```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### Obtain real-time microphone volume
This API is used to obtain real time microphone volume. An int value is returned.
#### Function prototype  
```
ITMGAudioCtrl int GetMicLevel
```
#### Sample code  
```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### Obtain real-time volume of audio sending
This API is used to obtain real-time volume of audio sending. An int value is returned, ranging from 0 to 100.
#### Function prototype  
```
ITMGAudioCtrl int GetSendStreamLevel()
```
#### Sample code  
```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetSendStreamLevel();
```

### Set software volume for the microphone
This API is used to set software volume for the microphone. The value "0" means Mute, and "100" means the volume remains unchanged. Default value is 100.

#### Function prototype  
```
ITMGAudioCtrl SetMicVolume(int volume)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| volume    |int      |Sets the volume, value range: 0 to 200|

#### Sample code  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```
### Obtain software volume for the microphone
This API is used to obtain the software volume for the microphone. An int value is returned to indicate the software volume for the microphone. Returned value of 101 means SetMicVolume() has not been called.

#### Function prototype  
```
ITMGAudioCtrl GetMicVolume()
```
#### Sample code  
```
ITMGContext.GetInstance().GetAudioCtrl().GetMicVolume();
```

### Enable/disable the speaker
This API is used to enable/disable the speaker.
EnableSpeaker = EnableAudioPlayDevice + EnableAudioRecv.
#### Function prototype  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |To disable the speaker, set this parameter to false, otherwise set it to true|

#### Sample code  
```
Enable the speaker
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```

### Obtain the speaker status
This API is used to obtain the speaker status. "0" means speaker is disabled, "1" means speaker is enabled, "2" means speaker is currently in use.
#### Function prototype  
```
ITMGAudioCtrl GetSpeakerState()
```

#### Sample code  
```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```



### Enable/disable audio playback device
This API is used to enable/disable audio playback device.

#### Function prototype  
```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |true means enable, false means disable|

#### Sample code  
```
Enable a playback device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```

### Obtain audio playback device status
This API is used to obtain the status of audio playback device.
#### Function prototype

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```
#### Sample code  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### Enable/disable the audio receiving
This API is used to enable/disable the audio receiving. If the device has been enabled, the audio of other members in the room will be played. Otherwise, there will be no playback. For enabling/disabling playback device, see the EnableAudioPlayDevice API.

#### Function prototype  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| isEnabled    |bool     |true means enabling the audio receiving. false means not|

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```



### Obtain status on if received audio is being played
This API is called to obtain the status if received audio is being played.
#### Function prototype  
```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### Sample code  
```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```

### Obtain real-time speaker volume
This API is used to obtain real time speaker volume. An int value is returned to indicate the real-time speaker volume.
#### Function prototype  
```
ITMGAudioCtrl GetSpeakerLevel()
```

#### Sample code  
```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### Obtain real-time volume of audio receiving of other members in the room
This API is used to obtain real-time volume of audio receiving of other members in the room. The return value is int type, which ranges from 0 to 100.
#### Function prototype  
```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| openId    |string       |openId of other members in the room|

#### Sample code  
```
int Level = ITMGContext.GetInstance().GetAudioCtrl().GetRecvStreamLevel(openId);
```

### Set software volume for the speaker
This API is used to set the software volume for the speaker.
The value "0" means Mute, and "100" means the volume remains unchanged. Default value is 100.

#### Function prototype  
```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| volume    |int        |Sets the volume, value range: 0 to 200|

#### Sample code  
```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### Obtain software volume for the speaker

This API is used to obtain the software volume for the speaker. An int value is returned to indicate the software volume for the speaker. Returned value of 101 means SetSpeakerVolume() has not been called.
"Level" indicates the real-time volume, and "Volume" the is software volume for the speaker. The ultimate volume equals to Level*Volume%. For example, if the value for "Level" is 100 and the one for "Volume" is 60, the ultimate volume will be "60".

#### Function prototype  
```
ITMGAudioCtrl GetSpeakerVolume()
```
#### Sample code  
```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerVolume();
```


### Enable in-ear monitoring
This API is used to enable in-ear monitoring.
#### Function prototype  
```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| enable    |bool         |Specifies whether to enable in-ear monitoring|

#### Sample code  
```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### Callback for device occupation and release
Callback is executed after a device is occupied or released, and the delegate function is used to pass the message.

```
Delegate function:
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
Event function:
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| deviceType    	|int       	|1 indicates a capturing device. 2 indicates a playback device							|
| deviceId   	 	|string 	|Device GUID, which is used to mark a device and only valid on Windows and Mac.	|
| openOrClose    |bool  	|Occupies or releases a capturing/playback device							|


|Parameter     | Value         |Description|
| ------------- |:-------------:|-------------|
| AUDIODEVICE_CAPTURE    	|1       	|Indicates a capturing device|
| AUDIODEVICE_PLAYER   	 	|2 			|Indicates a playback device|

#### Sample code  

```
Listen for an event:
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
Process the event after listening:
void QAVAudioDeviceStateCallback(int deviceType, string deviceId, bool openOrClose){
    //Callback for device occupation and release
}
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
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| authBuffer    |byte[]                   |Authentication data|

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().ApplyPTTAuthbuffer(authBuffer);
```

### Specify the maximum length of a voice message
This API is used to specify the maximum length of a voice message. The maximum duration is 60 seconds.

#### Function prototype

```
ITMGPTT int SetMaxMessageLength(int msTime)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| msTime    |int                    |Indicates the length of a voice message in millisecond|

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().SetMaxMessageLength(60000); 
```


### Start recording
TThis API is used to start recording. Recording files should be uploaded before you can conduct  voice-to-text and other operations.
#### Function prototype  
```
ITMGPTT int StartRecording(string fileDir)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| fileDir    |string                      |Indicates the path for storing the voice file|

#### Sample code  
```
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);
```

### Callback for starting recordings
Callback is executed after recording, and the delegate function is used to pass the message.
#### Function prototype  
```
Delegate function:
public delegate void QAVRecordFileCompleteCallback(int code, string filepath); 
Event function:
public abstract event QAVRecordFileCompleteCallback OnRecordFileComplete;
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| code    |string                      |When code is 0, recording is completed|
| filepath    |string                      |Path for storing the recorded file|

#### Error codes
|Error Codes |Cause  |Solution        |
|-----|------|------|
|4097   |Empty parameter|Check if the API parameters in the codes are correct|
|4098   |Initialization error|Check if the device is occupied, the permissions are normal, and the initialization is normal.|
|4099   |Recording is in process|Ensure the SDK recording feature is used at the right time|
|4100   |Audio data is not collected|Check if the microphone works properly|
|4101   |File access error while recording|Ensure the file exists and its path is valid|
|4102   |The microphone is not authorized|Microphone permission is required for using SDK. To add the permission, see SDK project configuration document for the applicable engine or platform.|
|4103   |The recording time is too short|The recording time should be in millisecond and longer than 1 second|
|4104   |No recording start operation|Check if the start recording API is called|

#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnRecordFileComplete +=  new QAVRecordFileCompleteCallback (OnRecordFileComplete);
Process the event after listening:
void OnRecordFileComplete(int code, string filepath){
    //Callback for starting recordings
}
```

### Enable streaming speech recognition
This API is used to start streaming speech recognition. Texts obtained from voice-to-text conversion will be returned in real time in its callback. It can also be used to translate specified information in an audio and return the text.

#### Function prototype  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string translateLanguage,string translateLanguage) 
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| filePath			|String	|Indicates the path for storing the voice file	|
| speechLanguage    		|String	|Recognizes specified language. See [language reference list](https://intl.cloud.tencent.com/document/product/607/30260)|
| translateLanguage	|String	|Translates into specified language. See [language reference list](https://intl.cloud.tencent.com/document/product/607/30260) (This parameter is not available. Enter the value for speechLanguage.) |

#### Sample code  
```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN","cmn-Hans-CN");
```

### Callback for streaming speech recognition
Callback is executed after recognition is finished, and the delegate function is used to pass the message.
```
Delegate function:
public delegate void QAVStreamingRecognitionCallback(int code, string fileID, string filepath, string result);
Event function:
public abstract event QAVStreamingRecognitionCallback OnStreamingSpeechComplete;
```

|Message Name     | Description         |
| ------------- |:-------------:|
| code    	|Error code indicating whether streaming speech recognition is successful		|
| result    		|Text obtained from voice-to-text conversion	|
| filepath 	|Local path for the recorded voice file		|
| fileid 		|URL for the recorded voice file uploaded to server	|

|Error Code     | Description         |Solution|
| ------------- |:-------------:|:-------------:|
|32775	|Recording is successful but streaming voice to text failed	|Call the API UploadRecordedFile to upload the recording, and then call the API SpeechToText to perform voice-to-text conversion.
|32777	|Recording and uploading is successful, but streaming voice to text is failed.	|The message returned includes a URL for successful upload. Call the SpeechToText API to perform voice-to-text conversion.

#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete +=new QAVStreamingRecognitionCallback (OnStreamingSpeechComplete);
Process the event after listening:
void OnStreamingSpeechComplete(int code, string fileid, string filepath, string result){
    //Callback for starting streaming recordings
}

```

### Pause recording
This API is used to pause recording. To resume recording, call the ResumeRecording API.

#### Function prototype  
```
ITMGPTT int PauseRecording()
```
#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().PauseRecording();
```

### Resume recording
This API is used to resume recording.

#### Function prototype  
```
ITMGPTT int ResumeRecording()
```
#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().ResumeRecording();
```


### Stop recording
This API is used to stop recording. This is an async API. There will be a callback after the recording is stopped. Only when the recording is successful can the recorded file be used.
#### Function prototype  
```
ITMGPTT int StopRecording()
```
#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```



### Cancel recording
This API is used to cancel recording. There will not be a callback after the cancellation.
#### Function prototype  
```
ITMGPTT int CancelRecording()
```
#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().CancelRecording();
```

### Obtain real-time microphone volume of offline voice
This API is used to obtain real-time microphone volume of offline voice. An int value is returned, ranging from 0 to 100.

#### Function prototype  
```
ITMGPTT int GetMicLevel()
```
#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().GetMicLevel();
```


### Set recording volume of offline voice
This API is used to set recording volume of offline voice. The value ranges from 0 to 100.

#### Function prototype  
```
ITMGPTT int SetMicVolume(int vol)
```
#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().SetMicVolume(100);
```

### Obtain recording volume of offline voice
This API is used to obtain recording volume of offline voice. An int value is returned, ranging from 0 to 100.

#### Function prototype  
```
ITMGPTT int GetMicVolume()
```

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().GetMicVolume();
```
### Obtain real-time speaker volume
This API is used to obtain real-time speaker volume. An int value is returned, ranging from 0 to 100.

#### Function prototype  
```
ITMGPTT int GetSpeakerLevel()
```

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerLevel();
```



### Set playback volume of offline voice
This API is used to set playback volume of offline voice. The value ranges from 0 to 100.

#### Function prototype  
```
ITMGPTT int SetSpeakerVolume(int vol)
```
#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().SetSpeakerVolume(100);
```

### Obtain playback volume of offline voice
This API is used to obtain playback volume of offline voice. An int value is returned, ranging from 0 to 100.

#### Function prototype  
```
ITMGPTT int GetSpeakerVolume()
```

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerVolume();
```

### Upload voice files
This API is used to upload voice files.
#### Function prototype  
```
ITMGPTT int UploadRecordedFile (string filePath)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| filePath    |string                      |Indicates the path of the voice files to be uploaded|

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().UploadRecordedFile(filePath);
```


### Callback for uploading voice files
Callback is executed after a voice file has been uploaded, and the delegate function is used to pass the message.
#### Function prototype
```
Delegate function:
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
Event function:
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| code    |int                       |When code is 0, recording is completed|
| filepath    |string                      |Path for storing the recorded file|
| fileid    |string                      |URL to the file|

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
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnUploadFileComplete +=new QAVUploadFileCompleteCallback (OnUploadFileComplete);
Process the event after listening:
void OnUploadFileComplete(int code, string filepath, string fileid){
    //Callback for uploading voice files
}
```


### Download voice files
This API is used to download voice files.
#### Function prototype  
```
ITMGPTT DownloadRecordedFile (string fileID, string downloadFilePath)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| fileID    |string                       |URL to a file|
| downloadFilePath    |string                       |Local path for saving the file|

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().DownloadRecordedFile(fileId, filePath);
```


### Callback for downloading voice files
Callback is executed after a voice file has been downloaded, and the delegate function is used to pass the message.
#### Function prototype  
```
Delegate function:
public delegate void QAVDownloadFileCompleteCallback(int code, string filepath, string fileid);
Event function:
public abstract event QAVDownloadFileCompleteCallback OnDownloadFileComplete;
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| code    |int                       |When code is 0, recording is completed|
| filepath    |string                      |Path for storing the recorded file|
| fileid    |string                      |URL to the file|

#### Error codes

|Error Codes |Cause  |Solution        |
|-----|------|------|
|12289  |File access error while downloading the file    |Check if the file path is valid|
|12290  |The signature verification failed    |Check if the authentication key is correct, and if the offline voice is initialized.|
|12291  |Network storage system exception    |The server failed to get voice file. Check if the fileid is correct, network status is normal, and the cos file exists.|
|12292  |An error occurs in the file system of the server    |Check if the device can be accessed via public network, and if the server has this file.|
|12293  |An HTTP network error occurs while getting download parameters|Check if the device can be accessed via public network|
|12294  |The response packet is empty while getting download parameters |Check if the device can be accessed via public network|
|12295  |Failed to parse the response packet while getting download parameters|Check if the device can be accessed via public network|
|12297  |The appinfo is not set|Check if the authentication key is correct, and if the offline voice is initialized.|



#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnDownloadFileComplete +=new QAVDownloadFileCompleteCallback(OnDownloadFileComplete);
Process the event after listening:
void OnDownloadFileComplete(int code, string filepath, string fileid){
    //Send a callback after a voice file has been downloaded
}
```



### Play voice files
This API is used to play voice files.
#### Function prototype  
```
ITMGPTT PlayRecordedFile (string downloadFilePath)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| downloadFilePath    |string                       |Indicates the path of the file to be played|

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().PlayRecordedFile(filePath); 
```


### Callback for playing voice files
Callback is executed after a voice file has been played, and the delegate function is used to pass the message.
#### Function prototype  
```
Delegate function:
public delegate void QAVPlayFileCompleteCallback(int code, string filepath);
Event function:
public abstract event QAVPlayFileCompleteCallback OnPlayFileComplete;
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| code    |int                       |When code is 0, recording is completed|
| filepath    |string                      |Path for storing the recorded file|

#### Error codes

|Error Codes |Cause  |Solution        |
|-----|------|------|
|20481  |Initialization error|Check if the device is occupied, the permissions are normal, and the initialization is normal.|
|20482  |A client fails to stop a video that is being played and play the next one (this can be done normally)|Check if the code logic is correct|
|20483  |Empty parameter|Check if the API parameters in the codes are correct|
|20484  |Internal error|Player initialization failed as decoding failed. Analyze logs for troubleshooting.|


#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnPlayFileComplete +=new  QAVPlayFileCompleteCallback(OnPlayFileComplete);
Process the event after listening:
void OnPlayFileComplete(int code, string filepath){
    //Callback for playing a voice file
}
```




### Stop playing voice files
This API is used to stop playing back voice files.
#### Function prototype  
```
ITMGPTT int StopPlayFile()
```

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().StopPlayFile();
```



### Obtain the size of a voice file
This API is used to get the size of a voice file.
#### Function prototype  
```
ITMGPTT GetFileSize(string filePath) 
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| filePath    |string                      |Indicates the path to a voice file|

#### Sample code  
```
int fileSize = ITMGContext.GetInstance().GetPttCtrl().GetFileSize(filepath);
```

### Obtain the length of a voice file
This API is used to obtain the duration of a voice file (in milliseconds).
#### Function prototype  
```
ITMGPTT int GetVoiceFileDuration(string filePath)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| filePath    |string                      |Indicates the path to a voice file|

#### Sample code  
```
int fileDuration = ITMGContext.GetInstance().GetPttCtrl().GetVoiceFileDuration(filepath);
```


### Convert the specified voice file into text with Speech Recognition
This API is used to convert the specified voice file into text with Speech Recognition.

#### Function prototype  
```
ITMGPTT int SpeechToText(String fileID)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| fileID    |string                      |URL to the voice file|

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID);
```



### Translate the specified voice file into text (specify language)
This API is used to recognize specified language and translate the recognized information in an audio into specified language.

#### Function prototype  
```
ITMGPTT int SpeechToText(String fileID,String language)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| fileID    |String                     |Voice file url|
| speechLanguage    |String                    |Recognizes specified language. See [language reference list](https://intl.cloud.tencent.com/document/product/607/30260)|
| translatelanguage    |String                    |Translates into specified language. See [language reference list](https://intl.cloud.tencent.com/document/product/607/30260) (This parameter is not available. Enter the value for speechLanguage.)|

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID,"cmn-Hans-CN","cmn-Hans-CN");
```



### Callback for Speech Recognition
This API is used to convert the specified voice file into text with Speech Recognition, and the delegate function is used to pass the message.
#### Function prototype  
```
Delegate function:
public delegate void QAVSpeechToTextCallback(int code, string fileid, string result);
Event function:
public abstract event QAVSpeechToTextCallback OnSpeechToTextComplete;
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| code    |int                       |When code is 0, recording is completed|
| fileid    |string                      |URL to the voice file|
| result    |string                      |Result of text conversion|

#### Sample code
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnSpeechToTextComplete += new QAVSpeechToTextCallback(OnSpeechToTextComplete);
Process the event after listening:
void OnSpeechToTextComplete(int code, string fileid, string result){
    //Callback for Speech Recognition
}
```



## Advanced APIs

### Obtain the version number
This API is used to get the SDK version number for analysis.
#### Function prototype
```
ITMGContext  abstract string GetSDKVersion()
```
#### Sample code  
```
ITMGContext.GetInstance().GetSDKVersion();
```





### Set the print log level
This API is used to set the print log level. It is recommended to use default level.
#### Function prototype
```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### Parameter description

|Parameter|Type|Description|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|Sets the write log level. TMG_LOG_LEVEL_NONE indicates no write, with TMG_LOG_LEVEL_INFO by default.|
|levelPrint|ITMG_LOG_LEVEL|Sets the print log level. TMG_LOG_LEVEL_NONE indicates no print, with TMG_LOG_LEVEL_ERROR by default.|



|ITMG_LOG_LEVEL|Description|
| -------------------------------|:-------------:|
|TMG_LOG_LEVEL_NONE=0		|Do not print logs			|
|TMG_LOG_LEVEL_ERROR=1		|Prints error logs (default)	|
|TMG_LOG_LEVEL_INFO=2			|Prints prompt logs		|
|TMG_LOG_LEVEL_DEBUG=3		|Prints development and debugging logs	|
|TMG_LOG_LEVEL_VERBOSE=4		|Prints verbose logs		|

#### Sample code  
```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_NONE,true,true);
```



### Set the print log path
This API is used to set the print log path.
The default path is:

|Platform     |Path        |
| ------------- |-------------|
|Windows 	|%appdata%\Tencent\GME\ProcessName|
|iOS    		|Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android	|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    		|/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

#### Function prototype
```
ITMGContext  SetLogPath(string logDir)
```

|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------
| logDir    		|NSString   		|Path|

#### Sample code  
```
ITMGContext.GetInstance().SetLogPath(path);
```


### Obtain diagnostic messages
This API is used to obtain information about the quality of real-time audio/video calls. This API is mainly used to check the quality of real-time calls and troubleshoot problems, and can be ignored for this service.
#### Function prototype  
```
ITMGRoom GetQualityTips()
```
#### Sample code  
```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();
```

### Add an ID to the audio data blacklist
This API is used to add an ID to the audio data blacklist. A return value of 0 indicates that the call is successful.
#### Function prototype  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| openId    |NSString      |Indicates the ID to be added to the blacklist|

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().AddAudioBlackList (id);
```

### Remove an ID from the audio data blacklist
This API is used to remove an ID from the audio data blacklist. A return value of 0 indicates that the call is successful.
#### Function prototype  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)
```
|Parameter     | Type         |Description|
| ------------- |:-------------:|-------------|
| openId    |NSString      |ID that needs to be removed from the blacklist|

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (id);
```


