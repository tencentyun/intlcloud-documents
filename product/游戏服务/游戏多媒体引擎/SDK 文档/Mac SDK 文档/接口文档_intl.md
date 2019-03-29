This document provides a detailed description that makes it easy for Mac developers to debug and integrate the APIs for Game Multimedia Engine.

>?This document applies to GME SDK version 2.4.

## How to Use
### How to use voice chat
![](https://main.qcloudimg.com/raw/bf2993148e4783caf331e6ffd5cec661.png)

### How to convert voice message to text
![](https://main.qcloudimg.com/raw/4c875d05cd2b4eaefba676d2e4fc031d.png)

### Key considerations for using GME

| Important API | Description |
| ------------- |:-------------:|
| InitEngine | Initializes GME |
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
| InitEngine | Initializes GME |
|Poll    		| Triggers event callback	|
|Pause   	| Pauses the system	|
|Resume 	| Resumes the system	|
|Uninit | Deinitializes GME |

### Get a singleton
To use the voice feature, get the ITMGContext object first.
#### Function prototype

```
ITMGContext ITMGDelegate <NSObject>
```
#### Sample code  

```
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate =self;
```

### Message passing
With the API class, the Delegate method is used to send callback notifications to your application. ITMG_MAIN_EVENT_TYPE indicates the message type. The message content is a dictionary, which varies depending on the event type.
#### Function prototype

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```
#### Sample code

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
		switch (eventType) {
			//Identify eventType
			}
	}
```


### Initialize the SDK
For more information on how to obtain parameters, see [Integration Guide](https://cloud.tencent.com/document/product/607/10782).
This API should contain SdkAppId and openId. The SdkAppId is obtained from the Tencent Cloud console, and the openId is used to uniquely identify a user. The setting rule for openId can be customized by App developers, and this ID must be unique in an App (only INT64 is supported).
SDK must be initialized before a user can enter a room.
#### Function prototype

```
ITMGContext -(void)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId | NSString | The sdkAppID obtained from the Tencent Cloud Console |
| openID | NSString | The OpenID supports Int64 type (which is passed after being converted to a string) only. It is used to identify users and must be greater than 10000. |

#### Sample code  

```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```


### Trigger event callback
Event callbacks can be triggered by periodically calling Poll in "update".
#### Function prototype

```
ITMGContext -(void)Poll
```
#### Sample code
```
[[ITMGContext GetInstance] Poll];
```



### Pause the system
When the system Pause occurs, notify the engine for Pause.
#### Function prototype

```
ITMGContext -(QAVResult)Pause
```

### Resume the system
When the system Resume occurs, notify the engine for Resume.
#### Function prototype

```
ITMGContext -(QAVResult)Resume
```


### Deinitialize the SDK
This API is used to deinitialize an SDK to make it uninitialized. Switching accounts requires deinitialization.
#### Function prototype

```
ITMGContext -(void)Uninit
```
#### Sample code
```
[[ITMGContext GetInstance] Uninit];
```


## APIs for Voice Chat Room
You must initialize and call the SDK to enter a room before Voice Chat can start.

| API | Description |
| ------------- |:-------------:|
|GenAuthBuffer    	| Initializes authentication |
| EnterRoom | Enters a room |
|IsRoomEntered   	| Indicates whether any member has entered a room |
| ExitRoom | Exits a room |
|ChangeRoomType 	| Modifies the audio type of the user's room |
|GetRoomType 		| Obtains the audio type of the user's room |



### Authentication information
This API is used to generate AuthBuffer for encryption and authentication. For more information on deployment at backend, see [Authentication Key](https://cloud.tencent.com/document/product/607/12218). To obtain authentication for voice message, the room ID parameter must be set to null.
A value of type NSData is returned by this API.
#### Function prototype

```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId | int | The sdkAppID obtained from the Tencent Cloud Console |
| roomId | NSString  | Room ID, which is limited to 127 characters (The room ID parameter for voice message must be set to null) |
| openID | NSString   | User ID |
| key | NSString   | The key obtained from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme) |



#### Sample code  

```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```

### Enter a room
When a user enter a room with the generated authentication information, the ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is received as a callback. Microphone and speaker are not enabled by default after a user enters the room. The returned value of AV_OK indicates a success.


#### Function prototype

```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int*)roomType authBuffer:(NSData*)authBuffer
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId | NSString | Room ID, which is limited to 127 characters |
| roomType | int | Audio type of the room |
| authBuffer | NSData | Authentication key |

For more information about room's audio types, see [Sound Quality Selection](https://cloud.tencent.com/document/product/607/18522).
  
#### Sample code  

```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### Callback for entering a room
The ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is returned after a user enters a room, which is checked in the OnEvent function.
#### Sample code 

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
            //Receive the event of entering the room successfully.
        }
            break;
     }
}
```

### Identify whether any member has entered a room
This API is called to identify whether any member has entered a room. A bool value is returned.
#### Function prototype  

```
ITMGContext -(BOOL)IsRoomEntered
```
#### Sample code  

```
[[ITMGContext GetInstance] IsRoomEntered];
```

### Exit a room
This API is called to exit the current room. It is an asynchronous API. The returned value of AV_OK indicates a successful asynchronous delivery.

> If a user enters the room immediately after exiting a room in the application, the developer does not have to wait for the RoomExitComplete notification as a callback of ExitRoom in the API call process, but just calls the API directly.

#### Function prototype  

```
ITMGContext -(int)ExitRoom
```
#### Sample code

```
[[ITMGContext GetInstance] ExitRoom];
```

### Callback for exiting a room
After a user exits the room, a callback response is returned and the ITMG_MAIN_EVENT_TYPE_EXIT_ROOM message is received.

#### Sample code  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM：
        {
	    //Receive the event of exiting the room successfully.
        }
            break;
    }
}
```



### Modify the audio type of the user's room
This API is used to modify the audio type of the user's room. See the callback event for the result. The event type is ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE.

#### Function prototype  
```
ITMGContext GetRoom -(void)ChangeRoomType:(int)nRoomType
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| nRoomType    | int    | The room type to be switched to. See the API EnterRoom for the audio type of the user's room. |

#### Sample code

```
[[[ITMGContext GetInstance]GetRoom ]ChangeRoomType:_roomType];
```

### Obtain the audio type of the user's room
This API is used to obtain the audio type of the user's room. The returned value is the audio type of the room. Value 0 means that an error occurred while obtaining the audio type of the user's room. See the API EnterRoom for the audio type of the user's room.

#### Function prototype  
```
ITMGContext GetRoom -(int)GetRoomType
```


#### Sample code

```
[[[ITMGContext GetInstance]GetRoom ]GetRoomType];
```

### Callback after the room type is set
After the room type is set, the event message ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE is returned in the callback response. The returned parameters include result, error_info, and new_room_type. The new_room_type represents the following information. The event message is identified in the OnEvent function.

| Event Sub-type | Parameters | Description |
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM		|1 	| Indicates that the existing audio type is inconsistent and changed to that of the room to enter.	|
| ITMG_ROOM_CHANGE_EVENT_START			|2	| Indicates that a user is already in the room and the audio type starts changing (e.g., call the ChangeRoomType API to change the audio type). |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE		|3	| Indicates that a user is already in the room and the audio type has been changed. |
| ITMG_ROOM_CHANGE_EVENT_REQUEST			|4	| Indicates that a room member calls the ChangeRoomType API to request a change in the audio type. |	


#### Sample code  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
 		case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
			//Process
	 }
    }
}
```


### Member status change
Notification about this event is sent only when the status changes. To obtain member status in real time, cache it when receiving notifications at a higher layer. The event message ITMG_MAIN_EVNET_TYPE_USER_UPDATE is returned. The passed parameter includes event_id and endpoints. The event message is identified in the OnEvent function.
Notifications for audio events are subject to a threshold and a notification is sent only when this threshold is exceeded. The notification "A member stops sending audio packets" is sent when audio packets are not received after 2 seconds.

|event_id     | Description | Maintenance |
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    				| A member enters the room			| Member list		|
|ITMG_EVENT_ID_USER_EXIT    				| A member exits the room			| Member list		|
|ITMG_EVENT_ID_USER_HAS_AUDIO    		| A member sends audio packets		| Chat member list	|
|ITMG_EVENT_ID_USER_NO_AUDIO    			| A member stops sending audio packets		| Chat member list	|

#### Sample code  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
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
 		    }
		break;
		}
    }
}
```

### Quality monitoring events
The message for quality monitoring events is ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY. The returned parameters include weight, floss, and delay, which represent the following information. The event message is identified in the OnEvent function.

| Parameter | Description |
| ------------- |-------------|
|weight    				| Its value ranges from 1 to 50. "50" indicates excellent quality of audio packets, and "1" indicates poor quality of audio packets, which can barely be used; "0" represents an initial value and can be ignored. |
|floss    				| Packet loss |
|delay    		| Voice chat delay (ms) |


### Message details

| Message | Description   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				       | Indicates that a member enters an audio/video room |
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				         	| Indicates that a member exits an audio/video room |
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		       | Indicates that a room is disconnected due to network or other reasons |
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE				| Indicates a room type change event |

### Details of Data corresponding to the message
| Message     | Data         | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				|result; error_info					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				|result; error_info  					|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		|result; error_info  					|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    		|result; error_info; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|


## APIs for Voice Chat
The APIs for Voice Chat can only be called after the SDK is initialized and you are in the room.
Calling scenario examples:

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
ITMGContext GetAudioCtrl -(void)EnableMic:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | boolean | To enable the microphone, set this parameter to YES; otherwise set it to NO. |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```

### Obtain the microphone status
This API is used to obtain the microphone status. If "0" is returned, the microphone is off. If "1" is returned, the microphone is on.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(int)GetMicState
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicState];
```

### Enable/disable a capturing device
This API is used to enable/disable a capturing device. The device is not enabled by default after a user enters the room.
- This API can only be called after a user enters the room. The device is disabled after the user exits the room.
- Operations such as permission application and volume type adjustment come with enabling the capturing device on mobile.

#### Function prototype  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enabled | BOOL | To enable the capturing device, set this parameter to YES, otherwise set it to NO. |

#### Sample code  

```
Enable a capturing device
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioCaptureDevice:enabled];
```

### Obtain the status of a capturing device
This API is used to obtain the status of a capturing device.
#### Function prototype

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioCaptureDeviceEnabled
```
#### Sample code

```
BOOL IsAudioCaptureDevice = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioCaptureDeviceEnabled];
```

### Enable/disable audio upstream
This API is used to enable/disable audio upstream. If the capturing device is already enabled, it will send captured audio data. If not, it remains mute. Use the API EnableAudioCaptureDevice to enable or disable the capturing device.

#### Function prototype

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioSend:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable | BOOL | To enable the audio upstream, set this parameter to YES, otherwise set it to NO. |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioSend:enabled];
```

### Obtain the status of audio upstream
This API is used to obtain the status of audio upstream.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioSendEnabled
```
#### Sample code  

```
BOOL IsAudioSend =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioSendEnabled];
```

### Obtain real-time microphone volume
This API is used to obtain real-time microphone volume. An "int" value is returned.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(int)GetMicLevel
```
#### Sample code  
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicLevel];
```

### Set the microphone volume
This API is used to set microphone volume. The corresponding parameter is "volume". "0" means the volume is set to Mute, and "100" means the volume remains unchanged. It defaults to 100.

#### Function prototype 
 
```
ITMGContext GetAudioCtrl -(QAVResult)SetMicVolume:(int) volume
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume | int | Sets the volume. Value range: 0 to 200. |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] SetMicVolume:100];
```

### Obtain the microphone volume
This API is used to obtain the microphone volume. An "int" value is returned. Value 101 represents API SetMicVolume has not been called.

#### Function prototype  

```
ITMGContext GetAudioCtrl -(int) GetMicVolume
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicVolume];
```

### Enable/disable the speaker
This API is used to enable/disable the speaker.
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled | boolean | To disable the speaker, set this parameter to NO, otherwise set it to YES. |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```

### Obtain the speaker status
This API is used to obtain the speaker status. If "0" is returned, the speaker is off. If "1" is returned, the speaker is on. If "2" is returned, the speaker is working.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(int)GetSpeakerState
```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerState];
```

### Enable/disable a playback device
This API is used to enable/disable a playback device.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioPlayDevice:(BOOL)enabled
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enabled | BOOL | To disable the playback device, set this parameter to NO, otherwise set it to YES. |

#### Sample code

```
Enable a playback device
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioPlayDevice:enabled];
```


### Obtain the status of a playback device
This API is used to obtain the status of a playback device.
#### Function prototype

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioPlayDeviceEnabled
```
#### Sample code  

```
BOOL IsAudioPlayDevice =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioPlayDeviceEnabled];
```

### Enable/disable audio downstream
This API is used to enable/disable audio downstream. If the playback device is already enabled, it will play audio data from other members of the room. If not, it remains mute. Use the API EnableAudioPlayDevice to enable and disable the playback device.

#### Function prototype  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioRecv:(BOOL)enabled
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enabled | BOOL | To enable the audio downstream, set this parameter to YES, otherwise set it to NO. |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioRecv:enabled];
```

### Obtain the status of audio downstream
This API is used to obtain the status of audio downstream.
#### Function prototype  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### Sample code  

```
BOOL IsAudioRecv = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioRecvEnabled];
```

### Obtain real-time speaker volume
This API is used to obtain real time speaker volume. An "int" value is returned to indicate the real-time speaker volume.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(int)GetSpeakerLevel
```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerLevel];
```

### Set the speaker volume
This API is used to set the speaker volume.
The corresponding parameter is "volume". "0" means the volume is set to Mute, and "100" means the volume remains unchanged. It defaults to 100.

#### Function prototype  

```
ITMGContext GetAudioCtrl -(QAVResult)SetSpeakerVolume:(int)vol
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| vol | int | Sets the volume, value range: 0 to 200. |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] SetSpeakerVolume:100];
```

### Obtain the speaker volume
This API is used to obtain the speaker volume. An "int" value is returned to indicate the speaker volume. Value 101 represents the API SetSpeakerVolume has not been called.
"Level" indicates the real-time volume, and "Volume" the speaker volume. The ultimate volume equals to Level*Volume%. For example, if the value for "Level" is 100 and the one for "Volume" is 60, the ultimate volume will be "60".

#### Function prototype  

```
ITMGContext GetAudioCtrl -(int)GetSpeakerVolume
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerVolume];
```


### Enable in-ear monitoring
This API is used to enable in-ear monitoring.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(QAVResult)EnableLoopBack:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable | boolean | Specifies whether to enable in-ear monitoring |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableLoopBack:YES];
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
ITMGContext GetAudioEffectCtrl -(QAVAccResult)StartAccompany:(NSString*)filePath loopBack:(BOOL)loopBack loopCount:(int)loopCount
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | NSString | Accompaniment's playback path |
| loopBack | boolean | Indicates whether to send a mix. This is generally set to true, indicating that other users can also hear the accompaniment. |
| loopCount | int | Indicates the number of loops. Value -1 means an infinite loop. |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StartAccompany:path loopBack:isLoopBack loopCount:loopCount];
```

### Callback for accompaniment playback
After the accompaniment is over, the event message ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH is returned, which is identified in the OnEvent function.
#### Sample code  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH：
        {
	    //Callback for accompaniment playback
        }
            break;
    }
}
```

### Stop playing back the accompaniment
This API is used to stop playing back the accompaniment.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVAccResult)StopAccompany:(int)duckerTime
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| duckerTimeMs    |int             | Indicates the fading time |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StopAccompany:duckerTime];
```

### Indicate whether the accompaniment is over
If it is over, "YES" is returned. If it is not, "NO" is returned.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(bool)IsAccompanyPlayEnd
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] IsAccompanyPlayEnd];
```

### Pause playing back the accompaniment
This API is used to pause playing back the accompaniment.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVAccResult)PauseAccompany
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PauseAccompany];
```

### Resume playing back the accompaniment
This API is used to resume playing back the accompaniment.
#### Function prototype  

```
GetAudioEffectCtrl -(QAVAccResult)ResumeAccompany
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] ResumeAccompany];
```

### Set the accompaniment volume
This API is used to set the accompaniment volume, which ranges from 0 to 200. It defaults to 100. A value greater than 100 means "volume up", while a value less than 100 means "volume down".
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVAccResult)SetAccompanyVolume:(int)vol
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| vol | int | Indicates the volume value |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetAccompanyVolume:volume];
```

### Obtain the volume of the accompaniment
This API is used to get the accompaniment volume.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(int)GetAccompanyVolume
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] GetAccompanyVolume];
```

### Obtain the accompaniment playback progress
The following two APIs are used to obtain the accompaniment playback progress. Note: Current/Total = current loop times and Current % Total = current loop playback position.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(int)GetAccompanyFileTotalTimeByMs
ITMGContext GetAudioEffectCtrl -(int)GetAccompanyFileCurrentPlayedTimeByMs
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] GetAccompanyFileTotalTimeByMs];
[[[ITMGContext GetInstance] GetAudioEffectCtrl] GetAccompanyFileCurrentPlayedTimeByMs];
```

### Set the playback progress
This API is used to set the playback progress.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVAccResult)SetAccompanyFileCurrentPlayedTimeByMs:(uint) time
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| time | uint | Indicates the playback progress in milliseconds |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetAccompanyFileCurrentPlayedTimeByMs:time];
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
ITMGContext GetAudioEffectCtrl -(QAVResult)PlayEffect:(int)soundId filePath:(NSString*)filePath loop:(BOOL)loop
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |
| filePath | NSString | Indicates the sound effect path |
| loop | boolean | Indicates whether to repeat playback |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PlayEffect:soundId filePath:path loop:isLoop];
```

### Pause the sound effect
This API is used to pause playing back the sound effect.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)PauseEffect:(int)soundId
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PauseEffect:soundId];
```

### Pause all sound effects
This API is used to pause all sound effects.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)PauseAllEffects
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PauseAllEffects];
```

### Resume playing back the sound effect
This API is used to resume playing back the sound effect.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)ResumeEffect:(int)soundId
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] ResumeEffect:soundId];
```

### Resume playing back all sound effects
This API is used to resume playing back all sound effects.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)ResumeAllEffects
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] ResumeAllEffects];
```

### Stop the sound effect
This API is used to stop the sound effect.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)StopEffect:(int)soundId
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| soundId | int | Indicates the sound effect ID |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StopEffect:soundId];
```

### Stop all sound effects
This API is used to stop all sound effects.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)StopAllEffects
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StopAllEffects];
```

### Voice changing effects
This API is used to set the voice changing effects.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)SetVoiceType:(ITMG_VOICE_TYPE) type
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
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetVoiceType:0];
```

### Special karaoke sound effects
This API is used to set special karaoke sound effects.
#### Function prototype  
```
ITMGContext GetAudioEffectCtrl -(QAVResult)SetKaraokeType:(ITMG_KARAOKE_TYPE) type
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
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetKaraokeType:0];
```

### Obtain the volume of sound effects
This API is used to obtain the volume (linear volume) of sound effects, which ranges from 0 to 200. It defaults to 100. A value greater than 100 means "volume up", while a value less than 100 means "volume down".
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(int)GetEffectsVolume
```
#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] GetEffectsVolume];
```

### Set the volume of sound effects
This API is used to set the volume of sound effects.
#### Function prototype  

```
ITMGContext GetAudioEffectCtrl -(QAVResult)SetEffectsVolume:(int)volume
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume | int | Indicates the volume value |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioEffectCtrl] SetEffectsVolume:(int)Volume];
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
|SpeechToText | Converts the voice file into text with Automatic Speech Recognition |



### Authentication initialization
Call authentication initialization after initializing the SDK. To obtain authBuffer, see the API of voice chat authentication.
#### Function prototype  
```
ITMGContext GetPTT -(QAVResult)ApplyPTTAuthbuffer:(NSData *)authBuffer
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| authBuffer | NSData* | Authentication |

#### Sample code  
```
[[[ITMGContext GetInstance]GetPTT]ApplyPTTAuthbuffer:(NSData *)authBuffer];
```

### Specify the maximum length of a voice message
This API is used to specify the maximum length of a voice message, which is limited to 60 seconds.

#### Function prototype  

```
ITMGContext GetPTT -(void)SetMaxMessageLength:(int)msTime
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| msTime    |int                    |Indicates the length of a voice message in ms |

#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]SetMaxMessageLength:(int)msTime];
```

### Start recording
This API is used to start recording. The recorded file must be uploaded before you can perform operations such as voice-to-text converting.
#### Function prototype  

```
ITMGContext GetPTT -(void)StartRecording:(NSString*)fileDir
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileDir | NSString | Indicates the path for storing the voice file |

#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]StartRecording:path];
```

### Callback for starting recordings
The callback function OnEvent is called after the recording is started. The event message ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE is returned, which is identified in the OnEvent function.

#### Sample code  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE：
        {
	    //Callback for recording
        }
            break;
    }
}
```


### Start streaming speech recognition
This API is used to start streaming speech recognition. Texts obtained from voice-to-text converting will be returned in real time in its callback. It can specify a language for recognition, or translate the information recognized in speech into a specified language and return it.


#### Function prototype  

```
ITMGContext GetPTT int StartRecordingWithStreamingRecognition(const NSString* filePath)
ITMGContext GetPTT int StartRecordingWithStreamingRecognition(const NSString* filePath,const NSString*speechLanguage,const NSString*translateLanguage)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | NSString* | Indicates the path for storing the voice file |
| speechLanguage | NSString* | Indicates the language used to express the identified voice. See [Language Parameter Reference Table](https://cloud.tencent.com/document/product/607/30282) |
| translateLanguage | NSString* | Indicates the language into which the voice will be translated. See [Language Parameter Reference Table](https://cloud.tencent.com/document/product/607/30282) (This parameter is unavailable. Enter the same value as that of speechLanguage) |

#### Sample code  
```
[[[ITMGContext GetInstance] GetPTT] StartRecordingWithStreamingRecognition:recordfilePath  speechLanguage:@"cmn-Hans-CN" translateLanguage:@"cmn-Hans-CN"];
```


### Callback for starting streaming speech recognition
The callback function OnEvent is called after the speech recognition is started. The event message ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE is returned, which is identified in the OnEvent function. The passed parameter includes the following messages.

| Message Name | Description |
| ------------- |:-------------:|
| result | Error code indicating whether streaming speech recognition is successful |
| text | Indicates the text obtained from voice-to-text converting |
| file_path | Indicates the local path for saving the recording |
| file_id | Indicates the URL to background recording |

| Error Code | Description | Recommended Action |
| ------------- |:-------------:|:-------------:|
|32775	| Recording is successful, but streaming voice-to-text converting failed	| Call the API UploadRecordedFile to upload the recording, and then call the API SpeechToText to perform voice-to-text converting.
|32777	| Recording is successful and is uploaded, but streaming voice-to-text converting failed.	| The message returned includes a backend URL for successful upload. Call the API SpeechToText to perform voice-to-text converting.

#### Sample code  
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE：
        {
	    // Callback for streaming speech recognition
        }
            break;
    }
}

```

### Stop recording
This API is used to stop recording. It is an asynchronous API. A callback is returned after recording. After it is successful, the recording file is available.
#### Function prototype  

```
ITMGContext GetPTT -(QAVResult)StopRecording
```
#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]StopRecording];
```

### Cancel recording
This API is used to cancel recording. There is no callback after cancellation.
#### Function prototype  

```
ITMGContext GetPTT -(QAVResult)CancelRecording
```
#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]CancelRecording];
```

### Obtain real-time microphone volume of voice message
This API is used to obtain real-time microphone volume. An "int" value is returned. Value range: 0-200.

#### Function prototype  
```
ITMGContext GetPTT -(QAVResult)GetMicLevel
```
#### Sample code  
```
[[[ITMGContext GetInstance]GetPTT]GetMicLevel];
```


### Obtain real-time speaker volume
This API is used to obtain real-time speaker volume. An "int" value is returned. Value range: 0-200.

#### Function prototype  
```
ITMGContext GetPTT -(QAVResult)GetSpeakerLevel
```

#### Sample code  
```
[[[ITMGContext GetInstance]GetPTT]GetSpeakerLevel];
```




### Upload voice files
This API is used to upload voice files.
#### Function prototype  

```
ITMGContext GetPTT -(void)UploadRecordedFile:(NSString*)filePath 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | NSString | Indicates the path for uploading voice files |

#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]UploadRecordedFile:path];
```

### Callback for uploading voice files
After the voice file is uploaded, the event message ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE is returned, which is identified in the OnEvent function.
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE：
        {
	    //Voice file uploaded successfully
        }
            break;
    }
}
```

### Download voice files
This API is used to download voice files.
#### Function prototype  

```
ITMGContext GetPTT -(void)DownloadRecordedFile:(NSString*)fileId downloadFilePath:(NSString*)downloadFilePath 
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID | NSString | URL to the file |
| downloadFilePath | NSString | Local path for saving the file |

#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]DownloadRecordedFile:fileIdpath downloadFilePath:path];
```

### Callback for downloading voice files
After the voice file is downloaded, the event message ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE is returned, which is identified in the OnEvent function.
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE：
        {
	    //Downloaded successfully   
        }
            break;
    }
}
```

### Play voice files
This API is used to play voice files.
#### Function prototype  

```
ITMGContext GetPTT -(void)PlayRecordedFile:(NSString*)downloadFilePath
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| downloadFilePath | NSString | Path to the file |

#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]PlayRecordedFile:path];
```

### Callback for playing voice files
After the voice file is played back, the event message ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE is returned, which is identified in the OnEvent function.
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE：
        {
	    //Callback for playing a voice file 
        }
            break;
    }
}
```

### Stop playing voice files
This API is used to stop playing back voice files.
#### Function prototype  

```
ITMGContext GetPTT -(int)StopPlayFile
```
#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]StopPlayFile];
```

### Obtain the size of a voice file
This API is used to get the size of a voice file.
#### Function prototype  

```
ITMGContext GetPTT -(int)GetFileSize:(NSString*)filePath
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | NSString | Path to the voice file |

#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]GetFileSize:path];
```

### Obtain the length of a voice file
This API is used to obtain the length of a voice file (in milliseconds).
#### Function prototype  

```
ITMGContext GetPTT -(int)GetVoiceFileDuration:(NSString*)filePath
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | NSString | Path to the voice file |

#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]GetVoiceFileDuration:path];
```

### Convert the specified voice file into text with Automatic Speech Recognition
This API is used to convert the specified voice file into text with Automatic Speech Recognition.
#### Function prototype  

```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID | NSString | URL to the voice file |

#### Sample code  

```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID];
```

### Translate the specified voice file into text (specified language)
### This API is used to translate the specified voice file into text of specified language.


#### Function prototype  
```
ITMGContext GetPTT -(void)SpeechToText:(NSString*)fileID (NSString*)speechLanguage (NSString*)translateLanguage
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID | NSString* | URL to the voice file |
| speechLanguage | NSString* | Indicates the language used to express the identified voice. See [Language Parameter Reference Table](https://cloud.tencent.com/document/product/607/30282) |
| translatelanguage | NSString* | Indicates the language into which the voice will be translated. See [Language Parameter Reference Table](https://cloud.tencent.com/document/product/607/30282) (This parameter is unavailable. Enter the same value as that of speechLanguage) |

#### Sample code  
```
[[[ITMGContext GetInstance]GetPTT]SpeechToText:fileID speechLanguage:"cmn-Hans-CN" translateLanguage:"cmn-Hans-CN"];
```



### Callback for Automatic Speech Recognition
After the specified voice file is converted into text with Automatic Speech Recognition, the event message ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE is returned, which is identified in the OnEvent function.
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE：
        {
	    //Voice file recognized successfully       
        }
            break;   
    }
}
```
## Advanced APIs

### Obtain the version number
This API is used to get the SDK version number for analysis.
#### Function prototype

```
ITMGContext  -(NSString*)GetSDKVersion
```
#### Sample code  

```
[[ITMGContext GetInstance] GetSDKVersion];
```

### Set the level of logs to be printed
This API is used to set the level of logs to be printed. It is recommended to maintain the default level.
#### Function prototype
```
ITMGContext -(void)SetLogLevel:(ITMG_LOG_LEVEL)levelWrite (ITMG_LOG_LEVEL)levelPrint
```



#### Parameter description

| Parameter | Type | Description |
|---|---|---|
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written, TMG_LOG_LEVEL_NONE means not to write |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed, TMG_LOG_LEVEL_NONE means not to print |




| ITMG_LOG_LEVEL | Description |
| -------------------------------|:-------------:|
|TMG_LOG_LEVEL_NONE=0		| Do not print logs			|
|TMG_LOG_LEVEL_ERROR=1		| Prints error logs (default)	|
|TMG_LOG_LEVEL_INFO=2			| Prints prompt logs		|
|TMG_LOG_LEVEL_DEBUG=3		| Prints development and debugging logs	|
|TMG_LOG_LEVEL_VERBOSE=4		| Prints high-frequency logs		|

#### Sample code  
```
[[ITMGContext GetInstance] SetLogLevel:TMG_LOG_LEVEL_NONE YES YES];
```

### Set the path of logs to be printed
This API is used to set the path of the log to be printed. The default path is: /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents.
#### Function prototype
```
ITMGContext -(void)SetLogPath:(NSString*)logDir
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| logDir | NSString | Path |

#### Sample code  
```
[[ITMGContext GetInstance] SetLogPath:Path];
```


### Obtain diagnostic messages
This API is used to obtain information about the quality of real-time audio/video calls. This API is mainly used to check the quality of real-time calls and troubleshoot problems, and can be ignored for this service.
#### Function prototype  

```
ITMGContext GetRoom -(NSString*)GetQualityTips
```
#### Sample code  

```
[[[ITMGContext GetInstance]GetRoom ] GetQualityTips];
```

### Add an ID to the audio data blacklist
This API is used to add an ID to the audio data blacklist. A return value of 0 indicates that the call is successful.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(QAVResult)AddAudioBlackList:(NSString*)openID
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| openID | NSString | Indicates the ID to be added to the blacklist |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] AddAudioBlackList[id]];
```

### Remove an ID from the audio data blacklist
This API is used to remove an ID from the audio data blacklist. A return value of 0 indicates that the call is successful.
#### Function prototype  

```
ITMGContext GetAudioCtrl -(QAVResult)RemoveAudioBlackList:(NSString*)openID
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| openID | NSString | Indicates the ID to be removed from the blacklist |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] RemoveAudioBlackList[openId]];
```
## Callback Messages

#### Message list:

| Message | Description   
| ------------- |:-------------:|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    				       | Indicates that a member enters an audio room |
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    				         	| Indicates that a member exits an audio room |
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    		       | Indicates that a room is disconnected due to network or other reasons |
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE				| Indicates a room type change event |
|ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH		| Indicates that the accompaniment is over			|
|ITMG_MAIN_EVNET_TYPE_USER_UPDATE		| Indicates that the room members are updated		|
|ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE	| Indicates that PTT recording is completed			|
|ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE	| Indicates that the PTT is successfully uploaded			|
|ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	| Indicates that the PTT is successfully downloaded			|
|ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE		| Indicates that the playback of PTT is completed			|
|ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	| Indicates that the voice-to-text converting is completed			|

#### Data list:

| Message     | Data         | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    		|result; error_info			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    		|result; error_info  			|{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    	|result; error_info  			|{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    	|result; error_info; sub_event_type; new_room_type	|{"error_info":"","new_room_type":0,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE    	|result; error_info  			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Microphone (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE    	|result; error_info 			|{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Microphone (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0}|
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE    		|user_list;  event_id			|{"event_id":1,"user_list":["0"]}|
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE 	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE	|result; file_path;file_id  		|{"file_id":"","file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE 	|result; file_path  			|{"file_path":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE	|result; text;file_id		|{"file_id":"","text":"","result":0}|
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE	|result; file_path; text;file_id		|{"file_id":"","file_path":","text":"","result":0}|
