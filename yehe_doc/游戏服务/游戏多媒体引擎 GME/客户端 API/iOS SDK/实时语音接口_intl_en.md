This document describes how to access and debug the GME APIs for iOS.

> ?This document applies to GME SDK v2.8.

## Key Considerations for Using GME

GME provides two services: voice chat service and voice message and speech-to-text service, both of which rely on key APIs such as Init and Poll.

<dx-alert infotype="notice" title="Note on Init API">  
If you need to use voice chat and voice message services, **you only need to call `Init` API once**.
</dx-alert>

![image](https://main.qcloudimg.com/raw/99d612d90268a7248f5b55c385eeb8b8.png)

### Directions

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Entering a voice chat room</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Enabling the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Enabling the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exiting a voice room</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitializing GME</dx-tag-link>
</dx-steps>


### Important notes

- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error code, please see <dx-tag-link link="https://cloud.tencent.com/document/product/607/15173" tag="ErrorCode">Error Codes</dx-tag-link>.

### APIs

```
@class ITMGRoom;//Room APIs
@class ITMGAudioCtrl;//Audio APIs
@class ITMGAudioEffectCtrl;//Sound effect APIs
```

## Key APIs

Before the initialization, the SDK is in the uninitialized status, and **you need to initialize it through the `Init` API** before you can use the voice chat and speech-to-text services.

**You need to call the `Init` API before calling any APIs of GME.**


If you have any questions when using the service, please see [General FAQs](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------------------------------- | :------------------: |
| InitEngine | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |
| SetDefaultAudienceAudioCategory | Sets audio playback in background on device |



### Imported header files


```
#import "GMESDK/TMGEngine.h"
#import "GMESDK/QAVAuthBuffer.h"
```

### Getting singleton

To use the voice feature, get the `ITMGContext` object first.

```
+ (ITMGContext*) GetInstance;
```

#### Sample code  

```
//TMGSampleViewController.m
ITMGContext* _context = [ITMGContext GetInstance];
```


### Setting callbacks

The API class uses the `Delegate` method to send callback notifications to the application. Register the callback function to the SDK for receiving callback messages.


#### Sample code  

`ITMGDelegate` is used for declaration.

```
@interface TMGDemoViewController ()<ITMGDelegate>{}
ITMGDelegate < NSObject >

//TMGSampleViewController.m
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate = [DispatchCenter getInstance];
```


The API callback messages is processed in `OnEvent`. For the message type, please see `ITMG_MAIN_EVENT_TYPE`. The message content is a dictionary for parsing the API callback contents.

#### Function prototype 

```
- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data;
```



#### Sample code  

```
//TMGRealTimeViewController.m
TMGRealTimeViewController ()< ITMGDelegate >


- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
    NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    [self showLog:log];
    NSLog(@"====%@====", log);
    switch (eventType) {
        // Step 6/11 : Perform the enter room event
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM: {
            int result = ((NSNumber *)[data objectForKey:@"result"]).intValue;
            NSString *error_info = [data objectForKey:@"error_info"];

            [self showLog:[NSString stringWithFormat:@"OnEnterRoomComplete:%d msg:(%@)", result, error_info]];

            if (result == 0) {
                [self updateStatusEnterRoom:YES];
            }
        }
        break;
	}
}

// Refer to DispatchCenter.h and DispatchCenter.m
```



### [Initializing SDK](id:Init)

- This API is used to initialize the GME service. It is recommended to call it when initializing the application.
- **For more information on how to get the `sdkAppId` parameter, please see [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/39698)**.
- **The openID uniquely identifies a user with the rules stipulated by the application developer and unique in the application (currently, only INT64 is supported)**.

> !
> - The SDK must be initialized before a user can enter a voice chat room.
> - The Init API must be called in the same thread with other APIs. It is recommended to call all APIs in the main thread.

#### Function prototype

```
-(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID;
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String | `AppId` provided by the GME service from the [Tencent Cloud console](https://console.cloud.tencent.com/gamegme) |
| OpenId |String | `OpenId` can only be in Int64 type, which is passed after being converted to a string. |

| Returned Value | Description |
| --------------------------------- | --------------------------------------------- |
| QAV_OK= 0 | Initialized SDK successfully. |
| QAV_ERR_SDK_NOT_FULL_UPDATE= 7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is only a reminder but will not cause an initialization failure.

- If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- If this error is returned after executable file export, please ignore it and try to avoid displaying it in the UI.

#### Sample code 


```
_openId = _userIdText.text;
_appId = _appIdText.text;
[[ITMGContext GetInstance] InitEngine:SDKAPPID openID:_openId];

```


### [Triggering event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
Refer to the EnginePollHelper.m file in [Demo](https://intl.cloud.tencent.com/document/product/607/18521).

#### Function prototype

```
-(void)Poll;

```

#### Sample code

```
[[ITMGContext GetInstance] Poll];

```

### Pausing system

When a `Pause` event occurs in the system, the engine should also be notified for pause.
If you need to pause the audio when switching to the background, you can call the `Pause` API in the listening code used to switch to the background, and call the `Resume` API in the listening event used to resume the foreground.

#### Function prototype

```
-(QAVResult)Pause;

```

### Resuming system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### Function prototype

```
-(QAVResult)Resume;

```



### [Uninitializing SDK](id:UnInit)

This API is used to uninitialize the SDK to make it uninitialized. **Switching accounts requires uninitialization**.

#### Function prototype

```
-(int)Uninit;

```

#### Sample code

```
[[ITMGContext GetInstance] Uninit];

```



### Audio settings for iOS device

This API is used to set the audio playback in the background, and the GME audio not to be affected by the mute switch or lock screen. For example, when the notification center or control center is opened, you can still receive and play back the GME audio. You need to call this API before room entry.
Meanwhile, you should pay attention to the following two points in the application:
- Audio engine capture and playback are not paused when the application is switched to the background (i.e., `PauseAudio`).
- You need to add at least `key:Required background modes` and `string:App plays audio or streams audio/video using AirPlay` to the `Info.plist` of the application.

>! It is recommended that developers call this API to set the audio.

#### Function prototype

```
-(QAVResult)SetDefaultAudienceAudioCategory:(ITMG_AUDIO_CATEGORY)audioCategory;

```

| Type | Parameter | Description |
| ---------------------- | :------: | ---------------------- |
| ITMG_CATEGORY_AMBIENT | 0 | Audio is not played back in the background (default value) |
| ITMG_CATEGORY_PLAYBACK | 1 | Audio is played back in the background |

The specific implementation is to modify `kAudioSessionProperty_AudioCategory`. For more information, please see Apple's official documentation.


#### Sample code  

```
[[ITMGContext GetInstance]SetDefaultAudienceAudioCategory:ITMG_CATEGORY_AMBIENT];

```


## Voice Chat

Voice chat refers to the one-to-one or one-to-many real-time voice call feature.

### Voice chat flowchart

![](https://main.qcloudimg.com/raw/28a13d4beccdfecb0ad7530008ec8da0.png)





## Voice Chat Room APIs

You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, please see [FAQs About Voice Chat](https://intl.cloud.tencent.com/document/product/607/30257).


| API | Description |
| -------------- | :------------------: |
| GenAuthBuffer | Initializes authentication |
| EnterRoom | Enters room |
| IsRoomEntered | Indicates whether room entry is successful |
| ExitRoom | Exits room |
| ChangeRoomType | Modifies user's room audio type |
| GetRoomType | Gets user's room audio type |

## Voice Chat Room Call Flowchart

![](https://main.qcloudimg.com/raw/2b5d8f7f7f4b4b3fbce8c9ebf01f78d8.png)

### Authentication information

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    


#### Function prototype

```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end

```

| Parameter | Type | Description |
| ------ | :------: | ------------------------------------------------------------ |
| appId | int | `AppId` from the Tencent Cloud console.|
| roomId | NSString | Room ID, which can contain up to 127 characters. |
| openID | NSString | User ID, which is the same as `openID` during initialization. |
| key | NSString | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |



#### Sample code  

```
#import "GMESDK/QAVAuthBuffer.h"
NSData* authBuffer = [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];

```



###  [Entering a room](id:EnterRoom)

When a user enters a room with the generated authentication information, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` message will be received as a callback. Mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates a success.

The audio type of the room is determined by the first user to enter the room. After that, if a member in the room changes the room type, it will take effect for all members there. For example, if the first user entering the room uses the smooth sound quality, and the second user entering the room uses the HD sound quality, the room audio type of the second user will become smooth sound quality. Only when a member in the room calls the `ChangeRoomType` API, the audio type of the room will be changed.

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Function prototype

```
-(int)EnterRoom:(NSString*) roomId roomType:(int)roomType authBuffer:(NSData*)authBuffer;

```

| Parameter | Type | Description |
| ---------- | :------: | ----------------------- |
| roomId | NSString | Room ID, which can contain up to 127 characters |
| roomType | int | Room audio type |
| authBuffer | NSData | Authentication key |




#### Sample code  

```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];

```

### Callback for room entry

After the user enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function for callback and processing. A successful callback means that the room entry is successful, and the billing starts.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/36276)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will the billing continue if the client is disconnected when using the voice chat?](https://intl.cloud.tencent.com/document/product/607/30255)
</dx-fold-block>






#### Sample code  

Sample code for processing the callback, including room entry and network disconnection events.

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* error_info = [data objectForKey:@"error_info"];
           	 //Receive the event of successful room entry
        }
            break;
	}
}

```

#### Data details

| Message | Data | Sample |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |


If the network is disconnected, there will be a disconnected callback prompt `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. At this time, the SDK will automatically reconnect, and the callback is `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.


#### Error codes

| Error Code Value | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006 | Authentication failed <li>The `AppID` does not exist or is incorrect.<li>An error occurred while authenticating the `authbuff`.<li>Authentication expired.<li>The `OpenId` does not meet the specification. |
| 7007 | Already in another room. |
| 1001 | The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
| 1003 | The user was already in the room and called the room entering API again. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |

### [Exiting the room](id:ExitRoom)

This API is called to exit the current room. It is an async API. The returned value of `AV_OK` indicates a successful async delivery.

> !If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.

#### Function prototype  

```
-(int)ExitRoom

```

#### Sample code  

```
[[ITMGContext GetInstance] ExitRoom];

```

### Callback for room exit

After the user exits a room, a callback will be returned with the message being `ITMG_MAIN_EVENT_TYPE_EXIT_ROOM`.

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

| Message | Data | Sample |
| ------------------------------ | :----------------: | ---------------------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | result; error_info | {"error_info":"","result":0} |

### Determining whether user has entered room

This API is used to determine whether the user has entered a room. A bool-type value will be returned. The call is invalid during the process of room entry.

#### Function prototype  

```
-(BOOL)IsRoomEntered;

```

#### Sample code  

```
[[ITMGContext GetInstance] IsRoomEntered];

```


### Switching room

User can call this API to quickly switch the voice chat room after entering the room. After the room is switched, the device is not reset, that is, if the microphone is already enabled in this room, the microphone will keep enabled after the room is switched.

The callback for quickly switching rooms is `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM`, and the fields are `error_info` and `result`.

#### API prototype

```
-(int) SwitchRoom:(NSString *)roomID  authBuffer:(NSData*)authBuffer;

```

#### Type descriptions

| Parameter | Type | Description |
| ------------ | ---------- | ------------------------------ |
| targetRoomID | NSString * | ID of the room to enter |
| authBuffer | NSData* | Generates a new authentication with the ID of the room to enter |

#### Callback sample code

```
- (IBAction)swichRoom:(id)sender {
    NSData* authBuffer = [QAVAuthBuffer GenAuthBuffer:_appId.intValue roomID:_roomIdText.text openID:_openId key:_key];
    [[[ITMGContext GetInstance]GetRoom]SwitchRoom:_roomIdText.text authBuffer:authBuffer];
}

-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    NSString* log =[NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
    [self showLog:log];
    NSLog(@"====%@====",log);
    switch (eventType) {
	case ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM:
        {
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            NSString* log = nil;
            if (result == QAV_OK) {
                log = [NSString stringWithFormat:@"switch room success."];
            } else {
                log = [NSString stringWithFormat:@"switch room failed."];
            }
            [self showLog:log];
            break;
        }
    }
}

```


### Cross-room mic connection

Call this API to connect the microphones across rooms after the room entry. After the call, the local user can communicate with the target OpenID user in the target room.

#### API prototype

```
-(int) StartRoomSharing:(NSString *)targetRoomID targetOpenID:(NSString *)targetOpenID authBuffer:(NSData*)authBuffer;

-(int) StopRoomSharing;

```

#### Type descriptions

| Parameter | Type | Description |
| ------------ | ---------- | ----------------------- |
| targetRoomID | NSString * | ID of the room to connect mic |
| targetOpenID | NSString * | The target OpenID to connect mic |
| authBuffer | NSData* | Reserved flag. You just need to enter NULL. |

#### Sample code

```
- (IBAction)shareRoom:(id)sender {
    if(_shareRoomSwitch.isOn){
        [[[ITMGContext GetInstance]GetRoom]StartRoomSharing:_shareRoomID.text targetOpenID:_shareOpenID.text authBuffer:NULL];
    }else{
        [[[ITMGContext GetInstance]GetRoom]StopRoomSharing];
    }
}
}

```

### Member status change

This API is used to obtain the user speaking in the room and display it in the UI, and to send a notification when someone entering or exiting the room.

Notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at a higher layer. The event message is `ITMG_MAIN_EVNET_TYPE_USER_UPDATE`, where the data contains `event_id` and `user_list`. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds.


| event_id | Description | Maintenance |
| ---------------------------- | :----------------------------------------------------------: | ---------------------- |
| ITMG_EVENT_ID_USER_ENTER | A member enters the room | Member list |
| ITMG_EVENT_ID_USER_EXIT | A member exits the room | Member list |
| ITMG_EVENT_ID_USER_HAS_AUDIO | A member sends audio packets. This event can be used to determine whether a user is speaking and display the voiceprint effect. It can be called together with getRecvStreamLevel. | Chat member list |
| ITMG_EVENT_ID_USER_NO_AUDIO | A member stops sending audio packets | Chat member list |

#### Room member maintenance flowchart

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

#### Sample code

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    ITMG_EVENT_ID_USER_UPDATE event_id=((NSNumber*)[data objectForKey:@"event_id"]).intValue;
    NSMutableArray* uses = [NSMutableArray arrayWithArray: [data objectForKey:@"user_list"]];
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		//Process
		//Parse the parameter to get `event_id` and `user_list`
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    // A member enters the room
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    // A member exits the room
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

#### Data details

| Message | Data | Sample |
| -------------------------------- | :-----------------: | ----------------------------- |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | event_id; user_list | {"event_id":0,"user_list":""} |


### Muting in a room

This API is used to add an ID to the audio data blocklist. This operation blocks audio from someone and only applies to the local device. A returned value of `0` indicates the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 
- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.

This API is suitable for scenarios where a user is muted in a room.

#### Function prototype  

```
ITMGContext GetAudioCtrl -(QAVResult)AddAudioBlackList:(NSString*)openID;

```

| Parameter | Type | Description |
| ------ | :------: | ----------------- |
| openId | NSString | ID to be blocked |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] AddAudioBlackList[id]];

```

### Unmuting

This API is used to remove an ID from the audio data blocklist. A returned value of `0` indicates the call is successful.

#### Function prototype  

```
-(QAVResult)RemoveAudioBlackList:(NSString*)openID;

```

| Parameter | Type | Description |
| ------ | :------: | ----------------- |
| openId | NSString | ID to be unblocked |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] RemoveAudioBlackList[openId]];

```


## Voice Chat Audio APIs

![Image](https://main.qcloudimg.com/raw/c85fe68b4b26555adf8ad01c82711f5b.png)

### Notes on voice chat audio connection

The voice chat APIs can only be called after SDK initialization and room entry.
When Enable/Disable Mic or Speaker is clicked on the UI, the following practices are recommended:
- **For most game applications, it is recommended to call the `EnableMic` and `EnableSpeaker` APIs**, which is equivalent to calling the `EnableAudioCaptureDevice/EnableAudioSend` and `EnableAudioPlayDevice/EnableAudioRecv` APIs.
- For other mobile applications (such as social networking applications), enabling/disabling a capturing device will restart both capturing and playback devices. If the application is playing back background music, it will also be interrupted. Playback will not be interrupted if the mic is enabled/disabled through control of upstreaming/downstreaming. **Calling method: call `EnableAudioCaptureDevice(true)` and `EnableAudioPlayDevice(true)` once after room entry, and call `EnableAudioSend/Recv` to send/receive audio streams when Enable/Disable Mic is clicked**.
- For more information on how to release only a capturing or playback device, please see the `EnableAudioCaptureDevice` and `EnableAudioPlayDevice`.
- Call the `pause` API to pause the audio engine and call the `resume` API to resume the audio engine.

### Voice chat audio APIs

| API | Description |
| --------------------------- | :----------------------------: |
| EnableMic | Enables/disables mic |
| GetMicState | Gets mic status |
| EnableAudioCaptureDevice | Enables/disables capturing device |
| IsAudioCaptureDeviceEnabled | Gets capturing device status |
| EnableAudioSend | Enables/disables audio upstreaming |
| IsAudioSendEnabled | Gets audio upstreaming status |
| GetMicLevel | Gets real-time mic volume |
| GetSendStreamLevel | Gets real-time audio upstreaming volume |
| SetMicVolume | Sets mic volume |
| GetMicVolume | Gets mic volume |
| EnableSpeaker | Enables/disables speaker |
| GetSpeakerState | Gets speaker status |
| EnableAudioPlayDevice | Enables/disables playback device |
| IsAudioPlayDeviceEnabled | Gets playback device status |
| EnableAudioRecv | Enables/disables audio downstreaming |
| IsAudioRecvEnabled | Gets audio downstreaming status |
| GetSpeakerLevel | Gets real-time speaker volume |
| GetRecvStreamLevel | Gets real-time downstreaming audio levels of other members in room |
| SetSpeakerVolume | Sets speaker volume |
| GetSpeakerVolume | Gets speaker volume |
| EnableLoopBack | Enables/disables in-ear monitoring |

## Voice Chat Capturing APIs

### [Enabling or disabling the microphone](id:EnableMic)

This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

**EnableMic = EnableAudioCaptureDevice + EnableAudioSend**


#### Function prototype  

```
-(QAVResult)EnableMic:(BOOL)enable;

```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | To enable the mic, set this parameter to `YES`; otherwise, set it to `NO`. |

#### Sample code  

```
// Enable mic
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];

```

### Getting the mic status

This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 is on.

#### Function prototype  

```
-(int)GetMicState;

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicState];

```

### Enabling or disabling capturing device

This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.
- This API can only be called after room entry. The device will be disabled automatically after room exit.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### Function prototype  

```
-(QAVResult)EnableAudioCaptureDevice:(BOOL)enabled;

```

| Parameter | Type | Description |
| ------- | :--: | ------------------------------------------------------------ |
| enabled | BOOL | To enable the capturing device, set this parameter to `YES`, otherwise set it to `NO`. |

#### Sample code

```
// Enable capturing device
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioCaptureDevice:enabled];

```

### Getting the capturing device status

This API is used to get the status of a capturing device.

#### Function prototype

```
-(BOOL)IsAudioCaptureDeviceEnabled;

```

#### Sample code

```
BOOL IsAudioCaptureDevice = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioCaptureDeviceEnabled];

```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### Function prototype

```
-(QAVResult)EnableAudioSend:(BOOL)enable;

```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| enable | BOOL | To enable audio upstreaming, set this parameter to `YES`; otherwise, set it to `NO`. |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioSend:enabled];

```

### Getting audio upstreaming status

This API is used to get the status of audio upstreaming.

#### Function prototype  

```
-(BOOL)IsAudioSendEnabled;

```

#### Sample code  

```
BOOL IsAudioSend = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioSendEnabled];


```

### Getting the real-time mic volume

This API is used to get the real-time mic volume. An int-type value in the range of 0-100 will be returned. It is recommended to call this API once every 20 ms.

**This API is not applicable to the voice message service.**

#### Function prototype  

```
-(int)GetMicLevel;

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicLevel];

```

### Getting the real-time audio upstreaming volume

This API is used to get the local real-time audio upstreaming volume. An int-type value in the range of 0-100 will be returned.

**This API is not applicable to the voice message service.**


#### Function prototype  

```
-(int)GetSendStreamLevel();

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSendStreamLevel];

```

### Setting mic software volume level

This API is used to set the mic volume level. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.

*This API is not applicable to the voice messaging service.*

#### Function prototype  

```
-(QAVResult)SetMicVolume:(int) volume;

```

| Parameter | Type | Description |
| ------ | :--: | ----------------------- |
| volume | int | Sets volume. Value range: 0-200 |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] SetMicVolume:100];

```

### Getting the mic software volume

This API is used to obtain the microphone volume. An "int" value is returned. Value 101 represents API SetMicVolume has not been called.
**This API is not applicable to the voice message service.**

#### Function prototype  

```
-(int) GetMicVolume;

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicVolume];

```

## Voice Chat Playback APIs

### [Enabling or disabling the speaker](id:EnableSpeaker)

This API is used to enable/disable the speaker.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

**EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### Function prototype  

```
-(void)EnableSpeaker:(BOOL)enable;

```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | To disable the speaker, set this parameter to `NO`, otherwise set it to `YES`. |

#### Sample code  

```
// Enable the speaker
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];

```

### Getting the speaker status

This API is used to get the speaker status.
- 0 indicates that the speaker is off.
- 1 indicates that the speaker is on.
- 2 indicates that the speaker is being manipulated.

#### Function prototype  

```
-(int)GetSpeakerState;

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerState];

```



### Enabling or disabling playback device

This API is used to enable/disable a playback device.

#### Function prototype  

```
-(QAVResult)EnableAudioPlayDevice:(BOOL)enabled;

```

| Parameter | Type | Description |
| ------- | :--: | ------------------------------------------------------------ |
| enabled | BOOL | To disable a playback device, set this parameter to `NO`, otherwise set it to `YES`. |

#### Sample code  

```
// Enable the playback device
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioPlayDevice:enabled];

```

### Getting the playback device status

This API is used to get the status of a playback device.

#### Function prototype

```
-(BOOL)IsAudioPlayDeviceEnabled;

```

#### Sample code  

```
BOOL IsAudioPlayDevice =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioPlayDeviceEnabled];

```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### Function prototype  

```
-(QAVResult)EnableAudioRecv:(BOOL)enabled;

```

| Parameter | Type | Description |
| ------- | :--: | ------------------------------------------------------------ |
| enabled | BOOL | To enable audio downstreaming, set this parameter to `YES`; otherwise, set it to `NO`. |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ]EnableAudioRecv:enabled];

```



### Getting audio downstreaming status

This API is used to get the status of audio downstreaming.

#### Function prototype  

```
-(BOOL)IsAudioRecvEnabled;

```

#### Sample code  

```
BOOL IsAudioRecv = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioRecvEnabled];

```

### Getting real-time speaker volume level

This API is used to get the real-time speaker volume level. An int-type value will be returned to indicate the volume level. It is recommended to call this API once every 20 ms.

#### Function prototype  

```
-(int)GetSpeakerLevel;

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerLevel];

```

### Getting the real-time downstreaming audio levels of other members in room

This API is used to get the real-time audio downstreaming volume of other members in the room. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
-(int)GetRecvStreamLevel:(NSString*) openID;

```

| Parameter | Type | Description |
| ------ | :------: | --------------------- |
| openID | NSString | `openId` of another member in the room |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetRecvStreamLevel:(NSString*) openId

```

### Setting the speaker volume

This API is used to set the speaker volume.
The corresponding parameter is volume. 0 indicates that the audio is mute, while 100 indicates that the volume remains unchanged. The default value is 100.

#### Function prototype  

```
-(QAVResult)SetSpeakerVolume:(int)vol;

```

| Parameter | Type | Description |
| ---- | :--: | ----------------------- |
| vol | int | Sets volume. Value range: 0-200 |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] SetSpeakerVolume:100];

```

### Getting the speaker volume

This API is used to get the speaker volume. An int-type value will be returned to indicate the volume. 101 indicates that the `SetSpeakerVolume` API has not been called.
"Level" indicates the real-time volume, and "Volume" the speaker volume. The final volume = `Level * Volume%`. For example, if the "Level" is 100 and "Volume" is 60, the final volume is "60".

#### Function prototype  

```
-(int)GetSpeakerVolume;

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerVolume];

```



## Advanced APIs


### Enabling in-ear monitoring

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### Function prototype  

```
-(QAVResult)EnableLoopBack:(BOOL)enable;

```

| Parameter | Type | Description |
| ------ | :-----: | ------------ |
| enable | boolean | Specifies whether to enable in-ear monitoring. |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] EnableLoopBack:YES];

```



### Modifying user's room audio type

This API is used to modify a user's room audio type. For the result, please see the callback event. The event type is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE`. The audio type of the room is determined by the first user to enter the room. After that, if a member in the room changes the room type, it will take effect for all members there.

#### Function prototype  

```
-(int)ChangeRoomType:(int)nRoomType;

```

| Parameter | Type | Description |
| --------- | :--: | ----------------------------------------------------- |
| nRoomType | int | Target room type to be switched to. For room audio types, please see the `EnterRoom` API. |

#### Sample code  

```
[[[ITMGContext GetInstance]GetRoom ]ChangeRoomType:_roomType];

```

### Getting user's room audio type

This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, please see the `EnterRoom` API.

#### Function prototype  

```
-(int)GetRoomType;

```

#### Sample code  

```
[[[ITMGContext GetInstance]GetRoom ]GetRoomType];


```

### Callback for modifying the room type

After the room type is set, the event message `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE` will be returned in the callback. The returned parameters include `result`, `error_info`, and `new_room_type`. The `new_room_type` represents the following information. The event message will be identified in the `OnEvent` function.

| Event Subtype | Parameter | Description |
| -------------------------------- | :------: | ------------------------------------------------------------ |
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM | 1 | Indicates that the existing audio type is inconsistent with and changed to that of the entered room. |
| ITMG_ROOM_CHANGE_EVENT_START | 2 | Indicates that a user is already in the room and the audio type starts changing (e.g., calling the `ChangeRoomType` API to change the audio type). |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE | 3 | Indicates that a user is already in the room and the audio type has been changed. |
| ITMG_ROOM_CHANGE_EVENT_REQUEST | 4 | Indicates that a room member calls the `ChangeRoomType` API to request a change of room audio type. |

#### Sample code  

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
	NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
 		case ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE:
			NSLog(@"ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE:%@ ",data);
            int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
            int newRoomType = ((NSNumber*) [data objectForKey:@"new_room_type"]).intValue;
            int subEventType = ((NSNumber*) [data objectForKey:@"sub_event_type"]).intValue;
	 }
}

```

#### Data details

| Message | Data | Sample |
| ------------------------------------- | :------------------------------------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | result;error_info;new_room_type;subEventType | {"error_info":"","new_room_type":0,"subEventType":0,"result":0} |



### The monitoring event of room call quality

The message for quality monitoring event triggered once every two seconds after room entry is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which represent the following information.

This API is used to monitor the network quality. If the user's network is poor, the business layer will remind the user to switch to a better network through the UI.

| Parameter | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int | Value range: 1-50. 50 indicates excellent sound quality, 1 indicates very poor (barely usable) sound quality, and 0 represents an initial meaningless value. Generally, if the value is below 30, you can remind users that the network is poor and recommend them to switch the network. |
| loss | double | Upstream packet loss rate |
| delay | int | Voice chat delay in ms |


### Getting version number

This API is used to get the SDK version number for analysis.

#### Function prototype

```
-(NSString*)GetSDKVersion;

```

#### Sample code  

```
[[ITMGContext GetInstance] GetSDKVersion];

```

### Checking mic permission

This API is used to return the mic permission status.

#### Function prototype

```
-(ITMG_RECORD_PERMISSION)CheckMicPermission;

```

#### Parameter description

| Parameter | Value | Description |
| ----------------------------- | ---- | ---------------------------- |
| ITMG_PERMISSION_GRANTED | 0 | Mic permission is granted. |
| ITMG_PERMISSION_Denied | 1 | Mic is disabled. |
| ITMG_PERMISSION_NotDetermined | 2 | No authorization box has been popped up to request the permission. |
| ITMG_PERMISSION_ERROR | 3 | An error occurred while calling the API. |

#### Sample code  

```
[[ITMGContext GetInstance] CheckMicPermission];

```



### Setting log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### Function prototype

```
-(void)SetLogLevel:(ITMG_LOG_LEVEL)levelWrite (ITMG_LOG_LEVEL)levelPrint;

```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written. `TMG_LOG_LEVEL_NONE` indicates not to write. Default value: TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed. `TMG_LOG_LEVEL_NONE` indicates not to print. Default value: TMG_LOG_LEVEL_ERROR |



| ITMG_LOG_LEVEL | Description |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE | Does not print logs |
| TMG_LOG_LEVEL_ERROR | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO | Prints info logs |
| TMG_LOG_LEVEL_DEBUG | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE | Prints verbose logs |

#### Sample code  

```
[[ITMGContext GetInstance] SetLogLevel:TMG_LOG_LEVEL_INFO TMG_LOG_LEVEL_INFO];

```



### Setting log printing path

This API is used to set the log printing path, and needs to be called before initialization. The default path is `Application/********-****-****-****-************/Documents`.

#### Function prototype

```
-(void)SetLogPath:(NSString*)logDir;

```

| Parameter | Type | Description |
| ------ | :------: | ---- |
| logDir | NSString | Path |

#### Sample code  

```
[[ITMGContext GetInstance] SetLogPath:Path];

```

### Getting diagnostic messages

This API is used to get information on the quality of real-time audio/video calls, which is mainly used to view real-time call quality and troubleshoot and can be ignored on the business side.

#### Function prototype  

```
-(NSString*)GetQualityTips;

```

#### Sample code  

```
[[[ITMGContext GetInstance]GetRoom ] GetQualityTips];

```

## Callback Messages

### Message list

| Message | Description |
| ------------- |:-------------:|
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | Indicates that a member enters an audio room. |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | Indicates that a member exits an audio room. |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | Indicates that a room is disconnected for network or other reasons. |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | Indicates a room type change event. |
| ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH | Indicates that the accompaniment is over. |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | Indicates that the room members are updated. |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_USERS_UPDATE | Indicates that the room member quantity is updated. |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_AUDIOSTREAMS_UPDATE | Indicates that the room audio stream quantity is updated. |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY | Indicates the room quality information. |


### Data list

| Message | Data | Sample |
| -------------------------------------------------- | :-----------------------------------------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | result; error_info | {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | result; error_info | {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | result; error_info; sub_event_type; new_room_type | {"error_info":"","new_room_type":0,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE | result; error_info | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE | result; error_info | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE | result; error_info | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE | result; error_info | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | user_list;  event_id | {"event_id":1,"user_list":["0"]} |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_USERS_UPDATE | AllUser; AccUser; ProxyUser | {"AllUser":3,"AccUser":2,"ProxyUser":1} |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_AUDIOSTREAMS_UPDATE | AudioStreams | {"AudioStreams":3} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY | weight; loss; delay | {"weight":5,"loss":0.1,"delay":1} |


