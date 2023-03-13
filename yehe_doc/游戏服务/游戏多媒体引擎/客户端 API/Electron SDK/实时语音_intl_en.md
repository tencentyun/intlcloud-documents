
This document describes how to integrate with and debug GME client APIs for the voice chat feature for Electron.

## Key Considerations for Using GME

GME provides the real-time voice service and voice messaging and speech-to-text services, which all depend on core APIs such as `Init` and `Poll`.

#### Notes

- You have created a GME application and obtained the SDK `AppID` and key. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- You have activated **GME real-time voice service and voice messaging and speech-to-text services**. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).
- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `GmeError.AV_OK` will be returned with the value being `0`.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error codes, see <dx-tag-link link="https://www.tencentcloud.com/document/product/607/33223" tag="ErrorCode">Error Codes</dx-tag-link>.

## Integrating the SDK

### Directions

Key processes involved in SDK integration are as follows:

<img src="https://qcloudimg.tencent-cloud.cn/raw/c8758a24fe68fc084b8d12b09de5e27a.jpg"  width="70%" /></img>

<dx-steps>
-<dx-tag-link link="#Init" tag="API: Init">Initializing GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="API: Poll">Calling Poll periodically to trigger event callbacks</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="API: EnterRoom">Entering a voice chat room</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="API: EnableMic">Enabling the microphone</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="API: EnableSpeaker">Enabling the speaker</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="API: ExitRoom">Exiting a voice chat room</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="API: UnInit">Uninitializing GME</dx-tag-link>
</dx-steps>

## Core APIs

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |

### Importing the GME module
```
const { GmeContext } = require('gme-electron-sdk');
```

### Getting an instance

To use the voice chat feature, get the `GmeSDK` object first.

```
context = new GmeContext();
```

[](id:Init)
### Initializing the SDK

**You need to initialize the SDK through the `Init` API** before you can use the real-time voice, voice message, and speech-to-text services. The `Init` API must be called in the same thread as other APIs. We recommend you call all APIs in the main thread.

#### API prototype

```
//class GmeSDK
Init(appid: string, openid: string): number;
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | `AppID` provided in the [GME console](https://console.cloud.tencent.com/gamegme), which can be obtained as instructed in [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0). |
| openID   | string | `openID` can only be in `int64` type, which is passed in after being converted to a string. You can customize its rules, and it must be unique in the application. To pass in `openID` as a string, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=438&level2_id=445&source=0&data_title=%E6%B8%B8%E6%88%8F%E5%A4%9A%E5%AA%92%E4%BD%93%E5%BC%95%E6%93%8EGME&step=1) for application. |

#### Returned values

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| GmeError.AV_OK= 0                  | Initialized the SDK successfully. |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

<dx-alert infotype="notice" title="Notes on 7015 error code">

- The 7015 error code is judged by MD5. If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is **only a reminder** but will not cause an initialization failure.
- Due to the third-party reinforcement, Unity packaging mechanism and other factors, the MD5 of the library file will be affected, resulting in misjudgment. **Please ignore this error in the logic for official release**, and try to avoid displaying it in the UI.
  </dx-alert>

#### Sample code 

```
string SDKAPPID3RD = "14000xxxxx";
string openId="10001";
number ret = context.Init(SDKAPPID3RD, openId);
// Determine whether the initialization is successful by the returned value
if (ret != GmeError.AV_OK)
{
		console.log("Failed to initialize the SDK:");
		return;
}
```


### Setting callbacks

The API class uses the `Delegate` method to send callback notifications to the application. Register the callback function to the SDK for receiving callback messages before room entry.

#### Function prototype and sample code

Register the callback function to the SDK for receiving callback messages before room entry.
```
SetTMGDelegate(cb: ITMGDelegate);
// When initializing the SDK
context =  GmeSDK.GetInstance();
context.setTMGDelegate(function(eventId, msg){
  if (type == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
  {
            // Processing callbacks
  }
});
```

[](id:Poll)
### Triggering event callback

You need to periodically call the `Poll` API to trigger event callbacks. The `Poll` API is GME's message pump and should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run abnormally. For more information, see the `EnginePollHelper` file in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).

<dx-alert infotype="alarm" title="Calling the `Poll` API periodically">
The `Poll` API must be called periodically and in the main thread to avoid abnormal API callbacks.
</dx-alert>

#### API prototype

```
Poll():number;
```

#### Sample code

```
setInterval(function () {
      context.Poll();
    }, 50);
```

### Pausing the system

When a `Pause` event occurs in the system, the engine should also be notified for pause. For example, when the application switches to the background (OnApplicationPause, isPause=True), and you do not need the background to play back the audio in the room, please call `Pause` API to pause the GME service.

#### API prototype

```
Pause() :number
```

### Resuming the system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### API prototype

```
Resume() :number
```


[](id:UnInit)
### Uninitializing SDK

This API is used to uninitialize the SDK to make it uninitialized. **If the game business account is bound to `openid`, switching game account requires uninitializing GME and then using the new `openid` to initialize again.**

#### API prototype

```
Uninit() : number;
```

## Voice Chat Room APIs

You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, see [Sound and Audio](https://intl.cloud.tencent.com/document/product/607/39524).

![](https://qcloudimg.tencent-cloud.cn/raw/02f98895d0b7bfe1bac774d5983289c1.jpg)

| API | Description |
| ------------- | :------------------: |
| GenAuthBuffer |     Calculates the local authentication key     |
| EnterRoom     |       Enters a room       |
| ExitRoom      |       Exits a room       |
| IsRoomEntered | Determines whether room entry is successful |

### Local authentication key calculation

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    

#### API prototype

```
GenAuthBuffer(appId: string,roomId: string, openId:string, appKey: number) :string;
```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  string   | `AppID` from the Tencent Cloud console. |
| roomId | string | Room ID, which can contain up to 127 characters. |
| openId | string | User ID, which is the same as `openID` during initialization.                       |
| key    | number | Permission key from the Tencent Cloud [console](https://console.cloud.tencent.com/gamegme). |

#### Sample code  

```
 let userSig = context.GenAuthBuffer(this.appid, this.roomId, this.userId, this.authKey)
 context.EnterRoom(this.roomId, this.roomType, userSig);
```

[](id:EnterRoom)
### Entering a room

This API is used to enter a room with the generated authentication information. The mic and speaker are not enabled by default after room entry.

<dx-alert infotype="alarm" title="Notes">
- If the room entry callback result is `0`, the room entry is successful. If `0` is returned from the `EnterRoom` API, it doesn't necessarily mean that the room entry is successful.
- The audio type of the room is determined by the first user entering the room. After that, if a member in the room changes the room type, it will take effect for all members there. For example, if the first user entering the room uses the smooth sound quality, and the second user entering the room uses the HD sound quality, the room audio type of the second user will change to the smooth sound quality. Only after a member in the room calls the `ChangeRoomType` API will the audio type of the room be changed.
</dx-alert>

#### API prototype

```
EnterRoom(roomid: string, roomType: number, appKey: string) :number;
```

| Parameter | Type | Description |
| ---------- | :----------: | ------------------------------------------ |
| roomId     |    string    | Room ID, which can contain up to 127 characters.                    |
| roomType   | ITMGRoomType | Room type. We recommend you select `ITMG_ROOM_TYPE_FLUENCY` for games. For more information on room audio types, see [Sound Quality](https://intl.cloud.tencent.com/document/product/607/18522). |
| appKey |    string    | Authentication key                                     |

#### Sample code  

```
context.EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, retAuthBuff);
```

### Callback for room entry

After the user enters the room, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` event type will be called back to notify the room entry result, which can be listened on for processing. A successful callback means that the room entry is successful, and the billing **starts**.

<dx-fold-block title="Billing references">
[Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009)
[Billing FAQs](https://intl.cloud.tencent.com/document/product/607/30255)
[Will Voice Chat still be charged when client gets offline?](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

#### Sample code  

```
// Listen on an event:
 gmeContext.setTMGDelegate(function(eventId, msg){
  switch (eventId) {
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
      {
      }
  }
});
```

#### Data details

| Message | Data | Sample |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0}                                 |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |

If the network is disconnected, there will be a disconnection callback notification `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`. At this time, the SDK will automatically reconnect, and the callback is `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`. When the reconnection is successful, there will be a callback `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS`.

#### Error codes

| Error Code Value | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006     | Authentication failed. Possible causes: <li>The `AppID` does not exist or is incorrect.<li>An error occurred while authenticating the `authbuff`.<li>Authentication expired.<li>The `OpenId` does not meet the specification. |
| 7007 | Already in another room. |
| 1001 | The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
| 1003 | The user was already in the room and called the room entering API again. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |

[](id:ExitRoom)	
### Exiting a room

This API is used to exit the current room. It is an async API. The returned value `AV_OK` indicates a successful async delivery. If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API; instead, you can directly call the `EnterRoom` API.

#### API prototype  

```
ExitRoom(): number;
```

#### Sample code  

```
context.ExitRoom();
```

#### Callback for room exit

After the user exits a room, a callback will be returned with the message being `ITMG_MAIN_EVENT_TYPE_EXIT_ROOM`. The sample code is shown below:

#### Sample code  

```
gmeContext.setTMGDelegate(function(eventId, msg){
  switch (eventId) {
      case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
      {
			 // Process
        break;
      }
  }
});
```

### Determining whether user has entered room

This API is used to determine whether the user has entered a room. A value in boolean type will be returned. Do not call this API during room entry.

#### API prototype  

```
IsRoomEntered() :boolean
```

#### Sample code  

```
context.IsRoomEntered();
```

## Room Status Maintenance

APIs in this section are used to display speaking members and members entering or exiting the room and mute a member in the room at the business layer.

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

| API/Notification | Description |
| -------------------------------- | :--------------: |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | The member status changed |
| AddAudioBlackList                | Mutes a member in the room |
| RemoveAudioBlackList             |     Unmutes a user     |
| IsOpenIdInAudioBlackList             |    Queries whether the user of the specified `openid` is muted     |

### Notification events of member room entry and speaking status

- This event is used to get the user speaking in the room and display the user on the UI, and to send a notification when someone enters or exits the room.
- A notification for this event will be sent only when the status changes. To get the member status in real time, cache the notification when it is received at the business layer. The event message `ITMG_MAIN_EVNET_TYPE_USER_UPDATE` containing `event_id`, `count`, and `openIdList` will be returned, which will be identified in the `OnEvent` notification.
- Notifications of the `EVENT_ID_ENDPOINT_NO_AUDIO` audio event will be sent only when the threshold is exceeded, that is, other members in the room can receive the notification that the local user stops speaking only after the local client captures no voice for two seconds.
- The audio event returns only the member speaking status but not the specific volume level. If you need the specific volume levels of members in the room, you can use the `GetVolumeById` API.

| event_id                     |         Description         | Maintenance         |
| --------------------------- | :---------------------------------------------------: | ---------------------- |
| EVENT_ID_ENDPOINT_ENTER     |         Return the `openid` of the member entering the room.         | Member list     |
| EVENT_ID_ENDPOINT_EXIT      |         Return the `openid` of the member exiting the room.         | Member list     |
| EVENT_ID_ENDPOINT_HAS_AUDIO |     Return the `openid` of the member sending audio packets in the room. This event can be used to determine whether a user is speaking and display the voiceprint effect.     | Chat member list |
| EVENT_ID_ENDPOINT_NO_AUDIO  | Return the `openid` of the member stopping sending audio packets in the room. | Chat member list |

#### Sample code

```
context.setTMGDelegate(function(eventId, msg){
  if (type == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
  {
           	// Process
		    switch (eventID)
 		    {
 		    case EVENT_ID_ENDPOINT_ENTER:
  			    // A member enters the room
  			    break;
 		    case EVENT_ID_ENDPOINT_EXIT:
  			    // A member exits the room
			    break;
		    case EVENT_ID_ENDPOINT_HAS_AUDIO:
			    // A member sends audio packets
			    break;
		    case EVENT_ID_ENDPOINT_NO_AUDIO:
			    // A member stops sending audio packets
			    break;
		  
		    default:
			    break;
 		    }
		break;
  }
});
```

### Muting a member in the room

This API is used to add an ID to the audio data blocklist. This operation blocks audio from someone and only applies to the local device without affecting other devices. The returned value `0` indicates that the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 

- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.

This API is suitable for scenarios where a user is muted in a room.

#### API prototype  

```
AddAudioBlackList(openId: string) :number
```

| Parameter | Type | Description |
| ------ | :---: | ------------------ |
| openId | string | `openid` of the user to be blocked |

#### Sample code  

```
context.AddAudioBlackList(openId);
```

### Unmuting

This API is used to remove an ID from the audio data blacklist. A returned value of 0 indicates the call is successful.

#### API prototype  

```
RemoveAudioBlackList(openId: string) :number
```

| Parameter | Type | Description |
| ------ | :---: | ----------------- |
| openId |string | ID to be unblocked |

#### Sample code  

```
context.RemoveAudioBlackList(openId);
```

### Querying whether a user is muted

This API is used to query whether an ID is blocked. The returned value `true` indicates that the ID is blocked, while `false` indicates not.

#### API prototype  

```
IsOpenIdInAudioBlackList(openId: string) :boolean
```

| Parameter | Type | Description |
| ------ | :---: | ----------------- |
| openId |string | ID to be queried |

#### Sample code  

```
boolean isInBlackList = context.IsOpenIdInAudioBlackList(openId);
```

## Voice Chat Capturing APIs

- The voice chat APIs can only be called after SDK initialization and room entry.
- When the user clicks the button of enabling/disabling the mic or speaker on the UI, we recommend you call the `EnableMic` or `EnableSpeaker` API.
- To enable the user to press the mic button on the UI to speak and release it to stop speaking, we recommend you call `EnableAudioCaptureDevice` once during room entry and call `EnableAudioSend` to enable the user to speak while pressing the button.

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

#### API prototype  

```
EnableMic(bEnable: boolean) : number
```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | To enable the mic, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
// Turn on mic
context.EnableMic(true);
```

### Getting the mic status

This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 is on.

#### API prototype  

```
GetMicState() :number
```

#### Sample code  

```
context.GetMicState();
```

### Enabling or disabling capturing device

This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.

- This API can only be called after room entry. The device will be disabled automatically after room exit.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### API prototype  

```
EnableAudioCaptureDevice(enable:boolean) :number
```

| Parameter | Type | Description |
| --------- | :--: | ------------------------------------------------------------ |
| enable | boolean | To enable a capturing device, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code

```
// Enable capturing device
context.EnableAudioCaptureDevice(true);
```

### Getting the capturing device status

This API is used to get the status of a capturing device.

#### API prototype

```
IsAudioCaptureDeviceEnabled():boolean
```

#### Sample code

```
boolean IsAudioCaptureDevice = context.IsAudioCaptureDeviceEnabled();
```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, see the `EnableAudioCaptureDevice` API.

#### API prototype

```
EnableAudioSend(bEnable: boolean) :number
```

| Parameter | Type | Description |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled |boolean | To enable audio upstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
context.EnableAudioSend(true);
```

### Getting audio upstreaming status

This API is used to get the status of audio upstreaming.

#### API prototype  

```
IsAudioSendEnabled():boolean
```

#### Sample code  

```
boolean IsAudioSend = context.IsAudioSendEnabled();
```

### Getting the real-time mic volume

This API is used to get the real-time mic volume level. A number-type value in the range of 0–100 will be returned. We recommend you call this API once every 20 ms.

 

#### API prototype  

```
GetMicLevel():number
```

#### Sample code  

```
context.GetMicLevel();
```

 ### Getting the real-time audio upstreaming volume

This API is used to get the local real-time audio upstreaming volume level. A number-type value in the range of 0-100 will be returned.

#### API prototype  

```
GetSendStreamLevel() :number
```

#### Sample code  

```
context.GetSendStreamLevel();
```

### Setting the mic software volume

This API is used to set the mic volume level. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound.
#### API prototype  

```
SetMicVolume(volume:number) :number
```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| volume | number  | Value range: 0-200. Default value: `100`. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged. |

#### Sample code  

```
number micVol = (value * 100);
context.SetMicVolume (micVol);
```

### Getting the mic software volume

This API is used to get the mic volume level. A number-type value will be returned. `101` indicates that the `SetMicVolume` API has not been called.

 

#### API prototype  

```
GetMicVolume()
```

#### Sample code  

```
context.GetMicVolume();
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
| GetSpeakerLevel          |       Gets the real-time speaker volume level        |
| GetRecvStreamLevel       | Gets the real-time downstreaming audio volume levels of other members in the room |
| SetSpeakerVolume         |         Sets the speaker volume level         |
| GetSpeakerVolume         |         Gets the speaker volume level         |


[](id:EnableSpeaker)	
### Enabling or disabling speaker

This API is used to enable/disable the speaker. **EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### API prototype  

```
EnableSpeaker(bEnable: boolean) : number;
```

| Parameter | Type | Description |
| --------- | :--: | ------------------------------------------------------------ |
| bEnable | boolean | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
// Turn on the speaker
context.EnableSpeaker(true);
```

### Getting the speaker status

This API is used to get the speaker status. 0 indicates that the speaker is off, and 1 is on.

#### API prototype  

```
GetSpeakerState() :number
```

#### Sample code  

```
context.GetSpeakerState();
```

### Enabling or disabling playback device

This API is used to enable/disable a playback device.

#### API prototype  

```
EnableAudioPlayDevice(enable:boolean) :number
```

| Parameter | Type | Description |
| --------- | :--: | ------------------------------------------------------------ |
| enable | boolean | To disable a playback device, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
context.EnableAudioPlayDevice(true);
```

### Getting the playback device status

This API is used to get the status of a playback device.

#### API prototype

```
IsAudioPlayDeviceEnabled() :boolean
```

#### Sample code  

```
boolean enable = context.IsAudioPlayDeviceEnabled();
```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, see the `EnableAudioPlayDevice` API.

#### API prototype  

```
EnableAudioRecv(bEnable: boolean) :number
```

| Parameter | Type | Description |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | boolean | To enable audio downstreaming, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
context.EnableAudioRecv(true);
```



### Getting audio downstreaming status

This API is used to get the status of audio downstreaming.

#### API prototype  

```
IsAudioRecvEnabled():boolean
```

#### Sample code  

```
boolean IsAudioRecv = context.IsAudioRecvEnabled();
```

### Getting the real-time speaker volume

This API is used to get the real-time speaker volume level. A number-type value will be returned to indicate the volume level. We recommend you call this API once every 20 ms.

#### API prototype  

```
GetSpeakerLevel():number
```

#### Sample code  

```
context.GetSpeakerLevel();
```

### Getting the real-time downstreaming audio levels of other members in room

This API is used to get the real-time audio downstreaming volume of other members in the room. A number-type value will be returned. Value range: 0–200.

#### API prototype  

```
GetRecvStreamLevel(openId: string) :number
```

| Parameter | Type | Description |
| ------ | :----: | --------------------- |
| openId | string | `openId` of another member in the room |

#### Sample code  

```
number level =GetRecvStreamLevel(openId);
```

### Dynamically setting the volume of a member of the room

This API is used to set the volume of a member in the room. It takes effect only on the local side.

#### API prototype  

```
SetSpeakerVolumeByOpenID(openId: string, volume:number) :number;
```

|Parameter   |Type   |Description   |
|----------|-------|-------|
|openId       |string   | `OpenID` of the target user |
|volume  |number       | Percentage. Recommended value range: 0–200. Default value: `100`. |

#### Sample code  

```
context.SetSpeakerVolumeByOpenID(openId,  100);
```

### Getting volume percentage

This API is used to get the volume level set by `SetSpeakerVolumeByOpenID`.

#### API prototype

```
GetSpeakerVolumeByOpenID(openId: string) :number;
```

|Parameter   |Type   |Description   |
|----------|-------|-------|
|openId       |string| `OpenID` of the target user |


#### Returned values

API returns volume percentage set by OpenID, where 100 is by default.

#### Sample code  

```
context.GetSpeakerVolumeByOpenID(openId);
```

### Setting the speaker volume

This API is used to set the speaker volume.

#### API prototype  

```
SetSpeakerVolume(volume:number) :number
```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------------------ |
| volume | number  | Value range: 0–200. Default value: 100. `0` indicates that the audio is mute, while `100` indicates that the volume level remains unchanged. |

#### Sample code  

```
number vol = 100;
context.SetSpeakerVolume(vol);
```

### Getting the speaker volume

This API is used to get the speaker volume. A number-type value will be returned to indicate the volume. `101` indicates that the `SetSpeakerVolume` API has not been called.
"Level" indicates the real-time volume, and "Volume" the speaker volume. The final volume = Level * Volume%. For example, if the "Level" is 100 and "Volume" is 60, the final volume is "60".

#### API prototype  

```
GetSpeakerVolume() :number
```

#### Sample code  

```
numbet volume = context.GetSpeakerVolume();
```

## Device Selection APIs

Device selection APIs can be used only on PC.

| API | Description |
| --------------------------- | :------------------: |
| GetMicListCount             |       Gets the number of mics       |
| GetMicList                  |         Enumerates mics         |
| GetSpeakerListCount         |       Gets the number of speakers       |
| GetSpeakerList              |         Enumerates speakers         |
| SelectMic                   |         Selects mics         |
| SelectSpeaker               |         Selects speakers         |

### Getting the number of mics

This API is used to get the number of mics.

#### Function prototype  

```
GetMicListCount() :number
```

#### Sample code  

```
var micListCount = context.GetMicListCount();
```

### Enumerating mics

This API is used together with the `GetMicListCount` API to enumerate mics.

#### Function prototype 

```
GetMicList() :GmeAudioDeviceInfo[];
```

#### Sample code  

```
var micList = context.GetMicList();
```

### Selecting mic

This API is used to select a mic. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default mic will be selected.
The 0th device id returned in the GetMicList API is the default device of the call device. If there is a selected call device, it will be maintained by service. If it is unplugged, the call device will be changed back into the default device.

#### Function prototype  

```
SelectMic(micId: string) :number;
```

| Parameter   |  Type  | Description         |
| ------ | :---: | ------------- |
| micId | string | Mic ID, which is from the list returned by `GetMicList`. |

#### Sample code  

```
context.SelectMic(deviceID);
```

This API is used to get the number of speakers.

#### Function prototype  

```
 GetSpeakerListCount() :number;
```

#### Sample code  

```
context.GetSpeakerListCount();
```

### Enumerating speakers

This API is used together with the `GetSpeakerListCount` API to enumerate speakers.

#### Function prototype  

```
GetSpeakerList(): GmeAudioDeviceInfo[]
```

#### Sample code  

```
var speakList = GetSpeakerList();
```

### Selecting speaker

This API is used to select a playback device. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default playback device will be selected.

#### Function prototype  

```
SelectSpeaker(speakerId: string) :number
```

| Parameter       | Type  | Description          |
| ---------- | :---: | ------------- |
| speakerId | string | Speaker ID, which is from the list returned by `GetSpeakerList`. |

#### Sample code  

```
var ret = SelectSpeaker(deviceID);
```

## Advanced APIs

### Enabling in-ear monitoring

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### API prototype  

```
EnableLoopBack(bEnable: boolean) :number
```

| Parameter    | Type   | Description                                                                                                                    |
| ------ | :--: | ------------ |
| enable | boolean | Specifies whether to enable in-ear monitoring. |

#### Sample code  

```
context.EnableLoopBack(true);
```

### Getting user's room audio type

This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, see the `EnterRoom` API.

#### API prototype  

```
GetRoomType() :number
```

#### Sample code  

```
context.GetRoomType();
```

### Changing the room type

This API is used to modify a user's room audio type. For the result, see the callback event. The event type is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE`. The audio type of the room is determined by the first user to enter the room. After that, if a member in the room changes the room type, it will take effect for all members there.
#### API prototype  

```
ChangeRoomType(roomType: number) :number
```

| Parameter | Type | Description |
| -------- | :----------: | ----------------------------------------------------- |
| roomtype | number | Room type to be switched to. For room audio types, see the `EnterRoom` API.  |

#### Sample code  

```
context.ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```

#### Callback event

After the room type is set, the event message `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE` will be returned in the callback. The returned parameters include `result`, `error_info`, and `new_room_type`. The `new_room_type` represents the following information. The event message will be identified in the `OnEvent` function.

| Event Subtype | Parameter | Description |
| -------- | :----: | ------------------------------------------------------------ |
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM | 1 | Indicates that the existing audio type is inconsistent with and changed to that of the entered room. |
| ITMG_ROOM_CHANGE_EVENT_START | 2 | Indicates that a user is already in the room and the audio type starts changing (e.g., calling the `ChangeRoomType` API to change the audio type). |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE | 3 | Indicates that a user is already in the room and the audio type has been changed. |
| ITMG_ROOM_CHANGE_EVENT_REQUEST | 4 | Indicates that a room member calls the `ChangeRoomType` API to request a change of room audio type. |

#### Sample code  

```
context.setTMGDelegate(function(eventId, msg){
  if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
        {
        // Process room type events
     }
});
```

### The monitoring event of room call quality

This is the quality monitoring event used to listen on the network quality. If your network conditions are poor, the business layer will ask you to switch the network through the UI. This event is triggered once every two seconds after room entry, and its message is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| weight | number   | Value range: 1–50. `50` indicates excellent sound quality, `1` indicates very poor (barely usable) sound quality, and `0` represents an initial meaningless value. Generally, if the value is below 30, you can remind users that the network is poor and recommend them to switch the network. |
| loss   | var | Upstream packet loss rate |
| delay  | number    | Voice chat delay in ms |




### Getting version number

This API is used to get the SDK version number for analysis.

#### API prototype

```
GetSDKVersion() :string
```

#### Sample code  

```
context.GetSDKVersion();
```
### Setting the application name and version

This API is used to set the application name and version.

#### API prototype

```
SetAppVersion(appVersion: string) : number
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| appVersion | string | Application name and version |

#### Sample code  

```
context.SetAppVersion("gme V2.0.0");
```



### Setting log printing level

This API is used to set the level of logs to be printed, and needs to be called before the initialization. It is recommended to keep the default level.

#### API prototype

```
SetLogLevel(level: number) : number
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| level | number | Sets the log level. `TMG_LOG_LEVEL_NONE` indicates not to log. Default value: `TMG_LOG_LEVEL_INFO`. |

`level` description:

| Value of `level`       | Description                 |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE | Does not print logs |
| TMG_LOG_LEVEL_ERROR | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO | Prints info logs |
| TMG_LOG_LEVEL_DEBUG | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE | Prints verbose logs |

#### Sample code  

```
context.SetLogLevel(TMG_LOG_LEVEL_INFO);
```



### Setting the log printing path

This API is used to set the log printing path. The default path is as follows. It needs to be called before initialization.

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\GMEGLOBAL\GME\ProcessName                            |

#### API prototype

```
SetLogPath(logPath: string)
```

| Parameter | Type | Description |
| ------ | :----: | ---- |
| logPath | string | Path |

#### Sample code  

```
string logDir = ""// Set a path by yourself
context.SetLogPath(logDir);
```

### Getting the diagnostic messages

This API is used to get information on the quality of real-time audio/video calls, which is mainly used to view real-time call quality and troubleshoot and can be ignored on the business side.

#### API prototype  

```
GetQualityTips() :string
```

#### Sample code  

```
string tips = context.GetQualityTips();
```

### Callback message

| Message |  Description  | Data | Example｜
| -------- | ---------- | ---------------------- | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | A member entered the audio room | result; error_info |{"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | A member exited the audio room | result; error_info |{"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | The room was disconnected for network or other reasons | result; error_info |{"error_info":"waiting timeout, please check your network","result":0} |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | Room members were updated | user_list; event_id |{"event_id":1,"user_list":["0"]} |
| ITMG_MAIN_EVENT_TYPE_RECONNECT_START | The reconnection to the room started | result; error_info |{"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS | The reconnection to the room succeeded | result; error_info |{"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_SWITCH_ROOM | The room was quickly switched | result; error_info |{"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | The room status was changed |result; error_info; sub_event_type; new_room_type|{"error_info":"","new_room_type":0,"result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_START | Cross-room mic connect started | result; |{"result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_SHARING_STOP | Cross-room mic connect stopped | result; |{"result":0}|
| ITMG_MAIN_EVENT_TYPE_SPEAKER_DEFAULT_DEVICE_CHANGED | The default speaker device was changed | result; error_info |{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE | A new speaker device was added | result; error_info |{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE | A speaker device was lost | result; error_info |{"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE | A new mic device was added | result; error_info |{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE | A mic device was lost | result; error_info |{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_DEFAULT_DEVICE_CHANGED | The default mic device was changed | result; error_info |{"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY | The room quality changed | weight; loss; delay |{"weight":5,"loss":0.1,"delay":1} |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE | Voice message recording was completed | result; file_path |{"file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE | Voice message upload was completed | result; file_path;file_id |{"file_id":"","file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE | Voice message download was completed | result; file_path;file_id |{"file_id":"","file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE | Voice message playback was completed |result; file_path |{"file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE | Fast speech-to-text conversion was completed | result; text;file_id |{"file_id":"","text":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE | Streaming speech-to-text conversion was completed | result; file_path; text;file_id |{{"file_id":"","file_path":","text":"","result":0}} |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING | Streaming speech-to-text conversion is in progress | result; file_path; text;file_id |{{"file_id":"","file_path":","text":"","result":0}} |
| ITMG_MAIN_EVNET_TYPE_PTT_TEXT2SPEECH_COMPLETE | Text-to-speech conversion was completed | result; text;file_id |{{"file_id":"","text":"","result":0}} |
| ITMG_MAIN_EVNET_TYPE_PTT_TRANSLATE_TEXT_COMPLETE | Text translation was completed | result; text;file_id |{{"file_id":"","text":"","result":0}} |

​	

