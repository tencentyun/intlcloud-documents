This document describes how to access and debug GME client APIs for the voice chat feature for iOS.

## Key Considerations for Using GME

GME provides the real-time voice, voice message, and speech-to-text conversion services, which all depend on core APIs such as `Init` and `Poll`.

#### Key notes

- You have created a GME application and obtained the `AppID` and `Key` of the SDK as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- You have **activated the real-time voice, voice message, and speech-to-text services of GME** as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error code, please see <dx-tag-link link="https://cloud.tencent.com/document/product/607/15173" tag="ErrorCode">Error Codes</dx-tag-link>.

## Connecting to the SDK

### Directions

Key processes involved in SDK connection are as follows:

<img src="https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg"  width="70%" /></img>

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Entering a voice chat room</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Enabling the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Enabling the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exiting a voice room</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitializing GME</dx-tag-link>
</dx-steps>



### APIs

```
@class ITMGRoom;//Room APIs
@class ITMGAudioCtrl;//Audio APIs
@class ITMGAudioEffectCtrl;//Sound effect and accompaniment APIs
```

## Key APIs

| API | Description |
| ------ | :----------: |
| InitEngine | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |
|SetDefaultAudienceAudioCategory| Sets the audio of the iOS device |


<dx-alert infotype="notice" title="">
If you need to switch the account, call `UnInit` to uninitialize the SDK. No fees are incurred for calling the `InitEngine` API.
</dx-alert>

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

#### API prototype

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


**You need to initialize the SDK through the `InitEngine` API** before you can use the real-time voice, voice message, and speech-to-text services. **After the SDK is started, it will collect the user's personal information.** The `InitEngine` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

<dx-alert infotype="notice" title="Note">
After making sure that the user has read and consented to the application's privacy policy, call the `InitEngine` function to initialize the SDK at an appropriate time based on the application features. If the user does not consent to the privacy policy, the `InitEngine` function cannot be called.
</dx-alert>


#### API prototype

```
-(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID;
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0). |
| OpenId   | String | `openID` can only be in `Int64` type, which is passed in after being converted to a `const char*`. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application.         |

#### Returned values
| Returned Value | Description |
| --------------------------------- | --------------------------------------------- |
| QAV_OK= 0 | Initialized SDK successfully. |
| QAV_ERR_SDK_NOT_FULL_UPDATE= 7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

<dx-alert infotype="notice" title="Notes on 7015 error code">

- The 7015 error code is judged by md5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.
- Due to the third-party reinforcement, Unity packaging mechanism and other factors, the md5 of the library file will be affected, resulting in misjudgment. **Please ignore this error in the logic for official release**, and try to avoid displaying it in the UI.
  </dx-alert>

#### Sample code 


```
_openId = _userIdText.text;
_appId = _appIdText.text;
int result = 0;
// After the user consents to the application's privacy policy, initialize the SDK at an appropriate time based on the application features
//result = 0: The user consents to the application's privacy policy
//result = 1: The user does not consent to the application's privacy policy
// If the user does not consent to the privacy policy, change `ret` to a value other than 0 
if (result == 0) {
	[[ITMGContext GetInstance] InitEngine:SDKAPPID openID:_openId];}
	else{
	log = [NSString stringWithFormat:@"The user does not consent to the application's privacy policy"];
}
```


### [Triggering event callback](id:Poll)

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. `Poll` is the message pump of GME, and the `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
Refer to the EnginePollHelper.java file in [Demo](https://intl.cloud.tencent.com/document/product/607/18521).

<dx-alert infotype="alarm" title="Calling the `Poll` API periodically">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>

#### API prototype

```
-(void)Poll;

```

#### Sample code

```
[[ITMGContext GetInstance] Poll];

```

### Pausing the system

When a `Pause` event occurs in the system, the engine should also be notified for pause. If you do not need the background to play back the audio in the room, please call `Pause` API to pause the GME service.

#### API prototype

```
-(QAVResult)Pause;

```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### API prototype

```
-(QAVResult)Resume;

```

### [Uninitializing SDK](id:UnInit)

This API is used to uninitialize the SDK to make it uninitialized. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**


<dx-alert infotype="notice" title="Note">
If the end user revokes the permission granted to the SDK to process the personal information, you can call the `Uninit` API to stop using the SDK features and stop collecting and close the user data used by the features.
</dx-alert>

#### API prototype

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

![](https://qcloudimg.tencent-cloud.cn/raw/6d22d6345c15fae25591ecd273872c9d.png)

<dx-alert infotype="notice" title="">
It is recommended that developers call this API to set the audio.
</dx-alert>



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



## Voice Chat Room APIs

You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, please see [FAQs About Voice Chat](https://intl.cloud.tencent.com/document/product/607/39524).

![](https://qcloudimg.tencent-cloud.cn/raw/02f98895d0b7bfe1bac774d5983289c1.jpg)

| API | Description |
| ------------- | :------------------: |
| GenAuthBuffer |     Calculates the local authentication key     |
| EnterRoom     |       Enters a room       |
| ExitRoom      |       Exits the room       |
| IsRoomEntered | Determines whether room entry is successful |
| SwitchRoom    |     Switches the room quickly     |
|StartRoomSharing | Starts cross-room co-anchoring |

### Local authentication key calculation

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### API prototype

```
@interface QAVAuthBuffer : NSObject
+ (NSData*) GenAuthBuffer:(unsigned int)appId roomId:(NSString*)roomId openID:(NSString*)openID key:(NSString*)key;
+ @end

```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId | int | `AppId` from the Tencent Cloud console.|
| roomId | NSString | Room ID, which can contain up to 127 characters. |
| openID | NSString | User ID, which is the same as `openID` during initialization. |
| key | NSString | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |



#### Sample code  

```
#import "GMESDK/QAVAuthBuffer.h"
NSData* authBuffer = [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomId:_roomId openID:_openId key:AUTHKEY];

```

[](id:EnterRoom)
### Entering a room

This API is used to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry.

<dx-alert infotype="notice" title="Note">
- If the room entry callback result is `0`, the room entry is successful. If `0` is returned from the `EnterRoom` API, it doesn't necessarily mean that the room entry is successful.
- The audio type of the room is determined by the first user entering the room. After that, if a member in the room changes the room type, it will take effect for all members there. For example, if the first user entering the room uses the smooth sound quality, and the second user entering the room uses the HD sound quality, the room audio type of the second user will change to the smooth sound quality. Only after a member in the room calls the `ChangeRoomType` API will the audio type of the room be changed.
</dx-alert>

#### Function prototype

```
-(int)EnterRoom:(NSString*) roomId roomType:(int)roomType authBuffer:(NSData*)authBuffer;
```

| Parameter | Type | Description |
| ---------- | :------: | ----------------------- |
| roomId | NSString | Room ID, which can contain up to 127 characters |
| roomType   |  int   | Room type. We recommend you enter `ITMG_ROOM_TYPE_FLUENCY`. For more information on room audio types, see [Sound Quality](https://intl.cloud.tencent.com/document/product/607/18522).      |
| authBuffer | NSData | Authentication key |




#### Sample code  

```
[[ITMGContext GetInstance] EnterRoom:_roomId roomType:_roomType authBuffer:authBuffer];

```

#### Callback for room entry

After the user enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function for callback and processing. A successful callback means that the room entry is successful, and the billing starts.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will Voice Chat still be charged when client is offlined?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
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
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT                   |                result; error_info                 | {"error_info":"waiting timeout, please check your network","result":0} |

If the network is disconnected, there will be a disconnected callback prompt `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. At this time, the SDK will automatically reconnect, and the callback is `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.

#### Error codes

| Error Code Value | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006 | Authentication failed <li>The `AppID` does not exist or is incorrect.<li>An error occurred while authenticating the `authbuff`.<li>Authentication expired.<li>The `OpenId` does not meet the specification. |
| 7007 | Already in another room. |
| 1001 | The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
| 1003 | The user was already in the room and called the room entering API again. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |


[](id:ExitRoom)	
### Exiting a room

This API is used to exit the current room. It is an async API. The returned value `AV_OK` indicates a successful async delivery. If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API; instead, you can directly call the `EnterRoom` API.

#### API prototype  

```
-(int)ExitRoom

```

#### Sample code  

```
[[ITMGContext GetInstance] ExitRoom];

```

#### Callback for room exit

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

This API is used to determine whether the user has entered a room. A value in bool type will be returned. Do not call this API during room entry.

#### API prototype  

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

Call this API to connect the microphones across rooms after the room entry. After the call, the local user can communicate with the target OpenID user in the target room. The target room should be of the same type as the local room.

#### Example
User a is in room A, user b is in room B, and user a can talk with b through the cross-room API. When user c in room A speaks, users b and d in room B cannot hear. User c in room A can hear only the voice in room A and the voice of user b in room B but not other users in room B.

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
```

## Room Status Maintenance

APIs in this section are used to display speaking members and members entering or exiting the room and mute a member in the room at the business layer.

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

| API/Notification | Description |
| -------------------------------- | :--------------: |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | The member status changed |
| AddAudioBlackList                | Mutes a member in the room |
| RemoveAudioBlackList             |     Unmutes a user     |

### Notifications of member room entry and speaking status


This API is used to obtain the user speaking in the room and display it in the UI, and to send a notification when someone entering or exiting the room.
Notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at a higher layer. The event message is `ITMG_MAIN_EVNET_TYPE_USER_UPDATE`, where the data contains `event_id` and `user_list`. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds.

| event_id | Description | Maintenance |
| ---------------------------- | :----------------------------------------------------------: | ---------------------- |
| ITMG_EVENT_ID_USER_ENTER     |                     Return the `openid` of the member entering the room.                       | Member list     |
| ITMG_EVENT_ID_USER_EXIT      |                 Return the `openid` of the member exiting the room.           | Member list     |
| ITMG_EVENT_ID_USER_HAS_AUDIO | Return the `openid` of the member sending audio packets in the room. This event can be used to determine whether a user is speaking and display the voiceprint effect.  | Chat member list |
| ITMG_EVENT_ID_USER_NO_AUDIO  |                     Return the `openid` of the member stopping sending audio packets in the room.                     | Chat member list |

#### Sample code

```
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
    ITMG_EVENT_ID_USER_UPDATE event_id=((NSNumber*)[data objectForKey:@"event_id"]).intValue;
    NSMutableArray* uses = [NSMutableArray arrayWithArray: [data objectForKey:@"user_list"]];
    NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		// Process
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

#### Data details

| Message | Data | Sample |
| -------------------------------- | :-----------------: | ----------------------------- |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | event_id; user_list | {"event_id":0,"user_list":""} |


### Muting a member in the room

This API is used to add an ID to the audio data blocklist. This operation blocks audio from someone and only applies to the local device without affecting other devices. The returned value `0` indicates that the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 

- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.

This API is suitable for scenarios where a user is muted in a room.

#### API prototype  

```
ITMGContext GetAudioCtrl -(QAVResult)AddAudioBlackList:(NSString*)openID;

```

| Parameter | Type | Description |
| ------ | :----: | ----------------- |
| openId | NSString | ID to be blocked openid  |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] AddAudioBlackList[id]];

```

### Unmuting

This API is used to remove an ID from the audio data blacklist. A returned value of 0 indicates the call is successful.

#### API prototype  

```
-(QAVResult)RemoveAudioBlackList:(NSString*)openID;

```

| Parameter | Type | Description |
| ------ | :----: | ----------------- |
| openId | NSString | ID to be unblocked openid  |

#### Sample code  

```
[[[ITMGContext GetInstance]GetAudioCtrl ] RemoveAudioBlackList[openId]];

```



## Voice Chat Capturing APIs

- The voice chat APIs can only be called after SDK initialization and room entry.
- When the user clicks the button of enabling/disabling the mic or speaker on the UI, we recommend you call the `EnableMic` or `EnableSpeaker` API.
- When the user enters a voice chat room, enabling/disabling a capturing device will restart both capturing and playback devices. If the application is playing back background music, it will also be interrupted. Playback won't be interrupted if the mic is enabled/disabled through control of upstreaming/downstreaming. **Calling method: Call `EnableAudioCaptureDevice(true)` and `EnableAudioPlayDevice(true)` once after room entry, and call `EnableAudioSend/Recv` to send/receive audio streams when Enable/Disable Mic is clicked.**


| API | Description |
| --------------------------- | :------------------: |
| EnableMic                   |      Enables/Disables the mic      |
| GetMicState                 |    Gets the mic status    |
| EnableAudioCaptureDevice    |     Enables/Disables the capturing device     |
| IsAudioCaptureDeviceEnabled |   Gets the capturing device status   |
| EnableAudioSend             |   Enables/Disables audio upstreaming   |
| IsAudioSendEnabled          |   Gets the audio upstreaming status   |
| GetMicLevel                 |  Gets the real-time mic volume level  |
| GetSendStreamLevel | Gets real-time audio upstreaming volume |
| SetMicVolume                |    Sets the mic volume level    |
| GetMicVolume                |    Gets the mic volume level    |


[](id:EnableMic)	
### Enabling or disabling mic

This API is used to enable/disable the mic. The mic and speaker are not enabled by default after room entry. **EnableMic = EnableAudioCaptureDevice + EnableAudioSend**
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

#### API prototype  

```
-(QAVResult)EnableMic:(BOOL)enable;

```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| enable | boolean | <li>To enable the mic, set this parameter to `YES`.<li>To disable the mic, set this parameter to `NO`. |

#### Sample code  

```
// Enable mic
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];

```

### Getting the mic status

This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 is on.

#### API prototype  

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

#### API prototype  

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

#### API prototype

```
-(BOOL)IsAudioCaptureDeviceEnabled;

```

#### Sample code

```
BOOL IsAudioCaptureDevice = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioCaptureDeviceEnabled];

```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### API prototype

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

#### API prototype  

```
-(BOOL)IsAudioSendEnabled;

```

#### Sample code  

```
BOOL IsAudioSend = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioSendEnabled];


```

### Getting the real-time mic volume

This API is used to get the real-time mic volume. An int-type value in the range of 0-100 will be returned. It is recommended to call this API once every 20 ms.

 

#### API prototype  

```
-(int)GetMicLevel;

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicLevel];

```

### Getting the real-time audio upstreaming volume

This API is used to get the local real-time audio upstreaming volume. An int-type value in the range of 0-100 will be returned.

 

#### API prototype  

```
-(int)GetSendStreamLevel();

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSendStreamLevel];

```

### Setting the mic software volume

This API is used to set the mic volume level. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound.

 

#### API prototype  

```
-(QAVResult)SetMicVolume:(int) volume;

```

| Parameter | Type | Description |
| ------ | :--: | ----------------------- |
| volume | int  | Value range: 0–200. Default value: `100`. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged. |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] SetMicVolume:100];

```

### Getting the mic software volume

This API is used to obtain the microphone volume. An "int" value is returned. Value 101 represents API SetMicVolume has not been called.

 

#### API prototype  

```
-(int) GetMicVolume;

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetMicVolume];

```

## Voice Chat Playback APIs

| API | Description |
| ------------------------ | :----------------------------: |
| EnableSpeaker            |           Enables/Disables the speaker           |
| GetSpeakerState          |         Gets the speaker status         |
| EnableAudioPlayDevice    |          Enables/Disables the playback device          |
| IsAudioPlayDeviceEnabled | Gets playback device status |
| EnableAudioRecv          |        Enables/Disables audio downstreaming        |
| IsAudioRecvEnabled       |        Gets the audio downstreaming status        |
| GetSpeakerLevel          |       Gets the real-time speaker volume level       |
| GetRecvStreamLevel       | Gets the real-time downstreaming audio volume levels of other members in the room |
| SetSpeakerVolume         |         Sets the speaker volume level         |
| GetSpeakerVolume         |         Gets the speaker volume level         |

### [Enabling or disabling the speaker](id:EnableSpeaker)

This API is used to enable/disable the speaker. **EnableSpeaker = EnableAudioPlayDevice + EnableAudioRecv**
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

#### API prototype  

```
-(void)EnableSpeaker:(BOOL)enable;

```

| Parameter    | Type   | Description                                                                                                                    |
| --------- | :-----: | ------------------------------------------------------------ |
| enable | boolean | <li>To disable the speaker, set this parameter to `NO`.<li>To enable the speaker, set this parameter to `YES`. |

#### Sample code  

```
// Enable the speaker
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];

```

### Getting the speaker status

This API is used to get the speaker status. 0 indicates that the speaker is off, and 1 is on.

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

#### API prototype  

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

#### API prototype

```
-(BOOL)IsAudioPlayDeviceEnabled;

```

#### Sample code  

```
BOOL IsAudioPlayDevice =  [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioPlayDeviceEnabled];

```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### API prototype  

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

#### API prototype  

```
-(BOOL)IsAudioRecvEnabled;

```

#### Sample code  

```
BOOL IsAudioRecv = [[[ITMGContext GetInstance] GetAudioCtrl] IsAudioRecvEnabled];

```

### Getting the real-time speaker volume

This API is used to get the real-time speaker volume. An int-type value will be returned to indicate the volume. It is recommended to call this API once every 20 ms.

#### API prototype  

```
-(int)GetSpeakerLevel;

```

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetSpeakerLevel];

```

### Getting the real-time downstreaming audio levels of other members in room

This API is used to get the real-time audio downstreaming volume of other members in the room. An int-type value will be returned. Value range: 0-200.

#### API prototype  

```
-(int)GetRecvStreamLevel:(NSString*) openID;
```

| Parameter | Type | Description |
| ------ | :----: | -------------------- |
| openID | NSString | `openId` of another member in the room |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] GetRecvStreamLevel:(NSString*) openId];
```

### Dynamically setting the volume of a member of the room

This API is used to set the volume of a member in the room. It takes effect only on the local.

#### API prototype  

```
-(int) SetSpeakerVolumeByOpenID:(NSString *)openId volume:(int)volume;
```

| Parameter | Type | Description |
|----------|-------|-------|
|openId       |String *   |OpenID needs to set volume|
|volume  |int        |Percentage. It is recommended to set between [0-200], where 100 is by default||



### Getting volume percentage

Call this API to get the volume set by SetSpeakerVolumeByOpenID

#### API prototype

```
-(int) GetSpeakerVolumeByOpenID:(NSString *)openId;
```

#### Returned values

API returns volume percentage set by OpenID, where 100 is by default.

### Setting the speaker volume

This API is used to set the speaker volume.
The corresponding parameter is volume. 0 indicates that the audio is mute, while 100 indicates that the volume remains unchanged. The default value is 100.

#### Function prototype  

```
-(QAVResult)SetSpeakerVolume:(int)vol;

```

| Parameter             |        Type        | Description                 |
| ---- | :--: | ----------------------- |
| vol | int | Sets volume. Value range: 0-200 |

#### Sample code  

```
[[[ITMGContext GetInstance] GetAudioCtrl] SetSpeakerVolume:100];

```

### Getting the speaker volume

This API is used to get the speaker volume. An int-type value will be returned to indicate the volume. 101 indicates that the `SetSpeakerVolume` API has not been called.
"Level" indicates the real-time volume, and "Volume" the speaker volume. The final volume = Level * Volume%. For example, if the "Level" is 100 and "Volume" is 60, the final volume is "60".

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

| Parameter    | Type   | Description                                                                                                                    |
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
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
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



### Setting the log printing path

This API is used to set the log printing path, and needs to be called before initialization. The default path is `Application/********-****-****-****-************/Documents`.

#### Function prototype

```
-(void)SetLogPath:(NSString*)logDir;

```

| Parameter   |   Type   | Description                  |
| ------ | :------: | ---- |
| logDir | NSString | Path |

#### Sample code  

```
[[ITMGContext GetInstance] SetLogPath:Path];

```

### Getting the diagnostic messages

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
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | Indicates that the room members are updated. |
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
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_AUDIOSTREAMS_UPDATE     |                   AudioStreams                    | {"AudioStreams":3}                                           |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY | weight; loss; delay | {"weight":5,"loss":0.1,"delay":1} |
