This document describes how to access and debug the GME APIs for iOS.

>?This document applies to GME SDK v2.5.

## Key Considerations for Using GME

| Important API | Description |
| ------------- |:-------------:|
|InitEngine           | Initializes GME |
|Poll    | Triggers event callback |
|SetDefaultAudienceAudioCategory | Sets use in background |
|EnterRoom | Enters room  |
|EnableMic | Enables mic |
|EnableSpeaker | Enables speaker |

>?
>- Configure your project before using GME; otherwise, the SDK will not take effect.
>- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
>- GME APIs should be called in the same thread.
>- The `Poll` API should be called periodically for GME to trigger event callbacks.
>- For GME callback messages, please see the callback message list.
>- Operation on devices should be performed after successful room entry.
>- For detailed error codes, please see [Error Codes](https://intl.cloud.tencent.com/document/product/607/15173).

## Voice Chat Flowchart
![](https://main.qcloudimg.com/raw/e536525aa47c06a5a84bb6c8d4851b22.png)

## Key APIs
Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice messaging and speech-to-text features.
If you have any questions when using the service, please see [General FAQs](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------------- |:-------------:|
|InitEngine           | Initializes GME |
|Poll    | Triggers event callback |
|Pause   | Pauses system |
|Resume | Resumes system |
|Uninit    | Uninitializes GME |
|SetDefaultAudienceAudioCategory | Sets audio playback in background on device |

### Getting singleton
To use the voice feature, get the `ITMGContext` object first.
#### Function prototype

```
ITMGContext ITMGDelegate <NSObject>
```



#### Sample code 

```
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate =self;
```

### Message delivery
The API class uses the `Delegate` method to send callback notifications to the application. For the message type, please see `ITMG_MAIN_EVENT_TYPE`. The message content is a dictionary for receiving callback messages.
#### Function prototype

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
```



#### Sample code 
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
switch (eventType) {
// Identify `eventType`
}
}
```





### Initializing the SDK

For more information on how to get parameters, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/10782).
This API requires the `AppID` from the Tencent Cloud Console and the `openID` as parameters. The `openID` uniquely identifies a user with the rules stipulated by the application developer and must be unique in the application (currently, only INT64 is supported).

>!The SDK must be initialized before a client can enter a room.
>
>#### Function prototype

```
ITMGContext -(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openId
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| sdkAppId    |NSString  | `AppId` from the Tencent Cloud Console. |
| openId    |NSString  | `OpenID` can only be in Int64 type (converted to string) with a value greater than 10,000, which is used to identify the user. |


| Returned Value | Description |
|----|----|
|QAV_OK= 0| Initialized SDK successfully. |
|QAV_ERR_SDK_NOT_FULL_UPDATE= 7015| Check whether the SDK file is complete. You are recommended to delete it and then import the SDK again. |

#### Sample code


```
[[ITMGContext GetInstance] InitEngine:SDKAPPID3RD openID:_openId];
```
### Triggering event callback
Event callbacks can be triggered by periodically calling the `Poll` API in `update`.
#### Function prototype

```
ITMGContext -(void)Poll
```
#### Sample code
```
[[ITMGContext GetInstance] Poll];
```

### Pausing system
When a `Pause` event occurs in the system, the engine should also be notified for pause.
#### Function prototype

```
ITMGContext -(QAVResult)Pause
```

### Resuming system
When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.
#### Function prototype

```
ITMGContext -(QAVResult)Resume
```



### Uninitializing the SDK
This API is used to uninitialize the SDK to make it uninitialized. Switching accounts requires uninitialization.
#### Function prototype

```
ITMGContext -(void)Uninit
```
#### Sample code
```
[[ITMGContext GetInstance] Uninit];
```



### Setting audio playback in background
This API is used to set audio playback in the background and should be called before room entry.
Meanwhile, you should pay attention to the following two points in the application:
- Audio engine capture and playback are not paused when the application is switched to the background (i.e., `PauseAudio`);
- You need to add at least `key:Required background modes` and `string:App plays audio or streams audio/video using AirPlay` to the `Info.plist` of the application.

#### Function prototype
```
ITMGContext -(QAVResult)SetDefaultAudienceAudioCategory:(ITMG_AUDIO_CATEGORY)audioCategory
```

| Type     | Parameter         | Description |
| ------------- |:-------------:|-------------|
| ITMG_CATEGORY_AMBIENT    |0 | Audio is not played back in the background (default value) |
| ITMG_CATEGORY_PLAYBACK    |1   | Audio is played back in the background |

The specific implementation is to modify `kAudioSessionProperty_AudioCategory`. For more information, please see Apple's official documentation.


#### Sample code 
```
[[ITMGContext GetInstance]SetDefaultAudienceAudioCategory:ITMG_CATEGORY_AMBIENT];
```

## Voice Chat Room Call Flowchart

![](https://main.qcloudimg.com/raw/a61ca1d7cdecf09bd223766b2a5cd69f.png)

## Voice Chat Room APIs
You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, please see [FAQs About Voice Chat](https://intl.cloud.tencent.com/document/product/607/30257).

| API | Description |
| ------------- |:-------------:|
|GenAuthBuffer    | Initializes authentication |
| EnterRoom | Enters room |
|IsRoomEntered   | Indicates whether room entry is successful |
|ExitRoom | Exits room |
|ChangeRoomType | Modifies user's room audio type |
|GetRoomType | Gets user's room audio type |


### Authentication information
Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).   
To get authentication for voice messaging and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype
```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| appId    |int   | `AppId` from the Tencent Cloud Console. |
| roomId    |NSString  | Room ID, which can contain up to 127 characters (for voice messaging and speech-to-text feature, enter `null`). |
| openID  |NSString    | User ID, which is the same as `openID` during initialization. |
| key    |NSString    | Permission key from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme). |



#### Sample code 
```
NSData* authBuffer =   [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];
```



### Entering room
When a client enters a room with the generated authentication information, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` message will be received as a callback. Mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates a success.


#### Function prototype
```
ITMGContext   -(int)EnterRoom:(NSString*) roomId roomType:(int)roomType authBuffer:(NSData*)authBuffer
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId |NSString | Room ID, which can contain up to 127 characters |
| roomType |int | Room audio type |
| authBuffer    |NSData    | Authentication key |

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).


#### Sample code 
```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];
```

### Callback for room entry
After the client enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function.

#### Sample code 
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
           // Receive the event of successful room entry
        }
            break;
}
}
```

#### Data details
| Message | Data | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info |{"error_info":"","result":0}|

#### Error codes
| Error Code Value | Cause and Suggested Solution |
|-------|------------|
|7006| Authentication failed. Possible causes: 1. The `AppID` does not exist or is incorrect; 2. An error occurred while authenticating the `authbuff`; 3. Authentication expired; 4. The `openID` is non-compliant. |
|7007| Already in another room. |
|1001   | The client was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
|1003   | The client was already in the room and called the room entering API again. |
|1101   | Make sure that the SDK is initialized, the APIs are called in the same thread, and the `Poll` API is called normally. |

### Determining whether client has entered room
This API is used to determine whether the client has entered a room. A bool-type value will be returned.
#### Function prototype 
```
ITMGContext -(BOOL)IsRoomEntered
```
#### Sample code 
```
[[ITMGContext GetInstance] IsRoomEntered];
```

### Exiting room
This API is called to exit the current room. It is an async API. The returned value of `AV_OK` indicates a successful async delivery.

>!If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.

#### Function prototype 
```
ITMGContext -(int)ExitRoom
```
#### Sample code 
```
[[ITMGContext GetInstance] ExitRoom];
```

### Callback for room exit
After the client exits a room, a callback will be returned with the message being `ITMG_MAIN_EVENT_TYPE_EXIT_ROOM`.
#### Sample code 
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
        {
            // Receive the event of successful room exit
        }
            break;
    }
}
```

#### Data details

| Message | Data | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|


### Modifying user's room audio type
This API is used to modify a user's room audio type. For the result, please see the callback event. The event type is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE`.

#### Function prototype 
```
ITMGContext GetRoom -(int)ChangeRoomType:(int)nRoomType
```


| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| nRoomType    | int    | Room type to be switched to. For room audio types, please see the `EnterRoom` API |

#### Sample code 
```
[[[ITMGContext GetInstance]GetRoom ]ChangeRoomType:_roomType];
```


### Getting user's room audio type
This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, please see the `EnterRoom` API.

#### Function prototype 
```
ITMGContext GetRoom -(int)GetRoomType
```

#### Sample code 
```
[[[ITMGContext GetInstance]GetRoom ]GetRoomType];
```


### Callback for room type setting completion
After the room type is set, the event message `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE` will be returned in the callback. The returned parameters include `result`, `error_info`, and `new_room_type`. The `new_room_type` represents the following information. The event message will be identified in the `OnEvent` function.

| Event Subtype | Parameter | Description |
| ------------- |:-------------:|-------------|
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM|1 | Indicates that the existing audio type is inconsistent with and changed to that of the entered room|
| ITMG_ROOM_CHANGE_EVENT_START |2 | Indicates that a client is already in the room and the audio type starts changing (e.g., calling the `ChangeRoomType` API to change the audio type) |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE |3 | Indicates that a client is already in the room and the audio type has been changed |
| ITMG_ROOM_CHANGE_EVENT_REQUEST |4 | Indicates that a room member calls the `ChangeRoomType` API to request a change of room audio type |


#### Sample code 
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
  case ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE:
// Process
}
    }
}
```

#### Data details
| Message | Data | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type |{"error_info":"","new_room_type":0,"result":0}|


### Member status change
Notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at a higher layer. The event message is `ITMG_MAIN_EVNET_TYPE_USER_UPDATE`, where the data contains `event_id` and `user_list`. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds.

|event_id     | Description | Maintenance |
| ------------- |:-------------:|-------------|
|ITMG_EVENT_ID_USER_ENTER    | A member enters the room | Member list |
|ITMG_EVENT_ID_USER_EXIT    | A member exits the room | Member list |
|ITMG_EVENT_ID_USER_HAS_AUDIO    | A member sends audio packets | Chat member list |
|ITMG_EVENT_ID_USER_NO_AUDIO    | A member stops sending audio packets | Chat member list |

#### Room member maintenance flowchart

![](https://main.qcloudimg.com/raw/50ef1ceda14eb244e434b8cbe85da5f3.png)


#### Sample code
```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
{
// Process
// Parse the parameter to get `event_id` and `user_list`
    switch (eventID)
      {
      case ITMG_EVENT_ID_USER_ENTER:
      // A member enters the room
      break;
      case ITMG_EVENT_ID_USER_EXIT:
      // A member exits the room
    break;
    case ITMG_EVENT_ID_USER_HAS_AUDIO:
    // A member sends audio packets
    break;
    case ITMG_EVENT_ID_USER_NO_AUDIO:
    // A member stops sending audio packets
    break;
      }
break;
}
    }
}
```

### Room call quality control event
The message for quality control event is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `floss`, and `delay`, which represent the following information. The event message will be identified in the `OnEvent` function.

| Parameter | Description |
| ------------- |-------------|
|weight    | Value range: 1–5. 5 indicates excellent sound quality, 1 indicates very poor (barely usable) sound quality, and 0 represents an initial meaningless value |
|floss    | Packet loss rate |
|delay    | Voice chat delay in ms |




### Message details

| Message | Description  |
| ------------- |-------------|
|ITMG_MAIN_EVENT_TYPE_ENTER_ROOM           | Indicates that a member enters an audio/video room |
|ITMG_MAIN_EVENT_TYPE_EXIT_ROOM             | Indicates that a member exits an audio/video room |
|ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT           | Indicates that a room is disconnected for network or other reasons |
|ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | Indicates a room type change event |

### Details of data corresponding to the message

| Message | Data | Example |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM    |result; error_info |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM    |result; error_info  |{"error_info":"","result":0}|
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT    |result; error_info  |{"error_info":"waiting timeout, please check your network","result":0}|
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE    |result; error_info; new_room_type |{"error_info":"","new_room_type":0,"result":0}|


## Voice Chat Audio APIs
The voice chat APIs can only be called after SDK initialization and room entry.
When Enable/Disable Mic/Speaker is clicked on the UI, the following practices are recommended:
- For most game applications, you are recommended to call the `EnableMic` and `EnableSpeaker` APIs, which is equivalent to calling the `EnableAudioCaptureDevice/EnableAudioSend` and `EnableAudioPlayDevice/EnableAudioRecv` APIs;
- For other mobile applications (such as social networking applications), enabling/disabling a capturing device will restart both capturing and playback devices. If the application is playing back background music, it will also be interrupted. Playback won't be interrupted if the mic is enabled/disabled through control of upstreaming/downstreaming. Calling method: call `EnableAudioCaptureDevice(true)` and `EnableAudioPlayDevice(true)` once after room entry, and call `EnableAudioSend/Recv` to send/receive audio streams when Enable/Disable Mic is clicked.
- For more information on how to release only a capturing or playback device, please see the `EnableAudioCaptureDevice` and `EnableAudioPlayDevice`.
- Call the `pause` API to pause the audio engine and call the `resume` API to resume the audio engine.

| API | Description |
| ------------- |:-------------:|
|EnableMic | Enables/disables mic |
|GetMicState    | Gets mic status |
|EnableAudioCaptureDevice    | Enables/disables capturing device |
|IsAudioCaptureDeviceEnabled    | Gets capturing device status |
|EnableAudioSend    | Enables/disables audio upstreaming |
|IsAudioSendEnabled    | Gets audio upstreaming status |
|GetMicLevel    | Gets real-time mic volume level |
|GetSendStreamLevel | Gets real-time audio upstreaming volume level |
|SetMicVolume    | Sets mic volume level |
|GetMicVolume    | Gets mic volume level |
|EnableSpeaker    | Enables/disables speaker |
|GetSpeakerState    | Gets speaker status |
|EnableAudioPlayDevice    | Enables/disables playback device |
|IsAudioPlayDeviceEnabled    | Gets playback device status |
|EnableAudioRecv    | Enables/disables audio downstreaming |
|IsAudioRecvEnabled    | Gets audio downstreaming status |
|GetSpeakerLevel    | Gets real-time speaker volume level |
|GetRecvStreamLevel | Gets real-time downstreaming audio levels of other members in room |
|SetSpeakerVolume    | Sets speaker volume level |
|GetSpeakerVolume    | Gets speaker volume level |
|EnableLoopBack    | Enables/disables in-ear monitoring |



### Enabling/Disabling the mic
This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.
EnableMic = EnableAudioCaptureDevice + EnableAudioSend.

#### Function prototype 
```
ITMGContext GetAudioCtrl -(QAVResult)EnableMic:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     | To enable the mic, set this parameter to `YES`; otherwise, set it to `NO` |

#### Sample code 
```
Enable the mic:
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
```

### Getting mic status
This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 on.
#### Function prototype 
```
ITMGContext GetAudioCtrl -(int)GetMicState
```
#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicState];
```

### Enabling/Disabling capture device
This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.
- This API can only be called after room entry. The device will be disabled automatically after room exit.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### Function prototype 
```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enabled    |BOOL     | To enable a capturing device, set this parameter to `YES`; otherwise, set it to `NO` |

#### Sample code

```
Enable a capturing device
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioCaptureDevice:enabled];
```

### Getting capturing device status
This API is used to get the status of a capturing device.
#### Function prototype

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioCaptureDeviceEnabled
```
#### Sample code

```
BOOL IsAudioCaptureDevice = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioCaptureDeviceEnabled];
```

### Enabling/Disabling audio upstreaming
This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### Function prototype

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioSend:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable    |BOOL     | To enable audio upstreaming, set this parameter to `YES`; otherwise, set it to `NO` |

#### Sample code 

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioSend:enabled];
```

### Getting audio upstreaming status
This API is used to get the status of audio upstreaming.
#### Function prototype 
```
ITMGContext GetAudioCtrl -(BOOL)IsAudioSendEnabled
```
#### Sample code 
```
BOOL IsAudioSend =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioSendEnabled];
```

### Getting real-time mic volume level
This API is used to get the real-time mic volume level. An int-type value will be returned. It is recommended to call this API once every 20 ms.
#### Function prototype 
```
ITMGContext GetAudioCtrl -(int)GetMicLevel
```
#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicLevel];
```

### Getting real-time audio upstreaming volume level
This API is used to get the real-time audio upstreaming volume level. An int-type value will be returned. Value range: 0–100.
#### Function prototype 
```
ITMGContext GetAudioCtrl -(int)GetSendStreamLevel()
```
#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSendStreamLevel];
```

### Setting mic volume level
This API is used to set the mic volume level. The corresponding parameter is `volume`. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.

#### Function prototype 
```
ITMGContext GetAudioCtrl -(QAVResult)SetMicVolume:(int) volume
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| volume    |int      | Volume level. Value range: 0–200 |

#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] SetMicVolume:100];
```
### Getting mic volume level
This API is used to get the mic volume level. An int-type value will be returned. 101 indicates that the `SetMicVolume` API has not been called.

#### Function prototype 
```
ITMGContext GetAudioCtrl -(int) GetMicVolume
```
#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicVolume];
```

### Enabling/Disabling the speaker
This API is used to enable/disable the speaker.
EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv.
#### Function prototype 
```
ITMGContext GetAudioCtrl -(void)EnableSpeaker:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| isEnabled    |boolean       | To disable the speaker, set this parameter to `NO`; otherwise, set it to `YES` |

#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
```

### Getting speaker status
This API is used to get the speaker status. 0 indicates that the speaker is off, 1 on, and 2 working.
#### Function prototype 
```
ITMGContext GetAudioCtrl -(int)GetSpeakerState
```

#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerState];
```



### Enabling/Disabling playback device
This API is used to enable/disable a playback device.

#### Function prototype 
```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioPlayDevice:(BOOL)enabled
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enabled    |BOOL        | To disable a playback device, set this parameter to `NO`; otherwise, set it to `YES` |

#### Sample code 
```
Enable a playback device
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioPlayDevice:enabled];
```

### Getting playback device status
This API is used to get the status of a playback device.
#### Function prototype

```
ITMGContext GetAudioCtrl -(BOOL)IsAudioPlayDeviceEnabled
```
#### Sample code 

```
BOOL IsAudioPlayDevice =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioPlayDeviceEnabled];
```

### Enabling/Disabling audio downstreaming
This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### Function prototype 

```
ITMGContext GetAudioCtrl -(QAVResult)EnableAudioRecv:(BOOL)enabled
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enabled    |BOOL     | To enable audio downstreaming, set this parameter to `YES`; otherwise, set it to `NO` |

#### Sample code 

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioRecv:enabled];
```



### Getting audio downstreaming status
This API is used to get the status of audio downstreaming.
#### Function prototype 
```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### Sample code 
```
BOOL IsAudioRecv = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioRecvEnabled];
```

### Getting real-time speaker volume level
This API is used to get the real-time speaker volume level. An int-type value will be returned to indicate the volume level. It is recommended to call this API once every 20 ms.
#### Function prototype 
```
ITMGContext GetAudioCtrl -(int)GetSpeakerLevel
```

#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerLevel];
```

### Getting real-time downstreaming audio levels of other members in room
This API is used to get the real-time audio downstreaming volume levels of other members in the room. An int-type value will be returned. Value range: 0–100.
#### Function prototype 
```
ITMGContext GetAudioCtrl -(int)GetRecvStreamLevel:(NSString*) openID
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| openID    |NSString       | `openId` of another member in the room |

#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetRecvStreamLevel:(NSString*) openId
```

### Setting speaker volume level
This API is used to set the speaker volume level.
The corresponding parameter is `volume`. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.

#### Function prototype 
```
ITMGContext GetAudioCtrl -(QAVResult)SetSpeakerVolume:(int)vol
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| vol    |int      | Volume level. Value range: 0–200 |

#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] SetSpeakerVolume:100];
```

### Getting speaker volume level

This API is used to get the speaker volume level. An int-type value will be returned to indicate the volume level. 101 indicates that the `SetSpeakerVolume` API has not been called.
`Level` indicates the real-time volume level, while `Volume` the speaker volume level. The final volume level equals to Level*Volume%. For example, if the value of "Level" is 100 and that of `Volume` is 60, then the final volume level will be 60.

#### Function prototype 
```
ITMGContext GetAudioCtrl -(int)GetSpeakerVolume
```
#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerVolume];
```


### Enabling in-ear monitoring
This API is used to enable in-ear monitoring.
#### Function prototype 
```
ITMGContext GetAudioCtrl -(QAVResult)EnableLoopBack:(BOOL)enable
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| enable    |boolean         | Specifies whether to enable |

#### Sample code 
```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableLoopBack:YES];
```


## Speech-to-Text Conversion Flowchart
<img src="https://main.qcloudimg.com/raw/310eaf2b780c5fc47ffeaf791a6df392.png" width="70%">


## Voice Messaging and Speech-to-Text
Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice messaging and speech-to-text features.
If you have any questions when using the service, please see [Voice Messaging and Speech-to-Text](https://intl.cloud.tencent.com/document/product/607/30258).


### Initialization APIs

| API | Description |
| ------------- |:-------------:|
|Init    | Initializes GME |
|Poll    | Triggers event callback |
|Pause   | Pauses system |
|Resume | Resumes system |
|Uninit    | Uninitializes GME |


### Voice messaging and speech-to-text APIs
| API | Description |
| ------------- |:-------------:|
|ApplyPTTAuthbuffer    | Initializes authentication |
|SetMaxMessageLength    | Specifies maximum length of voice message |
|StartRecording | Starts recording |
|StartRecordingWithStreamingRecognition | Starts streaming recording |
|PauseRecording| Pauses recording |
|ResumeRecording| Resumes recording |
|StopRecording    | Stops recording |
|CancelRecording | Cancels recording |
|GetMicLevel| Gets the real-time mic volume level of voice messaging |
|SetMicVolume| Sets the recording volume level of voice messaging |
|GetMicVolume| Gets the recording volume level of voice messaging |
|GetSpeakerLevel    | Gets the real-time speaker volume level of voice messaging |
|SetSpeakerVolume| Sets the playback volume level of voice messaging |
|GetSpeakerVolume| Gets the playback volume level of voice messaging |
|UploadRecordedFile | Uploads audio file |
|DownloadRecordedFile | Downloads audio file |
|PlayRecordedFile | Plays back audio |
|StopPlayFile | Stops playing back audio |
|GetFileSize | Gets audio file size |
|GetVoiceFileDuration | Gets audio file duration |
|SpeechToText | Converts speech to text |

### Authentication initialization
Call authentication initialization after initializing the SDK. For
