This document provides a detailed description that makes it easy for Unity developers to debug and integrate the APIs for Tencent Cloud's Game Multimedia Engine (GME).

>?This document applies to GME SDK version 2.3.
## How to Use
### How to use voice chat
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)
### How to convert voice message to text
![](https://main.qcloudimg.com/raw/4c875d05cd2b4eaefba676d2e4fc031d.png)


### Key considerations for using GME

| Important API | Description |
| ------------- |:-------------:|
| Init | Initializes GME |
|Poll    		| Triggers event callback	|
|EnterRoom	 	| Enters a room  		|
|EnableMic	 	| Enables the microphone 	|
|EnableSpeaker		| Enables the speaker 	|

>**Notes:**
- When a GME API is called successfully, QAVError.OK is returned, and the value is 0.
- GME APIs are called in the same thread.
- The request for entering a room via GME API should be authenticated. For more information, see authentication section in relevant documentation.
- The Poll API is called periodically for GME to trigger event callback.
- See the callback message list for GME callback information.
- The operation on devices shall be carried out after successful entry into a room.



## Initialization APIs
For an uninitialized SDK, you must initialize it via initialization authentication to enter a room.

| API | Description |
| ------------- |:-------------:|
|Init | Initializes GME |
|Poll    		| Triggers event callback	|
|Pause   	| Pauses the system	|
|Resume 	| Resumes the system	|
|Uninit | Uninitialzes GME |

### Obtain the instance
Obtain the Context instance using "ITMGContext.GetInstance()", instead of QAVContext.GetInstance().

### Initialize the SDK
For more information on how to obtain parameters, see [Integration Guide](https://cloud.tencent.com/document/product/607/10782).
This API should contain SdkAppId and openId. The SdkAppId is obtained from the Tencent Cloud console, and the openId is used to uniquely identify a user. The setting rule for openId can be customized by App developers, and this ID must be unique in an App (only INT64 is supported).
SDK must be initialized before a user can enter a room.

#### Function prototype
```
ITMGContext Init(string sdkAppID, string openID)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId | String | The sdkAppID obtained from the Tencent Cloud Console |
| openID |String | The OpenID only supports Int64 type(should be converted to String type for passing the api argument). It is used to identify the user and the value should be greater than 10000. |

#### Sample code  
```
int ret = ITMGContext.GetInstance().Init(str_appId, str_userId);
	if (ret != QAVError.OK) {
		return;
	}
```

### Trigger event callback
Event callbacks can be triggered by periodically calling Poll in "update".
#### Function prototype

```
ITMGContext public abstract int Poll();
```
### Pause the system
When the system Pause occurs, notify the engine for Pause.
#### Function prototype

```
ITMGContext public abstract int Pause()
```

### Resume the system
When the system Resume occurs, notify the engine for Resume.
#### Function prototype

```
ITMGContext  public abstract int Resume()
```






### Deinitialize the SDK
This API is used to deinitialize an SDK to make it uninitialized. Switching accounts requires deinitialization.
#### Function prototype

```
ITMGContext public abstract int Uninit()
```





## APIs for Voice Chat Room
You must initialize and call the SDK to enter a room before Voice Chat can start.

| API | Description |
| ------------- |:-------------:|
|GenAuthBuffer    	| Initializes authentication |
|EnterRoom | Enters a room |
|IsRoomEntered   	| Indicates whether any member has entered a room |
|ExitRoom 		| Exits a room |
|ChangeRoomType 	| Modifies the audio type of the user's room |
|GetRoomType 		| Obtains the audio type of the user's room |



### Authentication information
This API is used to generate AuthBuffer for encryption and authentication for the relevant features. For more information on deployment, see [Authentication Key](https://cloud.tencent.com/document/product/607/12218).    
- To obtain authentication for voice message, the room ID parameter must be set to null.
- The API returns a value of type Byte[].

#### Function prototype
```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId | int | The sdkAppID obtained from the Tencent Cloud Console |
| roomId | String | Room ID, which is limited to 127 characters (For voice message, enter "null".) |
| openId | String | User ID |
| key | string | The key obtained from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme) |



#### Sample code  
```
byte[] GetAuthBuffer(string appId, string userId, string roomId)
    {
	return QAVAuthBuffer.GenAuthBuffer(int.Parse(appId), roomId, userId, "a495dca2482589e9");
}
```

### Enter a room
This API is used to enter a room with the generated authentication information. Microphone and speaker are not enabled by default after a user enters the room. A callback is executed when the timeout threshold (30 seconds) for entering a room is exceeded.

For more information on how to integrate Range Voice, see [Range Voice](https://cloud.tencent.com/document/product/607/17972).


#### Function prototype
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId | string | Room ID, which is limited to 127 characters |
| roomType | ITMGRoomType | Audio type of the room |
| authBuffer | Byte[] | Authentication key |

For more information about room's audio types, see [Sound Quality Selection](https://cloud.tencent.com/document/product/607/18522).

#### Sample code  

```
ITMGContext.GetInstance().EnterRoom(roomId, ITMG_ROOM_TYPE_FLUENCY, authBuffer);
```

### Callback for entering a room
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

### Identify whether any member has entered a room
This API is called to identify whether any member has entered a room. A bool value is returned.
#### Function prototype  
```
ITMGContext abstract bool IsRoomEntered()
```
#### Sample code
```
ITMGContext.GetInstance().IsRoomEntered();
```

### Exit a room
This API is called to exit the current room. It is an asynchronous API. The returned value of AV_OK indicates a successful asynchronous delivery.

> If a user enters the room immediately after exiting a room in the application, the developer does not have to wait for the RoomExitComplete notification as a callback of ExitRoom in the API call process, but just calls the API directly.

#### Function prototype  
```
ITMGContext ExitRoom()
```
#### Sample code  
```
ITMGContext.GetInstance().ExitRoom();
```

### Callback for exiting a room
A callback is executed with a delegate function to pass message after a user exits the room.
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
    //A callback is executed after the user exits the room.
}
```

### Obtain the audio type of the user's room
This API is used to obtain the audio type of the user's room. The returned value is the audio type of the room. Value 0 means that an error occurred while obtaining the audio type of the user's room. See the API EnterRoom for the audio type of the user's room.

#### Function prototype  
```
ITMGContext ITMGRoom public  int GetRoomType()
```

#### Sample code  
```
ITMGContext.GetInstance().GetRoom().GetRoomType();
```

### Modify the audio type of the user's room
This API is used to modify the audio type of user's room.
#### Function prototype
```
ITMGContext ITMGRoom public void ChangeRoomType(ITMGRoomType roomtype)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomtype | ITMGRoomType | The room type to be switched to. For more information on the audio types of a room, see the document about API EnterRoom. |

#### Sample code
```
ITMGContext.GetInstance().GetRoom().ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```



### Callback for modifying the audio type of room
Set the room type. After the room type is set, a callback is executed with a delegate function to pass the message indicating the modification is completed.

| Returned Parameter | Description |
| ------------- |:-------------:|
| result | 0: successful |
| error_info | In case of failure, an error message is returned. |

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
void OnChangeRoomtypeCallback(){
    //A callback is executed after the room type is set.
}
```

### Notification of room type change
Once the room type is modified by you or another user in a room, this callback function is called to notify the business layer of the change of room type. The returned value is room type. See the document about API EnterRoom.
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
void OnRoomTypeChangedEvent(){
    //Send a callback after the room type has been changed
}
```


	
### Member status change
Notification about this event is sent only when the status changes. To obtain member status in real time, cache it when receiving notifications at a higher layer. The event message ITMG_MAIN_EVNET_TYPE_USER_UPDATE is returned. The parameter "openIdList" includes event_id and user_list. The event message is identified in the OnEvent function.
Notifications for audio events are subject to a threshold and a notification is sent only when this threshold is exceeded. The notification "A member stops sending audio packets" is sent when audio packets are not received after 2 seconds.

|event_id     | Description | Maintenance |
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				| A member enters the room			| Member list		|
|ITMG_EVENT_ID_USER_EXIT    				| A member exits the room			| Member list		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		| A member sends audio packets		| Chat member list	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			| A member stops sending audio packets		| Chat member list	|

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
		//The developer parses the parameter to obtain event_id and user_list.
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
The message for quality monitoring events is ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY. The returned parameters include weight, floss, and delay, which represent the following information. The event message is identified in the OnEvent function.

| Parameter | Description |
| ------------- |-------------|
|weight    				| Its value ranges from 1 to 5. "5" indicates excellent quality of audio packets, and "1" indicates poor quality of audio packets, which can barely be used; "0" represents an initial value and can be ignored. |
|floss    				| Packet loss |
|delay    		| Voice chat delay (ms) |


## APIs for Voice Chat
The APIs for Voice Chat can only be called after the SDK is initialized and you are in the room.
When you click the button to enable/disable the microphone or speaker:
- For most game Apps, it's recommended to call EnableMic and EnableSpeaker APIs. Because calling EnableMic is equivalent to calling EnableAudioCaptureDevice and EnableAudioSend at the same time, and calling EnableSpeaker is equivalent to calling EnableAudioPlayDevice and EnableAudioRecv at the same time.
- For other mobile Apps (such as social networking Apps), enabling/disabling a capturing device will restart both the capturing and the playback devices. If the App is playing background music, it will also be interrupted. Playback won't be interrupted if the microphone is enabled/disabled through upstream/downstream control. Calling method: Call EnableAudioCaptureDevice(true) and EnableAudioPlayDevice(true) once after a member enters the room. When clicking the button to enable/disable the microphone, you actually call EnableAudioSend/Recv to send/receive audio stream.
- For releasing only the capturing or the playback device, see APIs EnableAudioCaptureDevice and EnableAudioPlayDevice.
- Call "pause" to pause the audio engine and call "resume" to resume the audio engine.

### How to call social networking Apps
![](https://main.qcloudimg.com/raw/53598680491501ab5a144e87ba932ccc.png)


| API | Description |
| ------------- |:-------------:|
|EnableMic	 	| Enables/disables the microphone |
|GetMicState    						| Obtains the microphone status |
|EnableAudioCaptureDevice    		| Enables/disables the capturing device		|
|IsAudioCaptureDeviceEnabled    	| Obtains the capturing device status		|
|EnableAudioSend    				| Enables/disables audio upstream	|
|IsAudioSendEnabled    				| Obtains the audio upstream status	|
|GetMicLevel    						| Obtains real-time microphone volume	|
|SetMicVolume    					| Sets microphone volume |
|GetMicVolume    					| Obtains microphone volume	|
|EnableSpeaker    					| Enables/disables the speaker |
|GetSpeakerState    					| Obtains the speaker status |
|EnableAudioPlayDevice    			| Enables/disables the playback device		|
|IsAudioPlayDeviceEnabled    		| Obtains the playback device status	|
|EnableAudioRecv    					| Enables/disables audio downstream	|
|IsAudioRecvEnabled    				| Obtains the audio downstream status	|
|GetSpeakerLevel    					| Obtains real-time speaker volume |
|SetSpeakerVolume    				| Sets speaker volume |
|GetSpeakerVolume    				| Obtains speaker volume |
|EnableLoopBack    					| Enables/disables in-ear monitoring			|



### Enable/disable the microphone
This API is used to enable/disable the microphone. Microphone and speaker are not enabled by default after a user enters a room.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.
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

### Obtain the microphone status
This API is used to obtain the microphone status. If "0" is returned, the microphone is disabled. If "1" is returned, the microphone is enabled.
#### Function prototype  
```
ITMGAudioCtrl GetMicState()
```
#### Sample code  
```
micToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetMicState();
```

### Enable/disable a capturing device
This API is used to enable/disable a capturing device. The device is not enabled by default after a user enters the room.
- This API can only be called after a user enters the room. The device is disabled after the user exits the room.
- Operations such as permission application and volume type adjustment come with enabling the capturing device on mobile.

#### Function prototype
```
ITMGAudioCtrl int EnableAudioPlayDevice(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | true: enable the capturing device; false: disable the capturing device |

#### Sample code  
```
Enable a capturing device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioCaptureDevice(true);
```

### Obtain the status of a capturing device
This API is used to obtain the status of a capturing device.

#### Function prototype
```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()
```
#### Sample code

```
bool IsAudioCaptureDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioCaptureDeviceEnabled();
```

### Enable/disable audio upstream
This API is used to enable/disable audio upstream. If the capturing device is already enabled, it will send captured audio data. If not, it remains mute. Use the API EnableAudioCaptureDevice to enable or disable the capturing device.

#### Function prototype

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | true: enable the upstream delivery of audio data; false: disable this feature. |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioSend(true);
```

### Obtain the status of audio upstream
This API is used to obtain the status of audio upstream.
#### Function prototype  

```
ITMGAudioCtrl bool IsAudioSendEnabled()
```
#### Sample code
```
bool IsAudioSend = ITMGContext.GetInstance().GetAudioCtrl().IsAudioSendEnabled();
```

### Obtain real-time microphone volume
This API is used to obtain real-time microphone volume. An "int" value is returned.
#### Function prototype
```
ITMGAudioCtrl -(int)GetMicLevel
```
#### Sample code
```
ITMGContext.GetInstance().GetAudioCtrl().GetMicLevel();
```

### Set the microphone volume
This API is used to set microphone volume. When the value of parameter "volume" is 0, the microphone is muted; when the value is 100 (default), the volume remains unchanged.

#### Function prototype
```
ITMGAudioCtrl SetMicVolume(int volume)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume | int | Sets the volume, which ranges from 0 to 200. |

#### Sample code  

```
int micVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetMicVolume (micVol);
```

### Obtain the microphone volume
This API is used to obtain the microphone volume. An "int" value is returned. Value 101 represents API SetMicVolume has not been called.

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
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
#### Function prototype  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | true: enable the speaker; false: disable the speaker. |

#### Sample code  
```
Enable the speaker
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```


### Obtain the speaker status
This API is used to obtain the speaker status. If "0" is returned, the speaker is off. If "1" is returned, the speaker is on. If "2" is returned, the speaker is working.
#### Function prototype  
```
ITMGAudioCtrl GetSpeakerState()
```

#### Sample code  
```
speakerToggle.isOn = ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerState();
```


### Enable/disable a playback device
This API is used to enable/disable a playback device.
#### Function prototype  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | true: enable the playback device; false: disable the playback device. |

#### Sample code

```
Enable a playback device
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioPlayDevice(true);
```


### Obtain the status of a playback device
This API is used to obtain the status of a playback device.
#### Function prototype

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```
#### Sample code  

```
bool IsAudioPlayDevice = ITMGContext.GetInstance().GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### Enable/disable audio downstream
This API is used to enable/disable audio downstream. If the playback device is already enabled, it will play audio data from other members of the room. If not, it remains mute. Use the API EnableAudioPlayDevice to enable and disable the playback device.

#### Function prototype  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | bool | true: enable downstream delivery of audio data; false: disable downstream delivery of audio data. |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableAudioRecv(true);
```

### Obtain the status of audio downstream
This API is used to obtain the status of audio downstream.
#### Function prototype  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```
#### Sample code  

```
bool IsAudioRecv = ITMGContext.GetInstance().GetAudioCtrl().IsAudioRecvEnabled();
```


### Obtain real-time speaker volume
This API is used to obtain real time speaker volume. An "int" value is returned to indicate the real-time speaker volume.
#### Function prototype
```
ITMGAudioCtrl GetSpeakerLevel()
```

#### Sample code
```
ITMGContext.GetInstance().GetAudioCtrl().GetSpeakerLevel();
```

### Set the speaker volume
This API is used to set the speaker volume.
When the value of parameter "volume" is 0, the speaker is muted; when the value is 100 (default), the volume remains unchanged.

#### Function prototype  
```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume | int | Sets the volume, which ranges from 0 to 200. |

#### Sample code

```
int speVol = (int)(value * 100);
ITMGContext.GetInstance().GetAudioCtrl().SetSpeakerVolume(speVol);
```

### Obtain the speaker volume
This API is used to obtain the speaker volume. An "int" value is returned to indicate the speaker volume. Value 101 represents the API SetSpeakerVolume has not been called.
"Level" indicates the real-time volume, and "Volume" the speaker volume. The final volume equals to Level*Volume%. For example, if the "Level" is 100 and "Volume" is 60, the final volume is "60".

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
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable | bool | Specifies whether to enable in-ear monitoring |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl().EnableLoopBack(true);
```

### Callback for device occupation and release
After a device is occupied or released, a callback is executed with a delegate function to pass the message of the event.

```
Delegate function:
public delegate void QAVOnDeviceStateChangedEvent(int deviceType, string deviceId, bool openOrClose);
Event function:
public abstract event QAVOnDeviceStateChangedEvent OnDeviceStateChangedEvent;
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| deviceType | int |1: capturing device. 2: playback device |
| deviceId | string | Device GUID, which is used to identify a device and only applies to Windows and Mac. |
| openOrClose | bool | Occupies or releases a capturing/playback device |


| Parameter | Value | Description |
| ------------- |:-------------:|-------------|
| AUDIODEVICE_CAPTURE | 1 | Indicates a capturing device |
| AUDIODEVICE_PLAYER | 2 | Indicates a playback device |

#### Sample code  

```
Listen for an event:
ITMGContext.GetInstance().GetAudioCtrl().OnDeviceStateChangedEvent += new QAVAudioDeviceStateCallback(OnAudioDeviceStateChange);
Process the event after listening:
void QAVAudioDeviceStateCallback(){
    //A callback is executed when a device is occupied or released.
}
```


## APIs for Accompaniment in Voice Chat
| API | Description |
| ------------- |:-------------:|
|StartAccompany    				       | Starts playing back the accompaniment |
|StopAccompany    				   	| Stops playing back the accompaniment |
|IsAccompanyPlayEnd				| Indicates whether the accompaniment is over |
|PauseAccompany    					| Pauses playing back the accompaniment |
|ResumeAccompany					| Resumes playing back the accompaniment |
|SetAccompanyVolume 				| Sets the accompaniment volume |
|GetAccompanyVolume				| Obtains the volume of the accompaniment |
|SetAccompanyFileCurrentPlayedTimeByMs 				| Sets the playback progress |

### Start playing back the accompaniment
This API is called to play back the accompaniment. Supported formats include m4a, wav, and mp3. Calling this API resets the volume.
#### Function prototype
```
IQAVAudioEffectCtrl int StartAccompany(string filePath, bool loopBack, int loopCount, int duckerTimeMs)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | string  | Accompaniment's playback path |
| loopBack | bool | Indicates whether to output the accompaniment in a mixing mode. This is generally set to true, indicating that other users can also hear the accompaniment. |
| loopCount | int | Indicates the number of loops. Value -1 means an infinite loop. |
| duckerTimeMs | int | Indicates the fading time, which is generally set to 0 |

#### Sample code
```
ITMGContext.GetInstance().GetAudioEffectCtrl().StartAccompany(filePath,true,loopCount,duckerTimeMs);
```

### Callback for accompaniment playback
A callback is executed with a delegate function to pass the message when the playback of accompaniment ends.
#### Function prototype  
```
Delegate function:
public delegate void QAVAccompanyFileCompleteHandler(int code, string filepath);
Event function:
public abstract event QAVAccompanyFileCompleteHandler OnAccompanyFileCompleteHandler;
```
#### Sample code
```
Listen for an event:
ITMGContext.GetInstance().GetAudioEffectCtrl().OnAccompanyFileCompleteHandler += new QAVAccompanyFileCompleteHandler(OnAccomponyFileCompleteHandler);
Process the event after listening:
void OnAccomponyFileCompleteHandler(int code, string filepath){
    //Callback for accompaniment playback
}
```

### Stop playing back the accompaniment
This API is used to stop playing back the accompaniment.
#### Function prototype
```
IQAVAudioEffectCtrl int StopAccompany(int duckerTimeMs)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| duckerTimeMs | int | Fading time |

#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().StopAccompany(duckerTimeMs);
```

### Indicate whether the accompaniment is over
If it is over, "true" is returned. If it is not, "false" is returned.
#### Function prototype  
```
IQAAudioEffectCtrl bool IsAccompanyPlayEnd();
```
#### Sample code
```
ITMGContext.GetInstance().GetAudioEffectCtrl().IsAccompanyPlayEnd();
```


### Pause playing back the accompaniment
This API is used to pause playing back the accompaniment.
#### Function prototype
```
IQAAudioEffectCtrl int PauseAccompany()
```
#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().PauseAccompany();
```



### Resume playing back the accompaniment
This API is used to resume playing back the accompaniment.
#### Function prototype
```
IQAAudioEffectCtrl int ResumeAccompany()
```
#### Sample code
```
ITMGContext.GetInstance().GetAudioEffectCtrl().ResumeAccompany();
```

### Specify whether you can hear the accompaniment
This API is used to specify whether you can hear the accompaniment.
#### Function prototype  
```
IQAAudioEffectCtrl int EnableAccompanyPlay(bool enable)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable | bool | Indicates whether you can hear the accompaniment |

#### Sample code
```
ITMGContext.GetInstance().GetAudioEffectCtrl().EnableAccompanyPlay(true);
```

### Specify whether others can also hear the accompaniment
This API is used to specify whether others can also hear the accompaniment.
#### Function prototype  
```
IQAAudioEffectCtrl int EnableAccompanyLoopBack(bool enable)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable | bool | Indicates whether you can hear the accompaniment |

#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().EnableAccompanyLoopBack(true);
```


### Set the accompaniment volume
This API is used to set the accompaniment volume, which ranges from 0 to 200. It defaults to 100. A value greater than 100 means "volume up", while a value less than 100 means "volume down".
#### Function prototype  
```
IQAAudioEffectCtrl int SetAccompanyVolume(int vol)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| vol | int | Indicates the volume value |

#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().SetAccompanyVolume(vol);
```

### Obtain the volume of the accompaniment
This API is used to get the accompaniment volume.
#### Function prototype  
```
IQAAudioEffectCtrl abstract int GetAccompanyVolume()
```
#### Sample code  
```
string currentVol = "VOL: " + ITMGContext.GetInstance().GetAudioEffectCtrl().GetAccompanyVolume();
```

### Obtain the accompaniment playback progress
The following two APIs are used to obtain the accompaniment playback progress. Note: Current/Total = current loop times and Current % Total = current loop playback position.
#### Function prototype  
```
IQAAudioEffectCtrl abstract uint GetAccompanyFileTotalTimeByMs()
IQAAudioEffectCtrl abstract int GetAccompanyFileCurrentPlayedTimeByMs()
```
#### Sample code  
```
Sstring current = "Current: " + ITMGContext.GetInstance().GetAudioEffectCtrl().GetAccompanyFileCurrentPlayedTimeByMs() + " ms";
string total = "Total: " + ITMGContext.GetInstance().GetAudioEffectCtrl().GetAccompanyFileTotalTimeByMs() + " ms";
```


### Set the playback progress
This API is used to set the playback progress.
#### Function prototype  
```
IQAAudioEffectCtrl abstract uint SetAccompanyFileCurrentPlayedTimeByMs(uint time)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| time | uint | Indicates the playback progress in milliseconds |

#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().SetAccompanyFileCurrentPlayedTimeByMs(time);
```


## APIs for Sound Effect in Voice Chat
| API | Description |
| ------------- |:-------------:|
|PlayEffect    		| Plays the sound effect |
|PauseEffect    	| Pauses the sound effect |
|PauseAllEffects	| Pauses all sound effects |
|ResumeEffect    	| Resumes playing back the sound effect |
|ResumeAllEffects	| Resumes playing back all sound effects |
|StopEffect 		| Stops the sound effect |
|StopAllEffects		| Stops all sound effects |
|SetVoiceType 		| Voice changing effects |
|SetKaraokeType 		| Special karaoke sound effects |
|GetEffectsVolume	| Obtains the volume of sound effects |
|SetEffectsVolume 	| Sets the volume of sound effects |

### Play the sound effect
This API is used to play sound effects. The sound effect ID in the parameter needs to be managed by the App side. ID represents an independent playback event. This playback can be controlled later according to this ID. Three file formats are supported: m4a, wav, and mp3.
#### Function prototype  

```
IQAAudioEffectCtrl int PlayEffect(int soundId, string filePath, bool loop = false, double pitch = 1.0f, double pan = 0.0f, double gain = 1.0f)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |
| filePath | string | Indicates the path of sound effect |
| loop | bool | Indicates whether to repeat playback |
| pitch | double | Reserved field |
| pan | double | Reserved field |
| gain | double | Reserved field |

#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().PlayEffect(soundId,filePath,true,1.0,0,1.0);
```

### Pause the sound effect
This API is used to pause playing back the sound effect.
#### Function prototype  
```
IQAAudioEffectCtrl int PauseEffect(int soundId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |

#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().PauseEffect(soundId);
```

### Pause all sound effects
This API is used to pause all sound effects.
#### Function prototype  
```
IQAAudioEffectCtrl int PauseAllEffects()
```
#### Sample code
```
ITMGContext.GetInstance().GetAudioEffectCtrl().PauseAllEffects();
```

### Resume playing back the sound effect
This API is used to resume playing back the sound effect.
#### Function prototype  
```
IQAAudioEffectCtrl int ResumeEffect(int soundId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |

#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().ResumeEffect(soundId);
```



### Resume playing back all sound effects
This API is used to resume playing back all sound effects.
#### Function prototype  
```
IQAAudioEffectCtrl int ResumeAllEffects()
```
#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().ResumeAllEffects();
```

### Stop the sound effect
This API is used to stop the sound effect.
#### Function prototype
```
IQAAudioEffectCtrl int StopEffect(int soundId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |

#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().StopEffect(soundId);
```

### Stop all sound effects
This API is used to stop all sound effects.
#### Function prototype  
```
IQAAudioEffectCtrl int StopAllEffects()
```
#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().StopAllEffects(); 
```

### Voice changing effects
This API is used to set the voice changing effects.
#### Function prototype
```
IQAAudioEffectCtrl int setVoiceType(int type)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| type | int | Indicates the type of local voice changing effect |



| Type | Parameter | Description |
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND | 0 | Original sound |
| ITMG_VOICE_TYPE_LOLITA | 1 | Lolita |
| ITMG_VOICE_TYPE_UNCLE | 2 | Uncle |
| ITMG_VOICE_TYPE_INTANGIBLE | 3 | Ethereal |
| ITMG_VOICE_TYPE_DEAD_FATBOY | 4 | Fat boy |
| ITMG_VOICE_TYPE_HEAVY_MENTA | 5 | Heavy metal |
| ITMG_VOICE_TYPE_DIALECT | 6 | Dialect |
| ITMG_VOICE_TYPE_INFLUENZA | 7 | Catching cold |
| ITMG_VOICE_TYPE_CAGED_ANIMAL | 8 | Trapped beast |
| ITMG_VOICE_TYPE_HEAVY_MACHINE | 9 | Mechanic sound |
| ITMG_VOICE_TYPE_STRONG_CURRENT | 10 | Strong current |
| ITMG_VOICE_TYPE_KINDER_GARTEN | 11 | Kindergarten |
| ITMG_VOICE_TYPE_HUANG | 12 | Minions |


#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().setVoiceType(0);
```

### Special karaoke sound effects
This API is used to set special karaoke sound effects.
#### Function prototype  
```
IQAAudioEffectCtrl int SetKaraokeType(int type)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| type | int | Indicates the type of local voice changing effect |


| Type | Parameter | Description |
| ------------- |-------------|------------- |
| ITMG_KARAOKE_TYPE_ORIGINAL | 0 | Original sound |
| ITMG_KARAOKE_TYPE_POP | 1 | Popular |
| ITMG_KARAOKE_TYPE_ROCK | 2 | Rock |
| ITMG_KARAOKE_TYPE_RB | 3 | Hip-hop |
| ITMG_KARAOKE_TYPE_DANCE | 4 | Dance music |
| ITMG_KARAOKE_TYPE_HEAVEN | 5 | Ethereal |
| ITMG_KARAOKE_TYPE_TTS | 6 | TTS |

#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().SetKaraokeType(0);
```




### Obtain the volume of sound effects
This API is used to obtain the volume (linear volume) of sound effects, which ranges from 0 to 200. It defaults to 100. A value greater than 100 means "volume up", while a value less than 100 means "volume down".
#### Function prototype  
```
IQAAudioEffectCtrl  int GetEffectsVolume()
```
#### Sample code  
```
ITMGContext.GetInstance().GetAudioEffectCtrl().GetEffectsVolume();
```


### Set the volume of sound effects
This API is used to set the volume of sound effects.
#### Function prototype  
```
IQAAudioEffectCtrl  int SetEffectsVolume(int volume)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume | int | Indicates the volume value |

#### Sample code
```
ITMGContext.GetInstance().GetAudioEffectCtrl().SetEffectsVolume(volume);
```







## Voice Message
Initialize the SDK before using voice message and voice-to-text converting features.

| API | Description |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    | Initializes authentication	|
|SetMaxMessageLength    | Specifies the maximum length of a voice message	|
|StartRecording		| Starts recording		|
|StartRecordingWithStreamingRecognition		| Starts streaming recording		|
|StopRecording    	| Stops recording		|
|CancelRecording	| Cancels recording		|
|GetMicLevel    						| Obtains real-time microphone volume of voice message	|
|GetSpeakerLevel    					| Obtains real-time speaker volume for voice message |
|UploadRecordedFile 	| Uploads voice files		|
|DownloadRecordedFile	| Downloads voice files		|
|PlayRecordedFile 	| Plays voice files		|
|StopPlayFile		| Stops playing voice files		|
|GetFileSize 		| Indicates the size of a voice file		|
|GetVoiceFileDuration	| Indicates the length of a voice file		|
|SpeechToText | Converts voice to text |

### Authentication initialization
Call authentication initialization after initializing the SDK. To obtain authBuffer, see the API of voice chat authentication.
#### Function prototype  
```
ITMGPTT int ApplyPTTAuthbuffer (byte[] authBuffer)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| authBuffer	|byte[]	| Authentication |

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().ApplyPTTAuthbuffer(authBuffer);
```

### Specify the maximum length of a voice message
This API is used to specify the maximum length of a voice message, which is limited to 60 seconds.
#### Function prototype
```
ITMGPTT int SetMaxMessageLength(int msTime)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| msTime | int | Indicates the length of a voice message in ms |

#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().SetMaxMessageLength(60000); 
```


### Start recording
This API is used to start recording. The recorded file must be uploaded before you can perform operations such as voice-to-text converting.
#### Function prototype  
```
ITMGPTT int StartRecording(string fileDir)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileDir | string | Indicates the path for storing the voice file |

#### Sample code
```
string recordPath = Application.persistentDataPath + string.Format ("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecording(recordPath);
```

### Callback for starting recordings
A callback is executed with a delegate function to pass the message when recording is completed.
#### Function prototype  
```
Delegate function:
public delegate void QAVRecordFileCompleteCallback(int code, string filepath); 
Event function:
public abstract event QAVRecordFileCompleteCallback OnRecordFileComplete;
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | string | 0: recording is completed |
| filepath | string | Path for storing the recorded file |

#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnRecordFileComplete += mInnerHandler;
Process the event after listening:
void mInnerHandler(int code, string filepath){
    //Callback for starting recordings
}
```

### Start streaming speech recognition
This API is used to start streaming speech recognition. Texts obtained from voice-to-text converting will be returned in real time in its callback. It can specify a language for recognition, or translate the information recognized in speech into a specified language and return it.

#### Function prototype  

```
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath)
ITMGPTT int StartRecordingWithStreamingRecognition(string filePath, string speechLanguage,string translateLanguage)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | String | Indicates the path for storing the voice file |
| speechLanguage | String | String | Indicates the language in which the voice is converted to text. See [Language Parameter Reference List](https://cloud.tencent.com/document/product/607/30282) |
| translateLanguage | String | String | Indicates the language in which the voice is translated into text. See [Language Parameter Reference List](https://cloud.tencent.com/document/product/607/30282) (This parameter is unavailable. Enter the same value as that of speechLanguage) |

#### Sample code  
```
string recordPath = Application.persistentDataPath + string.Format("/{0}.silk", sUid++);
int ret = ITMGContext.GetInstance().GetPttCtrl().StartRecordingWithStreamingRecognition(recordPath, "cmn-Hans-CN", "cmn-Hans-CN");
```

### Callback for starting streaming speech recognition
A callback is executed with a delegate function to pass the message when streaming voice-to-text converting is completed.
```
Delegate function:
public delegate void QAVStreamingRecognitionCallback(int code, string fileid, string filepath, string result);
Event function:
public abstract event QAVStreamingRecognitionCallback OnStreamingSpeechComplete;
```

| Message Name | Description |
| ------------- |:-------------:|
| code | Indicates whether streaming voice-to-text converting is successful |
| result | The text obtained after voice-to-text converting |
| filepath | Indicates the local path of the recorded file |
| fileid | Indicates the backend URL to the recorded file |

| Error Code | Description | Recommended Action |
| ------------- |:-------------:|:-------------:|
|32775	| Recording is successful, but streaming voice-to-text converting failed	| Call the API UploadRecordedFile to upload the recording, and then call the API SpeechToText to perform voice-to-text converting.
|32777	| Recording is successful and is uploaded, but streaming voice-to-text converting failed.	| The message returned includes a backend URL for successful upload. Call the API SpeechToText to perform voice-to-text converting.

#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnStreamingSpeechComplete += mInnerHandler;
Process the event after listening:
void mInnerHandler(int code, string fileid, string filepath, string result){
    // A callback is executed when streaming voice-to-text converting is completed.
}

```
### Stop recording
This API is used to stop recording. It is an asynchronous API. A callback is returned after recording. After it is successful, the recording file is available.
#### Function prototype  
```
ITMGPTT int StopRecording()
```
#### Sample code
```
ITMGContext.GetInstance().GetPttCtrl().StopRecording();
```

### Cancel recording
This API is used to cancel recording. There is no callback after cancellation.
#### Function prototype  

```
IQAVPTT int CancelRecording()
```
#### Sample code  

```
ITMGContext.GetInstance().GetPttCtrl().CancelRecording();
```

### Obtain real-time microphone volume of voice message
This API is used to obtain real-time microphone volume. An "int" value is returned. Value range: 0-200.

#### Function prototype  
```
IQAVPTT int GetMicLevel()
```
#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().GetMicLevel();
```


### Obtain real-time speaker volume
This API is used to obtain real-time speaker volume. An "int" value is returned. Value range: 0-200.

#### Function prototype  
```
IQAVPTT int GetSpeakerLevel()
```

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().GetSpeakerLevel();
```




### Upload voice files
This API is used to upload voice files.
#### Function prototype  

```
IQAVPTT int UploadRecordedFile (string filePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | string | Indicates the path of the uploaded voice files |

#### Sample code

```
ITMGContext.GetInstance().GetPttCtrl().UploadRecordedFile(filePath);
```


### Callback for uploading voice files
A callback is executed with a delegate function to pass the message when the upload of voice files is completed.
#### Function prototype
```
Delegate function:
public delegate void QAVUploadFileCompleteCallback(int code, string filepath, string fileid);
Event function:
public abstract event QAVUploadFileCompleteCallback OnUploadFileComplete; 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | int | 0: recording is completed |
| filepath | string | Path for storing the recorded file |
| fileid | string | URL to the file |

#### Sample code
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnUploadFileComplete += mInnerHandler;
Process the event after listening:
void mInnerHandler(int code, string filepath, string fileid){
    //Callback for uploading voice files
}
```


### Download voice files
This API is used to download voice files.
#### Function prototype  

```
IQAVPTT DownloadRecordedFile (string fileID, string downloadFilePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID | string | URL to the file |
| downloadFilePath | string | Local path for storing the file |

#### Sample code

```
ITMGContext.GetInstance().GetPttCtrl().DownloadRecordedFile(fileId, filePath);
```


### Callback for downloading voice files
A callback is executed with a delegate function to pass the message when the download of a voice file is completed.
#### Function prototype  
```
Delegate function:
public delegate void QAVDownloadFileCompleteCallback(int code, string filepath, string fileid);
Event function:
public abstract event QAVDownloadFileCompleteCallback OnDownloadFileComplete;
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | int | 0: recording is completed |
| filepath | string | Path for storing the recorded file |
| fileid | string | URL to the file |

#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnDownloadFileComplete += mInnerHandler;
Process the event after listening:
void mInnerHandler(int code, string filepath, string fileid){
    //A callback is executed when the download of the voice file is downloaded.
}
```



### Play voice files
This API is used to play voice files.
#### Function prototype
```
IQAVPTT PlayRecordedFile (string downloadFilePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| downloadFilePath | string | Path to the file |

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().PlayRecordedFile(filePath); 
```


### Callback for playing voice files
The callback executed after a voice file is played. It passes the message with a delegate function.
#### Function prototype  
```
Delegate function:
public delegate void QAVPlayFileCompleteCallback(int code, string filepath);
Event function:
public abstract event QAVPlayFileCompleteCallback OnPlayFileComplete;
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | int | 0: recording is completed |
| filepath | string | Path for storing the recorded file |

#### Sample code  
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnPlayFileComplete += mInnerHandler;
Process the event after listening:
void mInnerHandler(int code, string filepath){
    //Callback for playing a voice file
}
```




### Stop playing voice files
This API is used to stop playing back voice files.
#### Function prototype  
```
IQAVPTT int StopPlayFile()
```

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().StopPlayFile();
```



### Obtain the size of a voice file
This API is used to get the size of a voice file.
#### Function prototype  
```
IQAVPTT GetFileSize(string filePath) 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | string | Path to the voice file |

#### Sample code  
```
int fileSize = ITMGContext.GetInstance().GetPttCtrl().GetFileSize(filepath);
```

### Obtain the length of a voice file
This API is used to obtain the length of a voice file (in milliseconds).
#### Function prototype  
```
IQAVPTT int GetVoiceFileDuration(string filePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | string | Path to the voice file |

#### Sample code  
```
int fileDuration = ITMGContext.GetInstance().GetPttCtrl().GetVoiceFileDuration(filepath);
```


### Convert the specified voice file into text with Automatic Speech Recognition
This API is used to convert the specified voice file into text with Automatic Speech Recognition.

#### Function prototype  

```
IQAVPTT int SpeechToText(String fileID)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID | string | URL to the voice file |

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID);
```

### Translate the specified voice file into text (specified language)
This API is used to translate the specified voice file into text in specified language.

#### Function prototype  
```
IQAVPTT int SpeechToText(String fileID,String speechLanguage,String translateLanguage)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID | String | URL to the voice file |
| speechLanguage | String | Indicates the language in which the voice file is converted to text. See [Language Parameter Reference List](https://cloud.tencent.com/document/product/607/30282) |
| translatelanguage | String | Indicates the language into which the voice will be translated. See [Language Parameter Reference Table](https://cloud.tencent.com/document/product/607/30282) (This parameter is unavailable. Enter the same value as that of speechLanguage) |

#### Sample code  
```
ITMGContext.GetInstance().GetPttCtrl().SpeechToText(fileID,"cmn-Hans-CN","cmn-Hans-CN");
```



### Callback for Automatic Speech Recognition
This is a callback executed when the specified voice file is converted to text. It passes message with a delegate function.
#### Function prototype  
```
Delegate function:
public delegate void QAVSpeechToTextCallback(int code, string fileid, string result);
Event function:
public abstract event QAVSpeechToTextCallback OnSpeechToTextComplete;
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| code | int | 0: recording is completed |
| fileid | string | URL to the voice file |
| result | string | Result of text conversion |

#### Sample code
```
Listen for an event:
ITMGContext.GetInstance().GetPttCtrl().OnSpeechToTextComplete += mInnerHandler;
Process the event after listening:
void mInnerHandler(int code, string fileid, string result){
    //Callback for voice-to-text converting
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





### Set the level of logs to be printed
This API is used to set the level of logs to be printed. It is recommended to maintain the default level.
#### Function prototype
```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### Parameter description

| Parameter | Type | Description |
|---|---|---|
| levelWrite | ITMG_LOG_LEVEL | Sets the log writing level. It defaults to TMG_LOG_LEVEL_INFO. TMG_LOG_LEVEL_NONE means no writing. |
| levelPrint | ITMG_LOG_LEVEL | Sets the log printing level. It defaults to TMG_LOG_LEVEL_ERROR. TMG_LOG_LEVEL_NONE means no printing. |



| ITMG_LOG_LEVEL | Description |
| -------------------------------|:-------------:|
|TMG_LOG_LEVEL_NONE=0		| Do not print logs			|
|TMG_LOG_LEVEL_ERROR=1		| Prints error logs (default)	|
|TMG_LOG_LEVEL_INFO=2			| Prints prompt logs		|
|TMG_LOG_LEVEL_DEBUG=3		| Prints development and debugging logs	|
|TMG_LOG_LEVEL_VERBOSE=4		| Prints high-frequency logs		|

#### Sample code  
```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_NONE,TMG_LOG_LEVEL_ERROR);
```

### Set the path of logs to be printed
This API is used to set the path of logs to be printed.
The default path is:

| Platform | Path |
| ------------- |-------------|
|Windows 	|%appdata%\Tencent\GME\ProcessName|
|iOS    		|Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents|
|Android	|/sdcard/Android/data/xxx.xxx.xxx/files|
|Mac    		|/Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents|

#### Function prototype
```
ITMGContext  SetLogPath(string logDir)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------
| logDir | NSString | Path |

#### Sample code  
```
ITMGContext.GetInstance().SetLogPath(path);
```
### Obtain diagnostic messages
This API is used to obtain information about the quality of real-time audio/video calls. This API is mainly used to check the quality of real-time calls and troubleshoot problems, and can be ignored for this service.
#### Function prototype  
```
IQAVRoom GetQualityTips()
```
#### Sample code  
```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();
```

### Add an ID to the audio data blacklist
This API is used to add an ID to the audio data blacklist. A return value of 0 indicates that the call is successful.
#### Function prototype  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(string openId)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| openId | NSString | Indicates the ID to be added to the blacklist |

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
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| openId | NSString | Indicates the ID to be removed from the blacklist |

#### Sample code  

```
ITMGContext.GetInstance().GetAudioCtrl ().RemoveAudioBlackList (id);
```


